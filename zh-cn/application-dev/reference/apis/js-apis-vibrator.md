# 振动

## 模块说明

vibrator模块提供控制马达振动的能力，如通过接口控制马达启动马达振动，停止马达振动等。

小器件是指用于向外传递信号的设备，包括马达和LED灯，本组件对开发者提供控制马达振动和LED灯开关的能力。

> **说明：**
>
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```js
import vibrator from '@ohos.vibrator';
```

## vibrator.vibrate

vibrate(duration: number): Promise&lt;void&gt;

按照指定持续时间触发马达振动。

**权限列表**：ohos.permission.VIBRATE，该权限为系统权限

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 

| 参数名      | 类型     | 必填   | 说明           |
| -------- | ------ | ---- | ------------ |
| duration | number | 是    | 指示马达振动的持续时间。 |

**返回值：** 

| 类型                  | 说明          |
| ------------------- | ----------- |
| Promise&lt;void&gt; | 指示触发振动是否成功。 |

**示例：** 

  ```js
  vibrator.vibrate(1000).then(()=>{
      console.log("Promise returned to indicate a successful vibration.");
  }, (error)=>{
      console.log("error.code"+error.code+"error.message"+error.message);
  });
  ```

## vibrator.vibrate

vibrate(effect: VibrateEffect, attribute: VibrateAttribute): Promise&lt;void&gt;

按照指定振动效果和振动属性触发马达振动。

**权限列表**：ohos.permission.VIBRATE，该权限为系统权限

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 

| 参数名    | 类型             | 必填 | 说明           |
| --------- | ---------------- | ---- | :------------- |
| effect    | VibrateEffect    | 是   | 马达振动效果。 |
| attribute | VibrateAttribute | 是   | 马达振动属性。 |

**返回值：** 

| 类型                | 说明          |
| ------------------- | ------------- |
| Promise&lt;void&gt; | Promise实例。 |

**示例：** 

```js
vibrator.vibrate({
	'type': 'time',
    'duration': 1000
}, {
   	'id': 1,
	'usage': 'alarm'
}).then((result)=>{
   	console.log("Promise returned to indicate a successful vibration");
}).catch((error)=>{
  	console.log("error.code"+error.code+"error.message"+error.message);
})
```

## vibrator.vibrate

vibrate(duration: number, callback?: AsyncCallback&lt;void&gt;): void

按照指定持续时间触发马达振动。

**权限列表**：ohos.permission.VIBRATE，该权限为系统权限

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 
| 参数名      | 类型                        | 必填   | 说明                      |
| -------- | ------------------------- | ---- | ----------------------- |
| duration | number                    | 是    | 指示马达振动的持续时间。            |
| callback | AsyncCallback&lt;void&gt; | 否    | 马达执行振动的回调函数，指示触发振动是否成功。 |

**示例：** 
  ```js
  vibrator.vibrate(1000,function(error){
      if(error){
          console.log("error.code"+error.code+"error.message"+error.message);
      }else{
          console.log("Callback returned to indicate a successful vibration.");
      }
  })
  ```


## vibrator.vibrate

vibrate(effectId: EffectId): Promise&lt;void&gt;

按照指定振动效果触发马达振动。

