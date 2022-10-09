# NewIP内核协议栈介绍


## 基本概念

NewIP在现有IP能力的基础上，以灵活轻量级报头和可变长多语义地址为基础，通过二三层协议融合，对协议去冗和压缩，减少冗余字节，实现高能效比，高净吞吐，提升通信效率。打造终端之间高效的横向通信，支撑超级终端的体验，实现异构网络的端到端互联。

目前WiFi协议报文，三层报头和地址开销使得报文开销大，传输效率较低。

![zh-cn_image-20220915162621809](figures/zh-cn_image-20220915162621809.png)

```
IPv4地址长度固定4字节，IPv6地址长度固定16字节。
IPv4网络层报头长度20~60字节，IPv6网络层报头长度40字节。
```

NewIP支持**可变长多语义地址（最短1字节）**，**可变长定制化报头封装（最短5字节）**，通过精简报文头开销，提升数据传输效率。

NewIP报头开销，相比IPv4节省25.9%，相比IPv6节省44.9%。

NewIP载荷传输效率，相比IPv4提高最少1%，相比IPv6提高最少2.33%。

| 对比场景       | 报头开销     | 载荷传输效率（WiFi MTU=1500B，BT MTU=255B） |
| -------------- | ------------ | ------------------------------------------- |
| IPv4 for WiFi  | 30+8+20=58 B | (1500-58)/1500=96.13%                       |
| IPv6 for WiFi  | 30+8+40=78 B | (1500-78)/1500=94.8%                        |
| NewIP for WiFi | 30+8+5=43 B  | (1500-43)/1500=97.13%                       |

## 可变长报头格式

NewIP WiFi灵活极简报文头如下图所示，通过LLC Header中的EtherType = 0xEADD标识NewIP灵活极简报文。Bitmap是一组由0和1组成的二进制序列，每个二进制位的数值用于表示特定目标特性的存在性。

![zh-cn_image-20220915140627223](figures/zh-cn_image-20220915140627223.png)

NewIP Eth灵活极简报文头如下图所示，通过Eth头中的EtherType = 0xEADD标识NewIP灵活极简报文。

![zh-cn_image-20220930113757464](figures/zh-cn_image-20220930113757464.png)

1)	Dispatch：指示封装子类，数值0b0表示其为极简封装子类，长度为1比特；(0b表示后面数值为二进制)。

2)	Bitmap：变长，Bitmap默认为紧跟在Dispatch有效位后面的7比特，Bitmap字段长度可持续扩展。Bitmap最后一位置0表示Bitmap结束，最后一位置1表示Bitmap向后扩展1 Byte，直至最后一位置0。
3)	Value: 标识字段的值，长度为1 Byte的整数倍，类型及长度由报头字段语义表确定。

**Bitmap字段定义如下：**

| 极简Bitmap标识             | Bitops | 字段长度         | 置位策略       | 备注                                    |
| -------------------------- | ------ | ---------------- | -------------- | --------------------------------------- |
| Bitmap 1st Byte:           | -      | -                | -              | -                                       |
| 标记位Dispatch             | 0      | 不表示具体字段   | 置0            | 0：极简帧，1：普通帧。                  |
| TTL                        | 1      | 1 Byte           | 置1            | 剩余跳数。                              |
| Total Length               | 2      | 2 Byte           | UDP置0，TCP置1 | NewIP报文总长度（包含报头长度）。       |
| Next Header                | 3      | 1 Byte           | 置1            | 协议类型。                              |
| Reserve                    | 4      | 保留             | 置0            | 保留字段。                              |
| Dest Address               | 5      | 变长（1~8 Byte） | 置1            | 目的地址。                              |
| Source Address             | 6      | 变长（1~8 Byte） | 由协议自行确定 | 源地址。                                |
| 标记位，标志是否有2nd Byte | 7      | 不表示具体字段   | -              | 0：bitmap结束，1：后跟另外8bit bitmap。 |
| Bitmap 2nd Byte:           | -      | -                | -              | -                                       |
| Header Length              | 0      | 1 Byte           | -              | NewIP报头长度。                         |
| Reserve                    | 1      | 保留             | 置0            | -                                       |
| Reserve                    | 2      | 保留             | 置0            | -                                       |
| Reserve                    | 3      | 保留             | 置0            | -                                       |
| Reserve                    | 4      | 保留             | 置0            | -                                       |
| Reserve                    | 5      | 保留             | 置0            | -                                       |
| Reserve                    | 6      | 保留             | 置0            | -                                       |
| 标记位，标志是否有3rd Byte | 7      | 不表示具体字段   | 置0            | 0：bitmap结束，1：后跟另外8bit bitmap。 |

