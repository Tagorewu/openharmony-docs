# appManager

The **appManager** module implements application management. You can use the APIs of this module to query whether the application is undergoing a stability test, whether the application is running on a RAM constrained device, the memory size of the application, and information about the running process.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```js
import app from '@ohos.application.appManager';
```

## appManager.isRunningInStabilityTest<sup>8+</sup>

static isRunningInStabilityTest(callback: AsyncCallback&lt;boolean&gt;): void

Checks whether this application is undergoing a stability test. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | No| Callback used to return the result. If the application is undergoing a stability test, **true** will be returned; otherwise, **false** will be returned.| 

**Example**
    
  ```js
  import app from '@ohos.application.appManager';
  app.isRunningInStabilityTest((err, flag) => {
      console.log('startAbility result:' + JSON.stringify(err));
  })  
  ```


## appManager.isRunningInStabilityTest<sup>8+</sup>

static isRunningInStabilityTest(): Promise&lt;boolean&gt;

Checks whether this application is undergoing a stability test. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;boolean&gt; | Promise used to return the result. If the application is undergoing a stability test, **true** will be returned; otherwise, **false** will be returned.| 

**Example**
    
  ```js
  import app from '@ohos.application.appManager';
  app.isRunningInStabilityTest().then((flag) => {
      console.log('success:' + JSON.stringify(flag));
  }).catch((error) => {
      console.log('failed:' + JSON.stringify(error));
  });
  ```


## appManager.isRamConstrainedDevice

isRamConstrainedDevice(): Promise\<boolean>;

Checks whether this application is running on a RAM constrained device. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;boolean&gt; | Promise used to return whether the application is running on a RAM constrained device. If the application is running on a RAM constrained device, **true** will be returned; otherwise, **false** will be returned.| 

**Example**
    
  ```js
        app.isRamConstrainedDevice().then((data) => {
            console.log('success:' + JSON.stringify(data));
        }).catch((error) => {
            console.log('failed:' + JSON.stringify(error));
        });
  ```

## appManager.isRamConstrainedDevice

isRamConstrainedDevice(callback: AsyncCallback\<boolean>): void;

Checks whether this application is running on a RAM constrained device. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;boolean&gt; | No| Callback used to return whether the application is running on a RAM constrained device. If the application is running on a RAM constrained device, **true** will be returned; otherwise, **false** will be returned.| 

**Example**
    
  ```js
        app.isRamConstrainedDevice((err, data) => {
            console.log('startAbility result failed:' + JSON.stringify(err));
            console.log('startAbility result success:' + JSON.stringify(data));
        })
  ```

## appManager.getAppMemorySize

getAppMemorySize(): Promise\<number>;

Obtains the memory size of this application. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Return value**

  | Type| Description| 
  | -------- | -------- |
  | Promise&lt;number&gt; | Size of the application memory.| 

**Example**
    
  ```js
        app.getAppMemorySize().then((data) => {
            console.log('success:' + JSON.stringify(data));
        }).catch((error) => {
            console.log('failed:' + JSON.stringify(error));
        });
  ```

## appManager.getAppMemorySize

getAppMemorySize(callback: AsyncCallback\<number>): void;

Obtains the memory size of this application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;number&gt; | No| Size of the application memory.| 

**Example**
    
  ```js
        app.getAppMemorySize((err, data) => {
            console.log('startAbility result failed :' + JSON.stringify(err));
            console.log('startAbility result success:' + JSON.stringify(data));
        })
  ```
## appManager.getProcessRunningInfos<sup>(deprecated)</sup>

getProcessRunningInfos(): Promise\<Array\<ProcessRunningInfo>>;

Obtains information about the running processes. This API uses a promise to return the result.

