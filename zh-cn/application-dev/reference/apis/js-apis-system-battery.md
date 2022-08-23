# 电量信息

>  **说明：**
> - 从API Version 9开始，该接口不再维护，推荐使用新接口[`@ohos.batteryInfo`](js-apis-battery-info.md)。
> 
> - 本模块首批接口从API version 3开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块


```js
import battery from '@system.battery';
```


## battery.getStatus

getStatus(Object): void

获取设备当前的充电状态及剩余电量。

**系统能力：** SystemCapability.PowerManager.BatteryManager.Core

**参数：**

| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| success | (data: BatteryResponse) => void | 否 | 接口调用成功的回调函数。|
| fail | (data: string, code: number) => void | 否 | 接口调用失败的回调函数。|
| complete | () => void | 否 | 接口调用结束的回调函数。 |

success返回值：

| 参数名 | 类型 | 说明 |
| -------- | -------- | -------- |
| charging | boolean | 当前电池是否在充电中。 |
| level | number | 当前电池的电量，取值范围：0.00&nbsp;-&nbsp;1.00&nbsp;。 |

**示例：**

```js
export default {    
  getStatus() {       
    battery.getStatus({           
      success: function(data) {               
        console.log('success get battery level:' + data.level);           
      },            
      fail: function(data, code) {                
        console.log('fail to get battery level code:' + code + ', data: ' + data);            
      },        
    });    
  },
}
```