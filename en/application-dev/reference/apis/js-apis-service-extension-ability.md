# ServiceExtensionAbility

The **ServiceExtensionAbility** module provides APIs for Service Extension abilities.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version. 
> The APIs of this module can be used only in the stage model.

## Modules to Import

```
import ServiceExtension from '@ohos.application.ServiceExtensionAbility';
```

## Required Permissions

None.

## Attributes

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

| Name| Type| Readable| Writable| Description| 
| -------- | -------- | -------- | -------- | -------- |
| context | [ServiceExtensionContext](js-apis-service-extension-context.md)  | Yes| No| Service Extension context, which is inherited from **ExtensionContext**.| 


## ServiceExtensionAbility.onCreate

onCreate(want: Want): void;

Called when a Service Extension ability is created to initialize the service logic.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | want |  [Want](js-apis-application-Want.md) | Yes| Information related to this Service Extension ability, including the ability name and bundle name.| 

**Example**

  ```js
  class ServiceExt extends ServiceExtension {
    onCreate(want) {
      console.log('onCreate, want:' + want.abilityName);
    }
  }
  ```


## ServiceExtensionAbility.onDestroy

onDestroy(): void;

Called when this Service Extension ability is destroyed to clear resources.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Example**

  ```js
  class ServiceExt extends ServiceExtension {
    onDestroy() {
      console.log('onDestroy');
    }
  }
  ```


## ServiceExtensionAbility.onRequest

onRequest(want: Want, startId: number): void;

Called after **onCreate** is invoked when a Service Extension ability is started by calling **startAbility**. The value of **startId** is incremented for each ability that is started.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | want |  [Want](js-apis-application-Want.md) | Yes| Information related to this Service Extension ability, including the ability name and bundle name.| 
  | startId | number | Yes| Number of ability start times. The initial value is **1**, and the value is automatically incremented for each ability started.| 

**Example**

  ```js
  class ServiceExt extends ServiceExtension {
    onRequest(want, startId) {
      console.log('onRequest, want:' + want.abilityName);
    }
  }
  ```


## ServiceExtensionAbility.onConnect

onConnect(want: Want): rpc.RemoteObject;

Called after **onCreate** is invoked when a Service Extension ability is started by calling **connectAbility**. A **RemoteObject** object is returned for communication with the client.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | want |  [Want](js-apis-application-Want.md)| Yes| Information related to this Service Extension ability, including the ability name and bundle name.| 

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | rpc.RemoteObject | A **RemoteObject** object used for communication with the client.| 

**Example**

  ```js
  import rpc from '@ohos.rpc'
  class StubTest extends rpc.RemoteObject{
      constructor(des) {
          super(des);
      }
      onConnect(code, data, reply, option) {
      }
  }
  class ServiceExt extends ServiceExtension {
    onConnect(want) {
      console.log('onConnect , want:' + want.abilityName);
      return new StubTest("test");
    }
  }
  ```


## ServiceExtensionAbility.onDisconnect

onDisconnect(want: Want): void;

Called when this Service Extension ability is disconnected.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | want |[Want](js-apis-application-Want.md)| Yes| Information related to this Service Extension ability, including the ability name and bundle name.| 

**Example**

  ```js
  class ServiceExt extends ServiceExtension {
    onDisconnect(want) {
      console.log('onDisconnect, want:' + want.abilityName);
    }
  }
  ```

## ServiceExtensionAbility.onReconnect

onReconnect(want: Want): void;

Called when this Service Extension ability is reconnected.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | want |[Want](js-apis-application-Want.md)| Yes| Information related to this Service Extension ability, including the ability name and bundle name.| 

**Example**

  ```js
  class ServiceExt extends ServiceExtension {
    onReconnect(want) {
      console.log('onReconnect, want:' + want.abilityName);
    }
  }
  ```

## ServiceExtensionAbility.onConfigurationUpdated

onConfigurationUpdated(config: Configuration): void;

 Called when the configuration of this Service Extension ability is updated.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | config | [Configuration](js-apis-configuration.md) | Yes| New configuration.| 

**Example**
    
  ```js
  class ServiceExt extends ServiceExtension {
      onConfigurationUpdated(config) {
          console.log('onConfigurationUpdated, config:' + JSON.stringify(config));
      }
  }
  ```

## ServiceExtensionAbility.dump

dump(params: Array\<string>): Array\<string>;

Dumps the client information.

**System capability**: SystemCapability.Ability.AbilityRuntime.AbilityCore

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | params | Array\<string> | Yes| Parameters in the form of a command.| 

**Example**
    
  ```js
  class ServiceExt extends ServiceExtension {
      dump(params) {
          console.log('dump, params:' + JSON.stringify(params));
          return ["params"]
      }
  }
  ```