NewIP数据报头（极简模式）解析遇到新bitmap字段时的处理方法：

仅解析当前版本协议中已定义的bitmap字段，从第一个未知语义的bitmap字段开始，跳过后面的所有bitmap字段，直接通过header length定位到报文开始位置并解析报文。如果报头中携带了未知语义的bitmap字段，且未携带header length字段，则丢弃该数据包。

## 可变长地址格式

NewIP采用自解释编码，编码格式如下所示：

| First Byte | Semantics                                                    | 地址段有效范围                                               |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 0x00       | Address is 0                                                 | 【1字节】0 ~ 220 (0x00 ~ 0xDC)                               |
| 0x01       | Address is 1                                                 | -                                                            |
| 0x02       | Address is 2                                                 | -                                                            |
| ...        | ...                                                          | -                                                            |
| 0xDC       | Address is 220                                               | -                                                            |
| 0xDD       | An 16-bit address, which is 0 + 256 * (0xDD - 0xDD) + the last byte value | 【2字节】221 ~ 255 (0x**DD**DD ~ 0x**DD**FF)                 |
| 0xDE       | An 16-bit address, which is 0 + 256 * (0xDE - 0xDD) + the last byte value | 【2字节】256 ~ 511 (0x**DE**00 ~ 0x**DE**FF)                 |
| 0xDF       | An 16-bit address, which is 0 + 256 * (0xDF - 0xDD) + the last byte value | 【2字节】512 ~ 767 (0x**DF**00 ~ 0x**DF**FF)                 |
| ...        | ...                                                          | -                                                            |
| 0xF0       | An 16-bit address, which is 0 + 256 * (0xF0 - 0xDD) + the last byte value | 【2字节】4864 ~ 5119 (0x**F0**00 ~ 0x**F0**FF)               |
| 0xF1       | An 16-bit address is followed                                | 【3字节】5120 ~ 65535 (0x**F1** 1400 ~ 0x**F1** FFFF)        |
| 0xF2       | An 32-bit address is followed                                | 【5字节】65536 ~ 4,294,967,295 (0x**F2** 0001 0000 ~ 0x**F2** FFFF FFFF) |
| 0xF3       | An 48-bit address is followed                                | 【7字节】4,294,967,296 ~ 281,474,976,710,655 (0x**F3** 0001 0000 0000 ~ 0x**F3** FFFF FFFF FFFF) |
| 0xFE       | An 56-bit address is followed                                | 【8字节】0 ~ 72,057,594,037,927,935 (0x**FE**00 0000 0000 0000 ~ 0x**FE**FF FFFF FFFF FFFF) |



## NewIP配置指导

启用NewIP，需要通过编译内核时打开相应的配置项及依赖，NewIP相关CONFIG如下：

```c
CONFIG_NEWIP=y          // 使能NewIP内核协议栈
CONFIG_NEWIP_HOOKS=y    // 使能NewIP内核侵入式修改插桩函数注册，使能NewIP的同时必须使用NewIP插桩功能
```

另有部分CONFIG被依赖：

```c
VENDOR_HOOKS=y          // 使能内核插桩基础框架
```

备注：

1. 只在Linux 5.10内核上支持NewIP内核协议栈。
2. 鸿蒙linux内核要求所有原生内核代码侵入式修改，都要修改成插桩方式。

