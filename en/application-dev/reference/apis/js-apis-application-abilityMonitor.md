# AbilityMonitor

The **AbilityMonitor** module provides monitors for abilities that meet specified conditions. The latest matched abilities are stored in an **AbilityMonitor** object.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version. 

## Usage

The ability monitor is set by calling **addAbilityMonitor** in **abilityDelegator**.

```js
import AbilityDelegatorRegistry from '@ohos.application.abilityDelegatorRegistry'
var abilityDelegator;

function onAbilityCreateCallback(data) {
    console.info("onAbilityCreateCallback");
}

var monitor = {
    abilityName: "abilityname",
    onAbilityCreate: onAbilityCreateCallback
}

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
abilityDelegator.addAbilityMonitor(monitor, (err : any) => {
    console.info("addAbilityMonitor callback");
});
```

## AbilityMonitor

Describes an ability monitor.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name                                                        | Type    | Readable| Writable| Description                                                        |
| ------------------------------------------------------------ | -------- | ---- | ---- | ------------------------------------------------------------ |
| abilityName                                                  | string   | Yes  | Yes  | Name of the ability bound to the ability monitor. |
| onAbilityCreate?:(data: [Ability](js-apis-application-ability.md#Ability)) | function | Yes  | Yes  | Called when the ability is created.<br>If this attribute is not set, the corresponding lifecycle callback cannot be received. |
| onAbilityForeground?:(data: [Ability](js-apis-application-ability.md#Ability)) | function | Yes  | Yes  | Called when the ability starts to run in the foreground.<br>If this attribute is not set, the corresponding lifecycle callback cannot be received. |
| onAbilityBackground?:(data: [Ability](js-apis-application-ability.md#Ability)) | function | Yes  | Yes  | Called when the ability starts to run in the background.<br>If this attribute is not set, the corresponding lifecycle callback cannot be received. |
| onAbilityDestroy?:(data: [Ability](js-apis-application-ability.md#Ability)) | function | Yes  | Yes  | Called when the ability is destroyed.<br>If this attribute is not set, the corresponding lifecycle callback cannot be received. |
| onWindowStageCreate?:(data: [Ability](js-apis-application-ability.md#Ability)) | function | Yes  | Yes  | Called when the window stage is created.<br>If this attribute is not set, the corresponding lifecycle callback cannot be received. |
| onWindowStageRestore?:(data: [Ability](js-apis-application-ability.md#Ability)) | function | Yes  | Yes  | Called when the window stage is restored.<br>If this attribute is not set, the corresponding lifecycle callback cannot be received. |
| onWindowStageDestroy?:(data: [Ability](js-apis-application-ability.md#Ability)) | function | Yes  | Yes  | Called when the window stage is destroyed.<br>If this attribute is not set, the corresponding lifecycle callback cannot be received. |