> This API is deprecated since API version 9. You are advised to use [appManager.getProcessRunningInformation<sup>9+</sup>](#appmanagergetprocessrunninginformation9) instead.

**Required permissions**: ohos.permission.GET_RUNNING_INFO

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<Array\<ProcessRunningInfo>> | Promise used to return the process information.|

**Example**
    
  ```js
        app.getProcessRunningInfos().then((data) => {
            console.log('success:' + JSON.stringify(data));
        }).catch((error) => {
            console.log('failed:' + JSON.stringify(error));
        });
  ```

## appManager.getProcessRunningInfos<sup>(deprecated)</sup>

getProcessRunningInfos(callback: AsyncCallback\<Array\<ProcessRunningInfo>>): void;

Obtains information about the running processes. This API uses an asynchronous callback to return the result.

> This API is deprecated since API version 9. You are advised to use [appManager.getProcessRunningInformation<sup>9+</sup>](#appmanagergetprocessrunninginformation9-1) instead.

**Required permissions**: ohos.permission.GET_RUNNING_INFO

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback\<Array\<ProcessRunningInfo>> | No| Callback used to return the process information.|

**Example**
    
  ```js
        app.getProcessRunningInfos((err, data) => {
            console.log('startAbility result failed :' + JSON.stringify(err));
            console.log('startAbility result success:' + JSON.stringify(data));
        })
  ```

## appManager.getProcessRunningInformation<sup>9+</sup>

getProcessRunningInformation(): Promise\<Array\<ProcessRunningInformation>>;

Obtains information about the running processes. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_RUNNING_INFO

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<Array\<[ProcessRunningInformation](#processrunninginformation)>> | Promise used to return the process information.|

**Example**
    
  ```js
        app.getProcessRunningInformation().then((data) => {
            console.log('success:' + JSON.stringify(data));
        }).catch((error) => {
            console.log('failed:' + JSON.stringify(error));
        });
  ```

## appManager.getProcessRunningInformation<sup>9+</sup>

getProcessRunningInformation(callback: AsyncCallback\<Array\<ProcessRunningInformation>>): void;

Obtains information about the running processes. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_RUNNING_INFO

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback\<Array\<[ProcessRunningInformation](#processrunninginformation)>> | No| Callback used to return the process information.|

**Example**
    
  ```js
        app.getProcessRunningInformation((err, data) => {
            console.log('startAbility result failed :' + JSON.stringify(err));
            console.log('startAbility result success:' + JSON.stringify(data));
        })
  ```

## appManager.registerApplicationStateObserver<sup>8+</sup>

registerApplicationStateObserver(observer: ApplicationStateObserver): number;

Registers an observer to listen for the state changes of all applications.

**Required permissions**: ohos.permission.RUNNING_STATE_OBSERVER

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| observer | [ApplicationStateObserver](#applicationstateobserver) | No| Numeric code of the observer.|

**Example**
    
  ```js
  var applicationStateObserver = {
    onForegroundApplicationChanged(appStateData) {
        console.log('------------ onForegroundApplicationChanged -----------', appStateData);
    },
    onAbilityStateChanged(abilityStateData) {
        console.log('------------ onAbilityStateChanged -----------', abilityStateData);
    },
    onProcessCreated(processData) {
        console.log('------------ onProcessCreated -----------', processData);
    },
    onProcessDied(processData) {
        console.log('------------ onProcessDied -----------', processData);
    },
    onProcessStateChanged(processData) {
        console.log('------------ onProcessStateChanged -----------', processData);
    }
  }
  const observerCode = app.registerApplicationStateObserver(applicationStateObserver);
  console.log('-------- observerCode: ---------', observerCode);

  ```

## appManager.registerApplicationStateObserver<sup>9+</sup>

registerApplicationStateObserver(observer: ApplicationStateObserver, bundleNameList: Array\<string>): number;

Registers an observer to listen for the state changes of a specified application.

**Required permissions**: ohos.permission.RUNNING_STATE_OBSERVER

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| observer | [ApplicationStateObserver](#applicationstateobserver) | No| Numeric code of the observer.|
| bundleNameList | Array<string> | No| **bundleName** array of the application. A maximum of 128 bundle names can be passed.|

**Example**
    
  ```js
  var applicationStateObserver = {
    onForegroundApplicationChanged(appStateData) {
        console.log('------------ onForegroundApplicationChanged -----------', appStateData);
    },
    onAbilityStateChanged(abilityStateData) {
        console.log('------------ onAbilityStateChanged -----------', abilityStateData);
    },
    onProcessCreated(processData) {
        console.log('------------ onProcessCreated -----------', processData);
    },
    onProcessDied(processData) {
        console.log('------------ onProcessDied -----------', processData);
    },
    onProcessStateChanged(processData) {
        console.log('------------ onProcessStateChanged -----------', processData);
    }
  }
  var bundleNameList = ['bundleName1', 'bundleName2'];
  const observerCode = app.registerApplicationStateObserver(applicationStateObserver, bundleNameList);
  console.log('-------- observerCode: ---------', observerCode);

  ```
## appManager.unregisterApplicationStateObserver<sup>8+</sup>

unregisterApplicationStateObserver(observerId: number,  callback: AsyncCallback\<void>): void;

Deregisters the application state observer. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.RUNNING_STATE_OBSERVER

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**
 
| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| observerId | number | No| Numeric code of the observer.|
| callback | AsyncCallback\<void> | No| Callback used to return the result.|

**Example**
    
  ```js
    var observerId = 100;

    function unregisterApplicationStateObserverCallback(err) {
      if (err) {
          console.log('------------ unregisterApplicationStateObserverCallback ------------', err);
      }
    }
    app.unregisterApplicationStateObserver(observerId, unregisterApplicationStateObserverCallback);
  ```

## appManager.unregisterApplicationStateObserver<sup>8+</sup>

unregisterApplicationStateObserver(observerId: number): Promise\<void>;

Deregisters the application state observer. This API uses a promise to return the result.

**Required permissions**: ohos.permission.RUNNING_STATE_OBSERVER

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| observerId | number | No| Numeric code of the observer.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<void> | Promise used to return the result.|

**Example**
    
  ```js
    var observerId = 100;

    app.unregisterApplicationStateObserver(observerId)
   .then((data) => {
       console.log('----------- unregisterApplicationStateObserver success ----------', data);
   })
   .catch((err) => {
       console.log('----------- unregisterApplicationStateObserver fail ----------', err);
   })
  ```

## appManager.getForegroundApplications<sup>8+</sup>

getForegroundApplications(callback: AsyncCallback\<Array\<AppStateData>>): void;

Obtains applications that are running in the foreground. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_RUNNING_INFO

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback\<Array\<AppStateData>> | No| Callback used to return the application state data.|

**Example**
    
  ```js
    function getForegroundApplicationsCallback(err, data) {
      if (err) {
          console.log('--------- getForegroundApplicationsCallback fail ---------', err);
      } else {
          console.log('--------- getForegroundApplicationsCallback success ---------', data)
      }
    }
    app.getForegroundApplications(getForegroundApplicationsCallback);
  ```

## appManager.getForegroundApplications<sup>8+</sup>

getForegroundApplications(): Promise\<Array\<AppStateData>>;

Obtains applications that are running in the foreground. This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_RUNNING_INFO

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<Array\<ProcessRunningInfo>> | Promise used to return the application state data.|

**Example**
    
  ```js
    app.getForegroundApplications()
    .then((data) => {
        console.log('--------- getForegroundApplications success -------', data);
    })
    .catch((err) => {
        console.log('--------- getForegroundApplications fail -------', err);
    })
  ```

## appManager.killProcessWithAccount<sup>8+</sup>

killProcessWithAccount(bundleName: string, accountId: number): Promise\<void\>

Kills a process by bundle name and account ID. This API uses a promise to return the result.

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS and ohos.permission.CLEAN_BACKGROUND_PROCESSES

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | bundleName | string | Yes| Bundle name of an application.| 
  | accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).| 

**Example**

```js
var bundleName = 'bundleName';
var accountId = 0;
app.killProcessWithAccount(bundleName, accountId)
   .then((data) => {
       console.log('------------ killProcessWithAccount success ------------', data);
   })
   .catch((err) => {
       console.log('------------ killProcessWithAccount fail ------------', err);
   })
```


## appManager.killProcessWithAccount<sup>8+</sup>

killProcessWithAccount(bundleName: string, accountId: number, callback: AsyncCallback\<void\>): void

Kills a process by bundle name and account ID. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS and ohos.permission.CLEAN_BACKGROUND_PROCESSES

**Parameters**

  | Name| Type| Mandatory| Description| 
  | -------- | -------- | -------- | -------- |
  | bundleName | string | Yes| Bundle name of an application.| 
  | accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).| 
  | callback | AsyncCallback\<void\> | Yes| Callback used to return the result.| 

**Example**

```js
var bundleName = 'bundleName';
var accountId = 0;
function killProcessWithAccountCallback(err, data) {
   if (err) {
       console.log('------------- killProcessWithAccountCallback fail, err: --------------', err);
   } else {
       console.log('------------- killProcessWithAccountCallback success, data: --------------', data);
   }
}
app.killProcessWithAccount(bundleName, accountId, killProcessWithAccountCallback);
```

## appManager.killProcessesByBundleName<sup>8+</sup>

killProcessesByBundleName(bundleName: string, callback: AsyncCallback\<void>);

Kills a process by bundle name. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.CLEAN_BACKGROUND_PROCESSES

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| bundleName | string | No| Bundle name of an application.|
| callback | AsyncCallback\<void> | No| Callback used to return the result.|

**Example**
    
  ```js
    var bundleName = 'bundleName';
    function killProcessesByBundleNameCallback(err, data) {
      if (err) {
          console.log('------------- killProcessesByBundleNameCallback fail, err: --------------', err);
      } else {
          console.log('------------- killProcessesByBundleNameCallback success, data: --------------', data);
      }
    }
    app.killProcessesByBundleName(bundleName, killProcessesByBundleNameCallback);
  ```

## appManager.killProcessesByBundleName<sup>8+</sup>

killProcessesByBundleName(bundleName: string): Promise\<void>;

Kills a process by bundle name. This API uses a promise to return the result.

**Required permissions**: ohos.permission.CLEAN_BACKGROUND_PROCESSES

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| bundleName | string | No| Bundle name of an application.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<void> | Promise used to return the result.|

**Example**
    
  ```js
var bundleName = 'bundleName';
app.killProcessesByBundleName(bundleName)
   .then((data) => {
       console.log('------------ killProcessesByBundleName success ------------', data);
   })
   .catch((err) => {
       console.log('------------ killProcessesByBundleName fail ------------', err);
   })

  ```

## appManager.clearUpApplicationData<sup>8+</sup>

clearUpApplicationData(bundleName: string, callback: AsyncCallback\<void>);

Clears application data by bundle name. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.CLEAN_APPLICATION_DATA

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| bundleName | string | No| Bundle name of an application.|
| callback | AsyncCallback\<void> | No| Callback used to return the result.|

**Example**
    
  ```js
    var bundleName = 'bundleName';
    function clearUpApplicationDataCallback(err, data) {
      if (err) {
          console.log('------------- clearUpApplicationDataCallback fail, err: --------------', err);
      } else {
          console.log('------------- clearUpApplicationDataCallback success, data: --------------', data);
      }
    }
    app.clearUpApplicationData(bundleName, clearUpApplicationDataCallback);

  ```

## appManager.clearUpApplicationData<sup>8+</sup>

clearUpApplicationData(bundleName: string): Promise\<void>;

Clears application data by bundle name. This API uses a promise to return the result.

**Required permissions**: ohos.permission.CLEAN_APPLICATION_DATA

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| bundleName | string | No| Bundle name of an application.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<void> | Promise used to return the result.|

**Example**
    
  ```js
  var bundleName = 'bundleName';
  app.clearUpApplicationData(bundleName)
    .then((data) => {
        console.log('------------ clearUpApplicationData success ------------', data);
    })
    .catch((err) => {
        console.log('------------ clearUpApplicationData fail ------------', err);
    })

  ```

## ApplicationStateObserver.onForegroundApplicationChanged<sup>8+</sup>

onForegroundApplicationChanged(appStateData: AppStateData): void;

Called when the application state changes.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| appStateData | [AppStateData](#appstatedata) | No| Information about the application whose state is changed.|

**Example**
    
```js
  var applicationStateObserver = {
    onForegroundApplicationChanged(appStateData) {
        console.log('------------ onForegroundApplicationChanged -----------', appStateData);
    },
    onAbilityStateChanged(abilityStateData) {
        console.log('------------ onAbilityStateChanged -----------', abilityStateData);
    },
    onProcessCreated(processData) {
        console.log('------------ onProcessCreated -----------', processData);
    },
    onProcessDied(processData) {
        console.log('------------ onProcessDied -----------', processData);
    },
    onProcessStateChanged(processData) {
        console.log('------------ onProcessStateChanged -----------', processData);
    }
  }
  const observerCode = app.registerApplicationStateObserver(applicationStateObserver);
  console.log('-------- observerCode: ---------', observerCode);

```

## ApplicationStateObserver.onAbilityStateChanged<sup>8+</sup>

onAbilityStateChanged(abilityStateData: AbilityStateData): void;

Called when the ability state changes.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| abilityStateData | [AbilityStateData](#abilitystatedata) | No| Information about the ability whose state is changed.|

**Example**
    
```js
  var applicationStateObserver = {
    onForegroundApplicationChanged(appStateData) {
        console.log('------------ onForegroundApplicationChanged -----------', appStateData);
    },
    onAbilityStateChanged(abilityStateData) {
        console.log('------------ onAbilityStateChanged -----------', abilityStateData);
    },
    onProcessCreated(processData) {
        console.log('------------ onProcessCreated -----------', processData);
    },
    onProcessDied(processData) {
        console.log('------------ onProcessDied -----------', processData);
    },
    onProcessStateChanged(processData) {
        console.log('------------ onProcessStateChanged -----------', processData);
    }
  }
  const observerCode = app.registerApplicationStateObserver(applicationStateObserver);
  console.log('-------- observerCode: ---------', observerCode);
```

## ApplicationStateObserver.onProcessCreated<sup>8+</sup>

onProcessCreated(processData: ProcessData): void;

Called when a process is created.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| processData | [ProcessData](#processdata) | No| Process information.|

**Example**
    
```js
  var applicationStateObserver = {
    onForegroundApplicationChanged(appStateData) {
        console.log('------------ onForegroundApplicationChanged -----------', appStateData);
    },
    onAbilityStateChanged(abilityStateData) {
        console.log('------------ onAbilityStateChanged -----------', abilityStateData);
    },
    onProcessCreated(processData) {
        console.log('------------ onProcessCreated -----------', processData);
    },
    onProcessDied(processData) {
        console.log('------------ onProcessDied -----------', processData);
    },
    onProcessStateChanged(processData) {
        console.log('------------ onProcessStateChanged -----------', processData);
    }
  }
  const observerCode = app.registerApplicationStateObserver(applicationStateObserver);
  console.log('-------- observerCode: ---------', observerCode);
```

## ApplicationStateObserver.onProcessDied<sup>8+</sup>

onProcessDied(processData: ProcessData): void;

Called when a process is terminated.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| processData | [ProcessData](#processdata) | No| Process information.|

**Example**
    
```js
  var applicationStateObserver = {
    onForegroundApplicationChanged(appStateData) {
        console.log('------------ onForegroundApplicationChanged -----------', appStateData);
    },
    onAbilityStateChanged(abilityStateData) {
        console.log('------------ onAbilityStateChanged -----------', abilityStateData);
    },
    onProcessCreated(processData) {
        console.log('------------ onProcessCreated -----------', processData);
    },
    onProcessDied(processData) {
        console.log('------------ onProcessDied -----------', processData);
    },
    onProcessStateChanged(processData) {
        console.log('------------ onProcessStateChanged -----------', processData);
    }
  }
  const observerCode = app.registerApplicationStateObserver(applicationStateObserver);
  console.log('-------- observerCode: ---------', observerCode);
```

## ApplicationStateObserver.onProcessStateChanged<sup>9+</sup>

 onProcessStateChanged(processData: ProcessData): void;

Called when the process state changes.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| processData | [ProcessData](#processdata) | No| Process information.|

**Example**
    
```js
  var applicationStateObserver = {
    onForegroundApplicationChanged(appStateData) {
        console.log('------------ onForegroundApplicationChanged -----------', appStateData);
    },
    onAbilityStateChanged(abilityStateData) {
        console.log('------------ onAbilityStateChanged -----------', abilityStateData);
    },
    onProcessCreated(processData) {
        console.log('------------ onProcessCreated -----------', processData);
    },
    onProcessDied(processData) {
        console.log('------------ onProcessDied -----------', processData);
    },
    onProcessStateChanged(processData) {
        console.log('------------ onProcessStateChanged -----------', processData);
    }
  }
  const observerCode = app.registerApplicationStateObserver(applicationStateObserver);
  console.log('-------- observerCode: ---------', observerCode);
```

## AppStateData

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

| Name       | Readable/Writable| Type                | Mandatory| Description                                                        |
| ----------- | -------- | -------------------- | ---- | ------------------------------------------------------------ |
| bundleName<sup>8+</sup>     | Read only    | string               | No  | Bundle name of an application.                               |
| uid<sup>8+</sup>   | Read only    | number               | No  | User ID.|
| state<sup>8+</sup>  | Read only    | number               | No  | Application state.|

## AbilityStateData

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

| Name                    | Type    | Readable| Writable| Description                      |
| ----------------------- | ---------| ---- | ---- | ------------------------- |
| pid<sup>8+</sup>                     | number   | Yes  | No  | Process ID.                   |
| bundleName<sup>8+</sup>              | string   | Yes  | No | Bundle name of an application.                 |
| abilityName<sup>8+</sup>             | string   | Yes  | No  | Ability name.              |
| uid<sup>8+</sup>                     | number   | Yes  | No  | User ID.                 |
| state<sup>8+</sup>                   | number   | Yes  | No  | Ability state.               |
| moduleName<sup>9+</sup> | string   | Yes  | No  | Name of the HAP file to which the ability belongs.   |
| abilityType<sup>8+</sup> | string   | Yes  | No  | Ability type.   |

## ProcessData

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

| Name                    | Type    | Readable| Writable| Description                      |
| ----------------------- | ---------| ---- | ---- | ------------------------- |
| pid<sup>8+</sup>         | number   | Yes  | No  | Process ID.                   |
| bundleName<sup>8+</sup>  | string   | Yes  | No | Bundle name of an application.                 |
| uid<sup>8+</sup>         | number   | Yes  | No  | User ID.                 |
| isContinuousTask<sup>9+</sup>         | boolean   | Yes  | No  | Whether the process is a continuous task.                 |
| isKeepAlive<sup>9+</sup>         | boolean   | Yes  | No  | Whether the process remains active.                 |

## ProcessRunningInfo

**System capability**: SystemCapability.Ability.AbilityRuntime.Mission

| Name       | Readable/Writable| Type                | Mandatory| Description                                                        |
| ----------- | -------- | -------------------- | ---- | ------------------------------------------------------------ |
| pid<sup>8+</sup>     | Read only    | number               | No  | Process ID.                               |
| uid<sup>8+</sup>   | Read only    | number               | No  | User ID.|
| processName<sup>8+</sup>  | Read only    | string               | No  | Process name.|
| bundleNames<sup>8+</sup>          | Read only    | Array\<string>              | No  | **bundleName** array in the running processes.|

## ApplicationStateObserver

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

| Name                    | Type    | Readable| Writable| Description                      |
| ----------------------- | ---------| ---- | ---- | ------------------------- |
| [onForegroundApplicationChanged<sup>8+</sup>](#applicationstateobserveronforegroundapplicationchanged8)         | AsyncCallback\<void>   | Yes  | No  | Callback invoked when the foreground or background state of an application changes.                   |
| [onAbilityStateChanged<sup>8+</sup>](#applicationstateobserveronabilitystatechanged8)  | AsyncCallback\<void>   | Yes  | No | Callback invoked when the ability state changes.                 |
| [onProcessCreated<sup>8+</sup>](#applicationstateobserveronprocesscreated8)         | AsyncCallback\<void>   | Yes  | No  | Callback invoked when a process is created.                 |
| [onProcessDied<sup>8+</sup>](#applicationstateobserveronprocessdied8)         | AsyncCallback\<void>   | Yes  | No  | Callback invoked when a process is destroyed.                 |

## ProcessRunningInformation
   
Defines the process running information.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name       | Readable/Writable| Type                | Mandatory| Description                                                        |
| ----------- | -------- | -------------------- | ---- | ------------------------------------------------------------ |
| pid<sup>9+</sup>     | Read only    | number               | No  | Process ID.                               |
| uid<sup>9+</sup>   | Read only    | number               | No  | User ID.|
| processName<sup>9+</sup>  | Read only    | string               | No  | Process name.|
| bundleNames<sup>9+</sup>          | Read only    | Array\<string>              | No  | **bundleName** array in the running processes.| 

## ApplicationState<sup>9+</sup>

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

| Name                | Value | Description                              |
| -------------------- | --- | --------------------------------- |
| STATE_CREATE    | 1   |   State indicating that the application is being created.        |
| STATE_FOREGROUND          | 2   |      State indicating that the application is running in the foreground.           |
| STATE_ACTIVE  | 3   |         State indicating that the application is active.    |
| STATE_BACKGROUND        | 4   |       State indicating that the application is running in the background.          |
| STATE_DESTROY        | 5   |           State indicating that the application is destroyed.      |

## ProcessState<sup>9+</sup>

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

| Name                | Value | Description                              |
| -------------------- | --- | --------------------------------- |
| STATE_CREATE    | 1   |      State indicating that the process is being created.      |
| STATE_FOREGROUND          | 2   |            State indicating that the process is running in the foreground.     |
| STATE_ACTIVE  | 3   |          State indicating that the process is active.  |
| STATE_BACKGROUND        | 4   |       State indicating that the process is running in the background.          |
| STATE_DESTROY        | 5   |         State indicating that the process is destroyed.        |
