# ProcessRunningInfo<sup>(deprecated)</sup>

ProcessRunningInfo模块提供对进程运行信息进行设置和查询的能力。

> **说明：**
> 
> 本模块首批接口从API Version 9 开始废弃，建议使用[ProcessRunningInformation<sup>9+</sup>](js-apis-processrunninginformation.md)替代。

## 使用说明

通过appManager来获取。

```js
import appManager from '@ohos.application.appManager';
appManager.getProcessRunningInfos((error,data) => { 
    console.log("getProcessRunningInfos error: "  + error.code + " data: " + JSON.stringify(data));
});
```

## 属性

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Mission

| 名称 | 参数类型 | 可读 | 可写 | 说明 | 
| -------- | -------- | -------- | -------- | -------- |
| pid | number | 是 | 否 | 进程ID。 | 
| uid | number | 是 | 否 | 用户ID。 | 
| processName | string | 是 | 否 | 进程名称。 | 
| bundleNames | Array&lt;string&gt; | 是 | 否 | 进程中所有运行的包名称。 | 