```c
/* 将NewIP ehash函数注册到内核 */
register_trace_ninet_ehashfn_hook(&ninet_ehashfn_hook, NULL);


/* 下面是IPv4，IPv6协议栈总入口函数，在总入口函数内新增NewIP协议栈相关处理 */
static u32 sk_ehashfn(const struct sock *sk)
{
    /* IPv6 */
#if IS_ENABLED(CONFIG_IPV6)
	if (sk->sk_family == AF_INET6 &&
	    !ipv6_addr_v4mapped(&sk->sk_v6_daddr))
		return inet6_ehashfn(sock_net(sk),
				     &sk->sk_v6_rcv_saddr, sk->sk_num,
				     &sk->sk_v6_daddr, sk->sk_dport);
#endif

#if IS_ENABLED(CONFIG_NEWIP_HOOKS)
	if (sk->sk_family == AF_NINET) {
		u32 ret = 0;

        /* NewIP注册的ehash函数 */
		trace_ninet_ehashfn_hook(sock_net(sk), &sk->sk_nip_rcv_saddr, sk->sk_num,
					 &sk->sk_nip_daddr, sk->sk_dport, &ret);
		return ret;
	}
#endif

    /* IPv4 */
	return inet_ehashfn(sock_net(sk),
			    sk->sk_rcv_saddr, sk->sk_num,
			    sk->sk_daddr, sk->sk_dport);
}
```



代码编译完成后，通过下面命令可以确认newip协议栈代码是否使能成功。

```c
find out/ -name *nip*.o
out/rk3568/obj/third_party/glib/glib/glib_source/guniprop.o
out/kernel/OBJ/linux-5.10/net/newip/nip_addrconf_core.o
out/kernel/OBJ/linux-5.10/net/newip/nip_hdr_decap.o
out/kernel/OBJ/linux-5.10/net/newip/nip_addr.o
out/kernel/OBJ/linux-5.10/net/newip/nip_checksum.o
out/kernel/OBJ/linux-5.10/net/newip/tcp_nip_output.o
...
```

禁用NewIP内核协议栈，删除CONFIG_NEWIP使能开关，删除out/kernel目录后重新编译。

```c
# CONFIG_NEWIP is not set
# CONFIG_NEWIP_HOOKS is not set
```

## NewIP相关接口

用户态应用程序调用Socket API创建NewIP socket，采用NewIP极简帧头封装进行收发包，NewIP协议socket接口列表如下：

| 函数     | 输入                                                         | 输出                                           | 返回值           | 接口具体描述                                                 |
| -------- | ------------------------------------------------------------ | ---------------------------------------------- | ---------------- | ------------------------------------------------------------ |
| socket   | int **domain**, int type, int **protocol**                   | NA                                             | Socket句柄sockfd | 创建NewIP 协议类型socket，并返回socket实例所对应的句柄。**domain参数填写 AF_NINET，表示创建NewIP协议类型socket。protocol参数填写IPPROTO_TCP或IPPROTO_UDP**。 |
| bind     | int sockfd, const **struct sockaddr_nin** *myaddr, socklen_t addrlen | NA                                             | int，返回错误码  | 将创建的socket绑定到指定的IP地址和端口上。**myaddr->sin_family填写AF_NINET**。 |
| listen   | int socket, int backlog                                      | NA                                             | int，返回错误码  | 服务端监听NewIP地址和端口。                                  |
| connect  | int sockfd, const **struct sockaddr_nin** *addr, aocklen_t addrlen | NA                                             | int，返回错误码  | 客户端创建至服务端的连接。                                   |
| accept   | int sockfd, **struct sockaddr_nin** *address, socklen_t *address_len | NA                                             | 返回socket的fd   | 服务端返回已建链成功的socket。                               |
| send     | int sockfd, const void *msg, int len, unsigned int flags, const **struct sockaddr_nin** *dst_addr, int addrlen | NA                                             | int，返回错误码  | 用于socket已连接的NewIP类型数据发送。                        |
| recv     | int sockfd, size_t len, int flags, **struct sockaddr_nin** *src_addr, | void  **buf, int* *fromlen                     | int，返回错误码  | 用于socket已连接的NewIP类型数据接收。                        |
| close    | int sockfd                                                   | NA                                             | int，返回错误码  | 关闭socket，释放资源。                                       |
| ioctl    | int sockfd, unsigned long cmd, ...                           | NA                                             | int，返回错误码  | 对NewIP协议栈相关信息进行查询或更改。                        |
| sendto   | int sockfd, const void *msg, int len, unsigned int flags, const **struct sockaddr** *dst_addr, int addrlen | NA                                             | int，返回错误码  | 用于socket无连接的NewIP类型数据发送。                        |
| recvfrom | int sockfd, size_t len, int flags,                           | void *buf, struct sockaddr *from, int *fromlen | int，返回错误码  | 用于socket无连接的NewIP类型数据接收。                        |

