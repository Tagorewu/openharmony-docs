# 设备设置管理器

本模块提供设备设置管理能力，包括设置时间等。仅企业设备管理员应用才能调用。

> **说明**：
> 
> 本模块首批接口从API version 9 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## DeviceSettingsManager.setDateTime

setDateTime(admin: Want, time: number, callback: AsyncCallback<void>): void

设置系统时间。使用callback异步回调。

**需要权限：** ohos.permission.EDM_MANAGE_DATETIME

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager

**参数：**

| 参数名   | 类型                                  | 必填   | 说明      |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-application-Want.md) | 是    | 设备管理员应用。 |
| time  | number | 是 | 时间戳(ms)。 |
| callback | AsyncCallback<void> | 是 | 回调函数。当系统时间设置成功err为null，否则为错误对象。 |

**示例：**

```js
let wantTemp = {
    bundleName: "bundleName",
    abilityName: "abilityName",
};
let deviceSettingsMgr = enterpriseDeviceManager.getDeviceSettingsManager();
deviceSettingsMgr.setDateTime(wantTemp, 1526003846000, (error, value) => { 
    if (error) {
        console.log(error);
    } else {
        console.log(value);
    }
});
```

## DeviceSettingsManager.setDateTime

setDateTime(admin: Want, time: number): Promise<void>

设置系统时间。使用Promise异步回调。

**需要权限：** ohos.permission.EDM_MANAGE_DATETIME

**系统能力：** SystemCapability.Customization.EnterpriseDeviceManager

**参数：**

| 参数名   | 类型                                  | 必填   | 说明      |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-application-Want.md) | 是    | 设备管理员应用。 |
| time  | number | 是 | 时间戳(ms)。 |

**返回值：**

| 类型   | 说明                                  |
| ----- | ----------------------------------- |
| Promise<void> | Promise对象。无返回结果的Promise对象。 |


**示例：**

```js
let wantTemp = {
    bundleName: "bundleName",
    abilityName: "abilityName",
};
let deviceSettingsMgr = enterpriseDeviceManager.getDeviceSettingsManager();
deviceSettingsMgr.setDateTime(wantTemp, 1526003846000).then((value) => {
    console.log(value);
}).catch((error) => {
    console.log(error);
})
```
