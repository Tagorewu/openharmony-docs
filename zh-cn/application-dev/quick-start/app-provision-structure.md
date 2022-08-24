#  HarmonyAppProvision配置文件的说明
在应用的开发过程中，应用的权限、签名信息等需要在HarmonyAppProvision配置文件（该文件在部分文档中也称为profile文件）中声明。

## 配置文件的内部结构
HarmonyAppProvision文件包含version-code对象、version-name对象、uuid对象、type对象、issuer对象、validity对象、bundle-info对象、acls对象、permissions对象、debug-info对象等部分组成。

**表1** 配置文件内部结构说明
| 属性名称     | 含义                                                                                     | 数据类型 | 是否必选 | 是否可缺省 |
| ----------- | ---------------------------------------------------------------------------------------- | -------- | -------- | -------- |
| version-code | 表示HarmonyAppProvision文件格式的版本号，取值范围为二进制32位以内的正整数。 | 数值   | 必选 | 不可缺省                 |
| version-name     | 表示版本号的文字描述，推荐使用三段数字版本号，如A.B.C。        | 字符串   | 必选 | 不可缺省 |
| uuid    | 表示文件的唯一ID号，用于OEM厂商标识HarmonyAppProvision文件，开源社区版本该属性不做强制要求。                       | 字符串     | 必选 | 不可缺省 |
| type | 表示HarmonyAppProvision文件的类型， 系统预定义的文件类型包括：debug（用于应用调试场景）和release（用于应用发布场景） ，开源社区版本该属性值建议为debug。 | 字符串     | 必选 | 不可缺省 |
| issuer | 表示HarmonyAppProvision签发者。        | 字符串     | 必选 | 不可缺省 |
| validity    | 表示HarmonyAppProvision文件有效期的信息。参考[validity对象内部结构](#validity对象内部结构)。  | 对象     | 必选 | 不可缺省  |
| bundle-info | 表示应用包以及开发者的信息。参考[bundle-info对象内部结构](#bundle-info对象内部结构)。         | 对象     | 必选 | 不可缺省  |
| acls        | 表示授权的acl权限信息。参考[acls对象内部结构](#acls对象内部结构)。                           | 对象     | 可选 | 不可缺省    |
| permissions | 表示允许使用的受限敏感权限信息。参考[permissions对象内部结构](#permissions对象内部结构)。      | 对象     | 可选 | 不可缺省    |
| debug-info  | 表示应用调试场景下的额外信息。参考[debug-info对象内部结构](#debug-info对象内部结构)。          | 对象     | 可选 | 不可缺省         |

HarmonyAppProvision文件示例：
```json
{
    "version-code": 1,
    "version-name": "1.0.0",
	"uuid": "string",
	"type": "debug",
	"validity": {
		"not-before": 1586422743,
		"not-after": 1617958743
	},
	"bundle-info" : {
		"developer-id": "OpenHarmony",
		"development-certificate": "Base64 string",
		"distribution-certificate": "Base64 string",
		"bundle-name": "com.OpenHarmony.app.test",
		"apl": "normal",
        "app-feature": "hos_normal_app"
	},
	"acls": {
		"allowed-acls": ["string"]
    },
	"permissions": {
		"restricted-permissions": ["string"]
    },
    "debug-info" : {
	    "device-id-type": "udid",
	    "device-ids": ["string"]
    },
    "issuer": "OpenHarmony"
}

```


### validity对象内部结构
| 属性名称    | 含义                            | 数据类型 | 是否必选 | 是否可缺省 |
| ---------- | ------------------------------- | ------- | ------- | --------- |
| not-before | 表示文件有效期的开始时间，时间表示方式为unix时间戳，非负整数。 | 数值    | 必选 | 不可缺省   |
| not-after  | 表示文件有效期的结束时间，时间表示方式为unix时间戳，非负整数。 | 数值    | 必选 | 不可缺省   |

### bundle-info对象内部结构
| 属性名称                  | 含义                            | 数据类型 | 是否必选 | 是否可缺省 |
| ------------------------ | ------------------------------- | ------- | -------- | --------- |
| developer-id | 表示开发者的唯一ID号，用于OEM厂商标识开发者，开源社区版本该属性不做强制要求。 | 字符串    | 必选 | 不可缺省   |
| development-certificate  | 表示[调试证书](../security/hapsigntool-guidelines.md)的信息。 | 数值    | 当type属性为debug时，该属性必选；否则，该属性可选。   | 不可缺省   |
| distribution-certificate  | 表示[发布证书](../security/hapsigntool-guidelines.md)的信息。 | 数值    | 当type属性为release时，该标签必选；否则，该标签可选。 | 不可缺省   |
| bundle-name  | 表示应用程序的包名。 | 字符串    | 必选 | 不可缺省   |
| apl  | 表示应用程序的[apl级别](../security/accesstoken-overview.md)，系统预定义的apl包括：normal、system_basic和system_core。 | 字符串    | 必选 | 不可缺省   |
| app-feature  | 表示应用程序的类型，系统预定义的app-feature包括hos_system_app （系统应用）和hos_normal_app（普通应用）。 | 字符串    | 必选 | 不可缺省   |


### acls对象内部结构
acls对象包含已授权的[acl权限](../security/accesstoken-overview.md)。需要指出的是，开发者仍然需要在应用包配置文件（[config.json](package-structure.md)）将acls权限信息填写到reqPermissions属性中。

表4 acls对象的内部结构
| 属性名称                  | 含义                            | 数据类型 | 是否必选 | 是否可缺省 |
| ------------------------ | ------------------------------- | ------- | ------- | --------- |
| allowed-acls | 表示已授权的[acl权限](../security/accesstoken-overview.md)列表。 | 字符串数组    | 可选 | 不可缺省   |

### permissions对象内部结构
permissions对象包含允许使用的受限敏感权限。不同于acls对象，permissions对象中的权限仅代表应用允许使用该敏感权限，权限最终由用户运行时授权。需要指出的是，开发者仍然需要在应用包配置文件（[config.json](package-structure.md)）将permissions权限信息填写到reqPermissions属性中。

表5 permissions对象的内部结构
| 属性名称                  | 含义                            | 数据类型 | 是否必选 | 是否可缺省 |
| ------------------------ | ------------------------------- | ------- | ------- | --------- |
| restricted-permissions | 表示允许使用的[受限敏感权限](../security/accesstoken-overview.md)。 | 字符串数组    | 可选 | 不可缺省   |

### debug-info对象内部结构
debug-info对象包含应用调试场景下的信息，主要是设备管控的信息。

表6 debug-info对象的内部结构
| 属性名称                  | 含义                            | 数据类型 | 是否必选 | 是否可缺省 |
| ------------------------ | ------------------------------- | ------- | ------- | --------- |
| device-id-type | 表示设备ID的类型，当前系统仅提供udid的设备ID类型。 | 字符串    | 可选 | 不可缺省   |
| device-ids | 表示应用调试场景下允许调试的设备ID列表。 | 字符串数组    | 可选 | 不可缺省   |