NewIP短地址结构如下：

```c
enum nip_8bit_addr_index {
	NIP_8BIT_ADDR_INDEX_0 = 0,
	NIP_8BIT_ADDR_INDEX_1 = 1,
	NIP_8BIT_ADDR_INDEX_2 = 2,
	NIP_8BIT_ADDR_INDEX_3 = 3,
	NIP_8BIT_ADDR_INDEX_4 = 4,
	NIP_8BIT_ADDR_INDEX_5 = 5,
	NIP_8BIT_ADDR_INDEX_6 = 6,
	NIP_8BIT_ADDR_INDEX_7 = 7,
	NIP_8BIT_ADDR_INDEX_MAX,
};

enum nip_16bit_addr_index {
	NIP_16BIT_ADDR_INDEX_0 = 0,
	NIP_16BIT_ADDR_INDEX_1 = 1,
	NIP_16BIT_ADDR_INDEX_2 = 2,
	NIP_16BIT_ADDR_INDEX_3 = 3,
	NIP_16BIT_ADDR_INDEX_MAX,
};

enum nip_32bit_addr_index {
	NIP_32BIT_ADDR_INDEX_0 = 0,
	NIP_32BIT_ADDR_INDEX_1 = 1,
	NIP_32BIT_ADDR_INDEX_MAX,
};

#define nip_addr_field8 v.u.field8
#define nip_addr_field16 v.u.field16
#define nip_addr_field32 v.u.field32

#pragma pack(1)
struct nip_addr_field {
	union {
		unsigned char   field8[NIP_8BIT_ADDR_INDEX_MAX];
		unsigned short field16[NIP_16BIT_ADDR_INDEX_MAX]; /* big-endian */
		unsigned int   field32[NIP_32BIT_ADDR_INDEX_MAX]; /* big-endian */
	} u;
};

struct nip_addr {
	unsigned char bitlen;	/* The address length is in bit (not byte) */
	struct nip_addr_field v;
};
#pragma pack()

/* The following structure must be larger than V4. System calls use V4.
 * If the definition is smaller than V4, the read process will have memory overruns
 * v4: include\linux\socket.h --> sockaddr (16Byte)
 */
#define POD_SOCKADDR_SIZE 3
struct sockaddr_nin {
	unsigned short sin_family; /* [2Byte] AF_NINET */
	unsigned short sin_port;   /* [2Byte] Transport layer port, big-endian */
	struct nip_addr sin_addr;  /* [9Byte] NIP address */

	unsigned char sin_zero[POD_SOCKADDR_SIZE]; /* [3Byte] Byte alignment */
};
```

## NewIP开发说明

目前只在鸿蒙Linux-5.10内核支持NewIP内核协议栈，只能在用户态人工配置NewIP地址和路由到内核，两台设备可以通过路由器WiFi连接，也可以通过Eth网线直接连接。如果想配置NewIP地址和路由后自动切换到NewIP内核协议栈通信，应用可以参考下面蓝框中描述。

![zh-cn_image-20221009112548444](figures/zh-cn_image-20221009112548444.png)

