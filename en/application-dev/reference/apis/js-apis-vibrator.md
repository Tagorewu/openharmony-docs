# Vibrator

The **Vibrator** module provides APIs for triggering or stopping vibration.

> **NOTE**
>
> The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```js
import vibrator from '@ohos.vibrator';
```

## vibrator.startVibration<sup>9+</sup>

startVibration(effect: VibrateEffect, attribute: VibrateAttribute, callback: AsyncCallback&lt;void&gt;): void

Triggers vibration with the specified effect and attribute. This API uses a promise to return the result.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name   | Type                                  | Mandatory| Description                                                      |
| --------- | -------------------------------------- | ---- | :--------------------------------------------------------- |
| effect    | [VibrateEffect](#vibrateeffect9)       | Yes  | Vibration effect.                                            |
| attribute | [VibrateAttribute](#vibrateattribute9) | Yes  | Vibration attribute.                                            |
| callback  | AsyncCallback&lt;void&gt;              | Yes  | Callback used to the result. If the vibration starts, **err** is **undefined**. Otherwise, **err** is an error object.|

**Example**

```js
try {
    vibrator.startVibration({
    type:'time',
    duration:1000,
    },{
        id:0,
        usage: 'alarm'
    }, (error)=>{
        if(error){
            console.log('vibrate fail, error.code: ' + error.code + 'error.message: ', + error.message);
        }else{
            console.log('Callback returned to indicate a successful vibration.');
        }
    });
} catch(err) {
      console.info('errCode: ' + err.code + ' ,msg: ' + err.message);
}
```

## vibrator.startVibration<sup>9+</sup>

startVibration(effect: VibrateEffect, attribute: VibrateAttribute): Promise&lt;void&gt;

Triggers vibration with the specified effect and attribute. This API uses a promise to return the result.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name   | Type                                  | Mandatory| Description          |
| --------- | -------------------------------------- | ---- | -------------- |
| effect    | [VibrateEffect](#vibrateeffect9)       | Yes  | Vibration effect.|
| attribute | [VibrateAttribute](#vibrateattribute9) | Yes  | Vibration attribute.|

**Return value**

| Type               | Description                                  |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

  ```js
try {
    vibrator.startVibration({
    type: 'time',
    duration: 1000
    }, {
        id: 0,
        usage: 'alarm'
    }).then(()=>{
        console.log('Promise returned to indicate a successful vibration');
    }).catch((error)=>{
        console.log('error.code' + error.code + 'error.message' + error.message);
    })
} catch(err) {
      console.info('errCode: ' + err.code + ' ,msg: ' + err.message);
}
  ```

## vibrator.stopVibration<sup>9+</sup>

stopVibration(stopMode: VibratorStopMode, callback: AsyncCallback&lt;void&gt;): void

Stops the vibration with the specified **stopMode**. This API uses a promise to return the result. If the specified **stopMode** is different from the mode used to trigger the vibration, this API fails to be called.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                                 | Mandatory| Description                                                        |
| -------- | ------------------------------------- | ---- | ------------------------------------------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | Yes  | Mode to stop the vibration.                                    |
| callback | AsyncCallback&lt;void&gt;             | Yes  | Callback used to the result. If the vibration stops, **err** is **undefined**. Otherwise, **err** is an error object.|

**Example**

  ```js
try {
    vibrator.stopVibration(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET, function(error){
        if(error){
            console.log('error.code' + error.code + 'error.message' + error.message);
        }else{
            console.log('Callback returned to indicate successful.');
        }
    })
} catch(err) {
      console.info('errCode: ' + err.code + ' ,msg: ' + err.message);
}
  ```

## vibrator.stopVibration<sup>9+</sup>

stopVibration(stopMode: VibratorStopMode): Promise&lt;void&gt;

Stops the vibration with the specified **stopMode**. This API uses a promise to return the result. If the specified **stopMode** is different from the mode used to trigger the vibration, this API fails to be called.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                                 | Mandatory| Description                    |
| -------- | ------------------------------------- | ---- | ------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | Yes  | Mode to stop the vibration.|

**Return value**

| Type               | Description                                  |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

  ```js
try {
    vibrator.stopVibration(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET).then(()=>{
    console.log('Promise returned to indicate a successful vibration.');
    }, (error)=>{
        console.log('error.code' + error.code + 'error.message' + error.message);
    });
} catch(err) {
      console.info('errCode: ' + err.code + ' ,msg: ' + err.message);
}
  ```

## EffectId

Describes the vibration effect ID.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name              | Default Value              | Description              |
| ------------------ | -------------------- | ------------------ |
| EFFECT_CLOCK_TIMER | "haptic.clock.timer" | Preset vibration effect ID.|


## VibratorStopMode

Enumerates the modes available to stop the vibration.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name                     | Default Value  | Description                                                        |
| ------------------------- | -------- | ------------------------------------------------------------ |
| VIBRATOR_STOP_MODE_TIME   | "time"   | The vibration to stop is in **duration** mode. This vibration is triggered with the parameter **duration** of the **number** type.|
| VIBRATOR_STOP_MODE_PRESET | "preset" | The vibration to stop is in **EffectId** mode. This vibration is triggered with the parameter **effectId** of the **EffectId** type.|

## VibrateEffect<sup>9+</sup>

Describes the vibration effect.

**System capability**: SystemCapability.Sensors.MiscDevice

| Type                            | Description                          |
| -------------------------------- | ------------------------------ |
| [VibrateTime](#vibratetime9)     | Triggers vibration with the specified duration. This API uses a promise to return the result.|
| [VibratePreset](#vibratepreset9) | Vibration with a preset effect.|

## VibrateTime<sup>9+</sup>

Describes the vibration with the specified duration.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name    | Default Value| Description                          |
| -------- | ------ | ------------------------------ |
| type     | "time" | Vibration with the specified duration.|
| duration | -      | Vibration duration, in ms.        |

## VibratePreset<sup>9+</sup>

Describes the vibration with a preset effect.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name    | Default Value  | Description                          |
| -------- | -------- | ------------------------------ |
| type     | "preset" | Vibration with the specified effect.|
| effectId | -        | Preset vibration effect ID.            |
| count    | -        | Number of vibrations to repeat.              |

## VibrateAttribute<sup>9+</sup>

Describes the vibration attribute.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name | Default Value| Description          |
| ----- | ------ | -------------- |
| id    | 0      | Vibrator ID.    |
| usage | -      | Vibration scenario.|

## Usage<sup>9+</sup>

Enumerates the vibration scenarios.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name            | Type  | Description                          |
| ---------------- | ------ | ------------------------------ |
| unknown          | string | Unknown scenario, with the lowest priority.|
| alarm            | string | Vibration for alarms.          |
| ring             | string | Vibration for incoming calls.          |
| notification     | string | Vibration for notifications.          |
| communication    | string | Vibration for communication.          |
| touch            | string | Touch vibration scenario.          |
| media            | string | Multimedia vibration scenario.        |
| physicalFeedback | string | Physical feedback vibration scenario.      |
| simulateReality  | string | Simulated reality vibration scenario.      |

## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(duration: number): Promise&lt;void&gt;

Triggers vibration with the specified duration. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.startVibration](#vibratorstartvibration9-1) instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type  | Mandatory| Description                  |
| -------- | ------ | ---- | ---------------------- |
| duration | number | Yes  | Vibration duration, in ms.|

**Return value**

| Type               | Description                                  |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

  ```js
vibrator.vibrate(1000).then(()=>{
    console.log('Promise returned to indicate a successful vibration.');
}, (error)=>{
    console.log('error.code' + error.code + 'error.message' + error.message);
});
  ```

## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(duration: number, callback?: AsyncCallback&lt;void&gt;): void

Triggers vibration with the specified duration. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.startVibration](#vibratorstartvibration9) instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                     | Mandatory| Description                                                      |
| -------- | ------------------------- | ---- | ---------------------------------------------------------- |
| duration | number                    | Yes  | Vibration duration, in ms.                                    |
| callback | AsyncCallback&lt;void&gt; | No  | Callback used to the result. If the vibration starts, **err** is **undefined**. Otherwise, **err** is an error object.|

**Example**

  ```js
vibrator.vibrate(1000,function(error){
    if(error){
        console.log('error.code' + error.code + 'error.message' + error.message);
    }else{
        console.log('Callback returned to indicate a successful vibration.');
    }
})
  ```


## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(effectId: EffectId): Promise&lt;void&gt;

Triggers vibration with the specified effect. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.startVibration](#vibratorstartvibration9-1) instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                 | Mandatory| Description              |
| -------- | --------------------- | ---- | ------------------ |
| effectId | [EffectId](#effectid) | Yes  | Preset vibration effect ID.|

**Return value**

| Type               | Description                                  |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

  ```js
vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER).then(()=>{
    console.log('Promise returned to indicate a successful vibration.');
}, (error)=>{
    console.log('error.code' + error.code + 'error.message' + error.message);
});
  ```


## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(effectId: EffectId, callback?: AsyncCallback&lt;void&gt;): void

Triggers vibration with the specified effect. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.startVibration](#vibratorstartvibration9) instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                     | Mandatory| Description                                                      |
| -------- | ------------------------- | ---- | ---------------------------------------------------------- |
| effectId | [EffectId](#effectid)     | Yes  | Preset vibration effect ID.                                        |
| callback | AsyncCallback&lt;void&gt; | No  | Callback used to the result. If the vibration starts, **err** is **undefined**. Otherwise, **err** is an error object.|

**Example**

  ```js
vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER, function(error){
    if(error){
        console.log('error.code' + error.code + 'error.message' + error.message);
    }else{
        console.log('Callback returned to indicate a successful vibration.');
    }
})
  ```

## vibrator.stop<sup>(deprecated)</sup>

stop(stopMode: VibratorStopMode): Promise&lt;void&gt;

Stops the vibration with the specified **stopMode**. This API uses a promise to return the result. If the specified **stopMode** is different from the mode used to trigger the vibration, this API fails to be called.

This API is deprecated since API version 9. You are advised to use [vibrator.stopVibration](#vibratorstopvibration9-1) instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                                 | Mandatory| Description                    |
| -------- | ------------------------------------- | ---- | ------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | Yes  | Mode to stop the vibration.|

**Return value**

| Type               | Description                                  |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

  ```js
vibrator.stop(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET).then(()=>{
    console.log('Promise returned to indicate a successful vibration.');
}, (error)=>{
    console.log('error.code' + error.code + 'error.message' + error.message);
});
  ```


## vibrator.stop<sup>(deprecated)</sup>

stop(stopMode: VibratorStopMode, callback?: AsyncCallback&lt;void&gt;): void

Stops the vibration with the specified **stopMode**. This API uses a promise to return the result. If the specified **stopMode** is different from the mode used to trigger the vibration, this API fails to be called.

This API is deprecated since API version 9. You are advised to use [vibrator.stopVibration](#vibratorstopvibration9) instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                                 | Mandatory| Description                                                        |
| -------- | ------------------------------------- | ---- | ------------------------------------------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | Yes  | Mode to stop the vibration.                                    |
| callback | AsyncCallback&lt;void&gt;             | No  | Callback used to the result. If the vibration stops, **err** is **undefined**. Otherwise, **err** is an error object.|

**Example**

  ```js
vibrator.stop(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET, function(error){
    if(error){
        console.log('error.code' + error.code + 'error.message' + error.message);
    }else{
        console.log('Callback returned to indicate successful.');
    }
})
  ```
