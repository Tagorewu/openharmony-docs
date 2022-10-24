#  huks错误码

## 12000001 该子功能不支持（特性）

**错误信息**

``${messageInfo}`` mode is not support in current device.

**可能原因**
支持API，但是不支持API内部某些子特性（功能），如算法参数。

**处理步骤**

调整API参数，使用可替代可支持的参数。

## 12000002 缺少密钥算法参数
**错误信息**

Check get ``${messageInfo}`` failed. User should add ``${messageInfo}`` in param set. 

**可能原因**

使用密钥时缺少相关参数。

**处理步骤**

1. 查看errorMessage确认缺少的密钥参数。
2. 添加对应的正确的密钥参数。

## 12000003 无效的密钥算法参数

**错误信息**

``${messageInfo}`` argument is invalid. User should make sure using the correct value. 

**可能原因**

使用密钥时无效相关参数。

**处理步骤**

1. 查看errorMessage确认无效的的密钥参数名。
2. 修改对应的密钥参数。

## 12000004 文件错误

**错误信息**

Read file failed. or Write file failed. 

**可能原因**

文件操作错误。

**处理步骤**

1. 查看是否磁盘空间已经写满、文件系统是否有其他异常。
2. 清理磁盘。

## 12000005 进程通信错误

**错误信息**

IPC communication timeout. or Receive message from IPC failed.

**可能原因**

进程通信错误。

**处理步骤**

查看错误信息，排查是否进程IPC通信问题。

## 12000006 算法库操作失败

**错误信息**

Error occured in crypto engine. 

**可能原因**

该错误码表示算法库操作失败，可能原因如下。

1. 算法库加解密错误，可能是密文数据不对。
2. 密钥参数不正确。

**处理步骤**

1. 排查密文数据是否正确。
2. 排查加解密参数是否正确。

## 12000007 密钥访问失败 - 密钥已失效

**错误信息**

This credential is already invalidated permanently. 

**可能原因**

该错误码表示密钥访问失败 - 密钥已失效，可能原因如下。

1. 该密钥设置了清除密码失效的用户认证访问控制属性，清除过设备密钥导致密钥失效。
2. 该密钥设置了新录入生物特征失效的用户认证访问控制属性，由于录入过新的指纹或人脸导致该密钥失败。

**处理步骤**

1. 确认日志是哪种方式导致的认证不通过。
2. 如果使用了正确参数，但是失效控制导致认证不通过，则该密钥已经无法使用。

## 12000008 密钥访问失败 - 密钥认证失败

**错误信息**

Verify authtoken failed. 

**可能原因**

该密钥设置了用户认证访问控制属性，由于challenge参数不正确导致无法通过认证。

**处理步骤**

1. 检查userIAM认证的challenge参数组装是否正确。
2. 如果是challenge参数不正确导致，则修改正确的组装方式，使用huks生成challenge组装，并传入userIAM重新认证。

## 12000009 密钥访问失败 - 密钥访问超时

**错误信息**

This authtoken is already timeout. 

**可能原因**

该密钥设置了用户认证访问控制属性，由于使用时间窗timeout导致无法通过认证。

**处理步骤**

如果是timeout导致不正确，则重新触发密钥init并重新认证，使得认证时间和密钥init时间小于设置的timeout时间。

## 12000010 密钥操作会话数已达上限

**错误信息**

The number of session has reached limit. 

**可能原因**

同时使用huks进行密钥会话操作的调用方（同应用或者跨应用）过多，已经达到上限（15个）。

**处理步骤**

1. 检查同应用内部是否同时存在多个密钥会话操作（init)，存在则修改避免同时调用。
2. 如不存在上述情形，则可能是其它应用同时调用多个会话，通过等待其它应用释放会话后再使用。

## 12000011 目标对象不存在

**错误信息**

Queried entity does not exist. 

**可能原因**

该别名对应的密钥不存在。

**处理步骤**

1. 检查密钥别名是否拼写错误。
2. 检查改密钥别名对应的密钥是否生成成功。

## 12000012 外部错误

**错误信息**

External error ``${messageInfo}``. 

**可能原因**

外部的硬件出错，文件错误等。

**处理步骤**

拿错误码与日志在社区反馈。

## 12000013 密钥设置生物访问控制时，待绑定的凭据不存在

**错误信息**

Queried credential does not exist. 

**可能原因**

密钥绑定PIN、指纹、人脸时，未录入相关凭据。

**处理步骤**

录入相关凭据，或更改绑定凭据类型。

## 12000014 内存不足

**错误信息**

Memory is insufficient. 

**可能原因**

系统内存不足。

**处理步骤**

开发者释放部分内存或重启。

## 12000015 调用其他系统服务失败

**错误信息**

Call ``${messageInfo}`` service to do ``${messageInfo}`` failed. 

**可能原因**

其他系统服务未启动。

**处理步骤**

开发者等待一段时间后尝试再次触发调用。