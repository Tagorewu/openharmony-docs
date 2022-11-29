# 设备状态感知框架

设备状态感知框架提供设备状态感知能力，包括绝对静止和相对静止。

> **说明：**
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```js
import deviceStatus from '@ohos.devicestatus'
```

## ActivityResponse

服务响应抽象接口。

**系统能力** SystemCapability.Msdp.DeviceStatus.Stationary

### 属性

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| state | [ActivityState](#activitystate) | 是 | 否 | 设备状态变化返回值。 |

## ActivityType

设备状态类型。

**系统能力** SystemCapability.Msdp.DeviceStatus.Stationary

| 名称 | 描述 |
| -------- | -------- |
| still | 绝对静止。 |
| relativeStill | 相对静止。 |

## ActivityEvent

设备状态事件。

**系统能力** SystemCapability.Msdp.DeviceStatus.Stationary

| 变量                             | 值    | 说明                                       |
| ------------------------------ | ---- | ---------------------------------------- |
| ENTER         | 1    | 进入。   |
| EXIT | 2   | 退出。 |
| ENTER_EXIT | 3   | 进入和退出。 |

## ActivityState

设备状态返回值。

**系统能力** SystemCapability.Msdp.DeviceStatus.Stationary

| 变量                             | 值    | 说明                                       |
| ------------------------------ | ---- | ---------------------------------------- |
| ENTER         | 1    | 进入。   |
| EXIT | 2   | 退出。 |

## deviceStatus.on('still' | 'relativeStill')

on(activity: ActivityType, event: ActivityEvent, reportLatencyNs: number, callback: Callback&lt;ActivityResponse&gt;): void

设备状态管理，订阅设备状态服务。

**系统能力** SystemCapability.Msdp.DeviceStatus.Stationary

**参数：**

| 名称                  | 类型                                               | 必填 | 说明                          |
| -------------------- | -------------------------------------------------- | ---- | ---------------------------- |
| activity  | [ActivityType](#activitytype)  | 是   | 设备状态能力类型。              |
| event  | [ActivityEvent](#activityevent)  | 是   | 事件类型。              |
| reportLatencyNs  | number  | 是   | 报告延时。              |
| callback             | Callback<[ActivityResponse](#activityresponse)\>  | 是   | 回调函数，接收上报状态变化事件。    |

**示例：**

```js
var reportLatencyNs = 100;
deviceStatus.on('still', deviceStatus.ActivityEvent.ENTER, reportLatencyNs, (data) => {
    console.log('data='+ JSON.stringify(data));
})
```

## deviceStatus.once('still' | 'relativeStill')

once(activity: ActivityType, callback: Callback&lt;ActivityResponse&gt;): void

设备状态管理，查询设备状态。

**系统能力** SystemCapability.Msdp.DeviceStatus.Stationary

**参数：**

| 名称                  | 类型                                               | 必填 | 说明                          |
| -------------------- | -------------------------------------------------- | ---- | ---------------------------- |
| activity  | [ActivityType](#activitytype)  | 是   | 设备状态能力类型。              |
| callback             | Callback<[ActivityResponse](#activityresponse)\>  | 是   | 回调函数，接收上报状态变化事件。    |

**示例：**

```js
deviceStatus.once('still', (data) => {
    console.log("data="+ JSON.stringify(data));
})
```

## deviceStatus.off('still' | 'relativeStill')

off(activity: ActivityType, event: ActivityEvent, callback?: Callback&lt;ActivityResponse&gt;): void

设备状态管理，取消订阅设备状态服务。

**系统能力** SystemCapability.Msdp.DeviceStatus.Stationary

**参数：**

| 名称                  | 类型                                               | 必填 | 说明                          |
| -------------------- | -------------------------------------------------- | ---- | ---------------------------- |
| activity  | [ActivityType](#activitytype)  | 是   | 设备状态能力类型。              |
| event  | [ActivityEvent](#activityevent)  | 是   | 事件类型。              |
| callback             | Callback<[ActivityResponse](#activityresponse)\>  | 否   | 回调函数，接收上报状态变化事件。    |

**示例：**

```js
deviceStatus.off('still', deviceStatus.ActivityEvent.ENTER);
```