上图中NewIP地址，路由配置程序可以参考[代码仓examples代码](https://gitee.com/openharmony-sig/communication_sfc_newip/tree/master/examples)，根据CPU硬件差异更改Makefile中CC定义编译成二级制文件后推送到开发板，参考上图命令给设备配置NewIP地址和路由。

| 文件名             | 功能                                                   |
| ------------------ | ------------------------------------------------------ |
| nip_addr.c         | NewIP可变长地址配置demo代码（可配置任意有效NewIP地址） |
| nip_route.c        | NewIP路由配置demo代码（可配置任意有效NewIP地址）       |
| check_nip_enable.c | 获取本机NewIP能力                                      |

设备1上查看NewIP地址和路由：

```sh
dev-1@localhost:~# cat /proc/net/nip_addr
01          wlan0
dev-1@localhost:~#
dev-1@localhost:~#
dev-1@localhost:~# cat /proc/net/nip_route
02      ff09       1 wlan0        # 到设备2的路由
01      01      2149580801 wlan0  # 本机自发自收路由
```

设备2上查看NewIP地址和路由：

```sh
dev-2@localhost:~# cat /proc/net/nip_addr
02          wlan0
dev-2@localhost:~#
dev-2@localhost:~#
dev-2@localhost:~#
dev-2@localhost:~# cat /proc/net/nip_route
01      ff09       1 wlan0        # 到设备1的路由
02      02      2149580801 wlan0  # 本机自发自收路由
```

## NewIP收发包代码示例

NewIP可变长地址配置，路由配置，UDP/TCP收发包demo代码链接如下，NewIP协议栈用户态接口使用方法可以参考[代码仓examples代码](https://gitee.com/openharmony-sig/communication_sfc_newip/tree/master/examples)。demo代码内配置固定地址和路由，执行编译后二进制程序时不需要人工指定地址和路由。

| 文件名                | 功能                          |
| --------------------- | ----------------------------- |
| nip_addr_cfg_demo.c   | NewIP可变长地址配置demo代码   |
| nip_route_cfg_demo.c  | NewIP路由配置demo代码         |
| nip_udp_server_demo.c | NewIP UDP收发包服务端demo代码 |
| nip_udp_client_demo.c | NewIP UDP收发包客户端demo代码 |
| nip_tcp_server_demo.c | NewIP TCP收发包服务端demo代码 |
| nip_tcp_client_demo.c | NewIP TCP收发包客户端demo代码 |
| nip_lib.c             | 接口索引获取等API接口demo代码 |

**基础操作步骤：**

![zh-cn_image-20220915165414926](figures/zh-cn_image-20220915165414926.png)

1、将demo代码拷贝到Linux编译机上，make clean，make all编译demo代码。

2、将编译生成二级制文件上传到设备1，设备2。

3、执行“ifconfig xxx up”开启网卡设备，xxx表示网卡名，比如eth0，wlan0。

4、在设备1的sh下执行“./nip_addr_cfg_demo server”给服务端配置0xDE00（2字节）变长地址，在设备2的sh下执。行“./nip_addr_cfg_demo client”给客户端配置0x50（1字节）变长地址，通过“cat /proc/net/nip_addr”查看内核地址配置结果。

5、在设备1的sh下执行“./nip_route_cfg_demo server”给服务端配置路由，在设备2的sh下执行“./nip_route_cfg_demo client”给客户端配置路由，通过“cat /proc/net/nip_route”查看内核路由配置结果。

以上步骤操作完成后，可以进行UDP/TCP收发包，收发包demo默认使用上面步骤中配置的地址和路由。



**UDP收发包操作步骤：**

先在服务端执行“./nip_udp_server_demo”，然后再在客户端执行“./nip_udp_client_demo”，客户端会发送10个NewIP报文，客户端收到报文后再发送给服务端。

```
服务端sh窗口打印内容：
Received -- 1661826989 498038 NIP_UDP #      0 -- from 0x50:57605
Sending  -- 1661826989 498038 NIP_UDP #      0 -- to 0x50:57605
Received -- 1661826990  14641 NIP_UDP #      1 -- from 0x50:57605
Sending  -- 1661826990  14641 NIP_UDP #      1 -- to 0x50:57605
Received -- 1661826990 518388 NIP_UDP #      2 -- from 0x50:57605
Sending  -- 1661826990 518388 NIP_UDP #      2 -- to 0x50:57605
...
Received -- 1661827011 590576 NIP_UDP #      9 -- from 0x50:37758
Sending  -- 1661827011 590576 NIP_UDP #      9 -- to 0x50:37758

客户端sh窗口打印内容：
Received --1661827007  55221 NIP_UDP #      0 sock 3 success:     1/     1/no=     0
Received --1661827007 557926 NIP_UDP #      1 sock 3 success:     2/     2/no=     1
Received --1661827008  62653 NIP_UDP #      2 sock 3 success:     3/     3/no=     2
...
Received --1661827011 590576 NIP_UDP #      9 sock 3 success:    10/    10/no=     9
```



**TCP收发包操作步骤：**

先在服务端执行“./nip_tcp_server_demo”，然后再在客户端执行“./nip_tcp_client_demo”，客户端会发送10个NewIP报文，客户端收到报文后再发送给服务端。

```
服务端sh窗口打印内容：
Received -- 1661760202 560605 NIP_TCP #      0 --:1024
Sending  -- 1661760202 560605 NIP_TCP #      0 --:1024
Received -- 1661760203  69254 NIP_TCP #      1 --:1024
Sending  -- 1661760203  69254 NIP_TCP #      1 --:1024
Received -- 1661760203 571604 NIP_TCP #      2 --:1024
Sending  -- 1661760203 571604 NIP_TCP #      2 --:1024
...
Received -- 1661760207  86544 NIP_TCP #      9 --:1024
Sending  -- 1661760207  86544 NIP_TCP #      9 --:1024

客户端sh窗口打印内容：
Received --1661760202 560605 NIP_TCP #      0 sock 3 success:     1/     1/no=     0
Received --1661760203  69254 NIP_TCP #      1 sock 3 success:     2/     2/no=     1
...
Received --1661760207  86544 NIP_TCP #      9 sock 3 success:    10/    10/no=     9
```

## selinux规则说明

用户态进程操作NewIP socket需要添加selinux policy，否则操作会被拦截。

```sh
# base\security\selinux\sepolicy\ohos_policy\xxx\xxx.te
# socket 基础操作
# avc:  denied  { create } for  pid=540 comm="thread_xxx" scontext=u:r:thread_xxx:s0 tcontext=u:r:thread_xxx:s0 tclass=socket permissive=0
allow thread_xxx thread_xxx:socket { create bind connect listen accept read write shutdown setopt getopt };

# ioctl 操作
# 操作码在 linux-xxx\include\uapi\linux\sockios.h 中定义
# 0x8933 : name -> if_index mapping
# 0x8916 : set PA address
# 0x890B : add routing table entry
allowxperm thread_xxx thread_xxx:socket ioctl { 0x8933 0x8916 0x890B };
```

## WireShark报文解析模板

### 模板导入

Wireshark默认报文解析规则无法解析NewIP报文，在WireShark配置中添加NewIP报文解析模板可以实现NewIP报文解析，[NewIP报文解析模板](https://gitee.com/openharmony-sig/communication_sfc_newip/blob/master/tools/wireshark_cfg_for_newip.lua)详见代码仓。

报文解析模板配置文件的方法：

依次点击Help->About Wireshark->Folders，打开Global Configuration目录，编辑init.lua文件。在末尾添加dofile(DATA_DIR..”newip.lua”)，其中DATA_DIR即为newip.lua插件所在路径。

![zh-cn_image-20220930141628922](figures/zh-cn_image-20220930141628922.png)

NewIP报文解析模板添加样例：

```
NewIP报文解析模板存放路径：
D:\tools\WireShark\wireshark_cfg_for_newip.lua

WireShark配置文件路径：
C:\Program Files\Wireshark\init.lua

在init.lua文件最后增加下面配置（window 11）
dofile("D:\\tools\\WireShark\\wireshark_cfg_for_newip.lua")
```

### 报文解析样例

#### ARP请求

![zh-cn_image-20220930142806235](figures/zh-cn_image-20220930142806235.png)

#### ARP应答

![zh-cn_image-20220930142858397](figures/zh-cn_image-20220930142858397.png)

#### TCP握手

![zh-cn_image-20220930142912014](figures/zh-cn_image-20220930142912014.png)

#### TCP数据包

![zh-cn_image-20220930142920255](figures/zh-cn_image-20220930142920255.png)
