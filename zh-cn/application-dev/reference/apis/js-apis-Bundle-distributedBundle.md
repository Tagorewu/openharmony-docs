# distributedBundle模块(JS端SDK接口)

本模块提供分布式包的管理

> **说明：**
>
> 本模块首批接口从API version 8 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```
import distributedBundle from '@ohos.distributedBundle';
```

## 系统能力

SystemCapability.BundleManager.DistributedBundleFramework

## 权限列表

| 权限                                       | 权限等级     | 描述               |
| ------------------------------------------ | ------------ | ------------------ |
| ohos.permission.GET_BUNDLE_INFO_PRIVILEGED | system_basic | 可查询所有应用信息 |

权限等级参考[权限等级说明](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/security/accesstoken-overview.md#%E6%9D%83%E9%99%90%E7%AD%89%E7%BA%A7%E8%AF%B4%E6%98%8E)

## distributedBundle.getRemoteAbilityInfo

getRemoteAbilityInfo(elementName: ElementName, callback: AsyncCallback&lt;RemoteAbilityInfo&gt;): void;

以异步方法根据给定的ElementName获取有关远程设备AbilityInfo信息，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：**

SystemCapability.BundleManager.DistributedBundleFramework

**系统API：**

此接口为系统接口，三方应用不支持调用

**参数：**

| 名称        | 类型                                                         | 必填 | 描述                                               |
| ----------- | ------------------------------------------------------------ | ---- | -------------------------------------------------- |
| elementName | [ElementName](js-apis-bundle-ElementName.md)                 | 是   | 获得的ElementName信息。                            |
| callback    | AsyncCallback<[RemoteAbilityInfo](js-apis-bundle-remoteAbilityInfo.md)> | 是   | 程序启动作为入参的回调函数，返回远程基本能力信息。 |



## distributedBundle.getRemoteAbilityInfo

getRemoteAbilityInfo(elementName: ElementName): Promise&lt;RemoteAbilityInfo&gt;

以异步方法根据给定的ElementName获取有关远程设备AbilityInfo信息，使用Promise形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：**

SystemCapability.BundleManager.DistributedBundleFramework

**系统API：**

此接口为系统接口，三方应用不支持调用

**参数：**

| 名称        | 类型                                         | 必填 | 描述                    |
| ----------- | -------------------------------------------- | ---- | ----------------------- |
| elementName | [ElementName](js-apis-bundle-ElementName.md) | 是   | 获得的ElementName信息。 |

**返回值：**

| 类型                                                         | 说明                              |
| ------------------------------------------------------------ | --------------------------------- |
| Promise\<[RemoteAbilityInfo](js-apis-bundle-remoteAbilityInfo.md)> | Promise形式返回远程基本能力信息。 |

## distributedBundle.getRemoteAbilityInfos

getRemoteAbilityInfos(elementNames: Array&lt;ElementName&gt;, callback: AsyncCallback&lt;Array&lt;RemoteAbilityInfo&gt;&gt;): void;

以异步方法根据给定的ElementName获取有关远程设备AbilityInfos信息，使用callback形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：**

SystemCapability.BundleManager.DistributedBundleFramework

**系统API：**

此接口为系统接口，三方应用不支持调用

**参数：**

| 名称         | 类型                                                         | 必填 | 描述                                               |
| ------------ | ------------------------------------------------------------ | ---- | -------------------------------------------------- |
| elementNames | Array<[ElementName](js-apis-bundle-ElementName.md)>          | 是   | ElementName信息,最大数组长度为10                   |
| callback     | AsyncCallback< Array<[RemoteAbilityInfo](js-apis-bundle-remoteAbilityInfo.md)>> | 是   | 程序启动作为入参的回调函数，返回远程基本能力信息。 |



## distributedBundle.getRemoteAbilityInfos

getRemoteAbilityInfos(elementNames: Array&lt;ElementName&gt;): Promise&lt;Array&lt;RemoteAbilityInfo&gt;&gt;

以异步方法根据给定的ElementName获取有关远程设备AbilityInfos信息，使用Promise形式返回结果。

**需要权限：**

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力：**

SystemCapability.BundleManager.DistributedBundleFramework

**系统API：**

此接口为系统接口，三方应用不支持调用

**参数：**

| 名称         | 类型                                                | 必填 | 描述                    |
| ------------ | --------------------------------------------------- | ---- | ----------------------- |
| elementNames | Array<[ElementName](js-apis-bundle-ElementName.md)> | 是   | ElementName信息,最大数组长度为10。 |

**返回值：**

| 类型                                                         | 说明                              |
| ------------------------------------------------------------ | --------------------------------- |
| Promise\<Array<[RemoteAbilityInfo](js-apis-bundle-remoteAbilityInfo.md)>> | Promise形式返回远程基本能力信息。 |