**权限列表**：ohos.permission.VIBRATE，该权限为系统权限

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 
| 参数名      | 类型                    | 必填   | 说明            |
| -------- | --------------------- | ---- | ------------- |
| effectId | [EffectId](#effectid) | 是    | 指示马达振动效果的字符串。 |

**返回值：** 
| 类型                  | 说明          |
| ------------------- | ----------- |
| Promise&lt;void&gt; | 指示触发振动是否成功。 |

**示例：** 
  ```js
  vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER).then(()=>{
      console.log("Promise returned to indicate a successful vibration.");
  }, (error)=>{
      console.log("error.code"+error.code+"error.message"+error.message);
  });
  ```


## vibrator.vibrate

vibrate(effectId: EffectId, callback?: AsyncCallback&lt;void&gt;): void

按照指定振动效果触发马达振动。

**权限列表**：ohos.permission.VIBRATE，该权限为系统权限

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 
| 参数名      | 类型                        | 必填   | 说明                      |
| -------- | ------------------------- | ---- | ----------------------- |
| effectId | [EffectId](#effectid)     | 是    | 指示马达振动效果的字符串。           |
| callback | AsyncCallback&lt;void&gt; | 否    | 马达执行振动的回调函数，指示触发振动是否成功。 |

**示例：** 

  ```js
  vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER, function(error){
      if(error){
          console.log("error.code"+error.code+"error.message"+error.message);
      }else{
          console.log("Callback returned to indicate a successful vibration.");
      }
  })
  ```

## vibrator.vibrate

vibrate(effect: VibrateEffect, attribute: VibrateAttribute, callback: AsyncCallback&lt;void&gt;): void

按照指定振动效果和振动属性触发马达振动。

**权限列表**：ohos.permission.VIBRATE，该权限为系统权限

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 

| 参数名    | 类型                      | 必填 | 说明                     |
| --------- | ------------------------- | ---- | :----------------------- |
| effect    | VibrateEffect             | 是   | 马达振动效果。           |
| attribute | VibrateAttribute          | 是   | 马达振动属性。           |
| callback  | AsyncCallback&lt;void&gt; | 是   | 指定的callback回调方法。 |

示例：

```js
vibrator.vibrate({
	'type':'time',
    'duration':1000,
},{
    'id':1,
    'usage': 'alarm'
}, (error)=>{
  	if(error){
    	console.log(TAG + " fail, error.code:"+error.code+",error.message:"+error.message);
    }else{
       	console.log("Callback returned to indicate a successful vibration.");
   	}
});
```

## vibrator.stop

stop(stopMode: VibratorStopMode): Promise&lt;void&gt;

按照要停止指定的振动模式来停止马达的振动。如果要停止的振动模式与触发马达振动时的模式不相同，则调用本接口会失败。

**权限列表**：ohos.permission.VIBRATE，该权限为系统权限

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 
| 参数名      | 类型                                    | 必填   | 说明              |
| -------- | ------------------------------------- | ---- | --------------- |
| stopMode | [VibratorStopMode](#vibratorstopmode) | 是    | 指示马达要停止指定的振动模式。 |

**返回值：** 
| 类型                  | 说明          |
| ------------------- | ----------- |
| Promise&lt;void&gt; | 指示停止振动是否成功。 |

**示例：** 
  ```js
  vibrator.stop(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET).then(()=>{
      console.log("Promise returned to indicate a successful vibration.");
  }, (error)=>{
      console.log("error.code"+error.code+"error.message"+error.message);
  });
  ```


## vibrator.stop

stop(stopMode: VibratorStopMode, callback?: AsyncCallback&lt;void&gt;): void;

按照要停止指定的振动模式来停止马达的振动。如果要停止的振动模式与触发马达振动时的模式不相同，则调用本接口会失败。

**权限列表**：ohos.permission.VIBRATE，该权限为系统权限

**系统能力**：SystemCapability.Sensors.MiscDevice

**参数：** 
| 参数名      | 类型                                    | 必填   | 说明                      |
| -------- | ------------------------------------- | ---- | ----------------------- |
| stopMode | [VibratorStopMode](#vibratorstopmode) | 是    | 指示马达要停止指定的振动模式。         |
| callback | AsyncCallback&lt;void&gt;             | 否    | 马达停止振动的回调函数，指示停止振动是否成功。 |

**示例：** 
  ```js
  vibrator.stop(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET, function(error){
      if(error){
          console.log("error.code"+error.code+"error.message"+error.message);
      }else{
          console.log("Callback returned to indicate successful.");
      }
  })
  ```


## EffectId

表示马达振动效果的字符串。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Sensors.MiscDevice

| 名称                 | 默认值                  | 说明              |
| ------------------ | -------------------- | --------------- |
| EFFECT_CLOCK_TIMER | "haptic.clock.timer" | 调整定时器时振动器的振动效果。 |


## VibratorStopMode

表示马达要停止指定的振动模式。

**系统能力**：以下各项对应的系统能力均为SystemCapability.Sensors.MiscDevice

| 名称                        | 默认值      | 说明                                       |
| ------------------------- | -------- | ---------------------------------------- |
| VIBRATOR_STOP_MODE_TIME   | "time"   | 停止模式为duration模式的振动。即触发振动时参数类型为number，参数本身为指示振动持续时间的触发方式。 |
| VIBRATOR_STOP_MODE_PRESET | "preset" | 停止模式为预置EffectId的振动。即触发振动时参数类型为EffectId，参数本身为指示马达振动效果的字符串的触发方式。 |

## VibrateTime

表示马达振动时间

| 名称     | 默认值 | 说明                     |
| -------- | ------ | ------------------------ |
| type     | "time" | 指定振动效果类型。       |
| duration | 100    | 指定振动效果的持续时间。 |

## VibratePreset

表示马达预置振动类型

| 名称     | 默认值               | 说明                           |
| -------- | -------------------- | ------------------------------ |
| type     | "preset"             | 预置振动类型。                 |
| effectId | "haptic.clock.timer" | 调整定时器时振动器的振动效果。 |
| count    | 1                    | 循环振动的次数。               |

## VibrateAttribute

表示马达振动属性

| 名称  | 默认值    | 说明                                                         |
| ----- | --------- | ------------------------------------------------------------ |
| id    | 123       | 振动器id。                                                   |
| usage | "unknown" | 振动的使用。取值范围["unknown" , "alarm" ,  "ring" ,  "notification" ,  "communication" ]。 |

