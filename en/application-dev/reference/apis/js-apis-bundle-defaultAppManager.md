# DefaultAppManager

The **DefaultAppManager** module provides APIs to query whether the current application is the default application of a specific type.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```
import defaultAppMgr from '@ohos.bundle.defaultAppManager'
```
## defaultAppMgr.ApplicationType

Enumerates the application types.

**System capability**: SystemCapability.BundleManager.BundleFramework

| Name     | Type    | Description                                  |
| -------- | -------- | -------------------------------------- |
| BROWSER  | string   | Default browser.                           |
| IMAGE    | string   | Default image viewer.                        |
| AUDIO    | string   | Default audio player.                        |
| VIDEO    | string   | Default video player.                        |
| PDF      | string   | Default PDF reader.                     |
| WORD     | string   | Default Word viewer.                    |
| EXCEL    | string   | Default Excel viewer.                   |
| PPT      | string   | Default PowerPoint viewer.                     |

## defaultAppMgr.isDefaultApplication

isDefaultApplication(type: string): Promise\<boolean>

Checks whether this application is the default application of a system-defined application type. This API uses a promise to return the result.

**System capability**: SystemCapability.BundleManager.BundleFramework

**Parameters**

| Name         | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](#defaultappmgrapplicationtype).                          |

**Return value**

| Type                       | Description                |
| ------------------------- | ------------------ |
| Promise\<boolean> | Promise used to return the result. If the application is the default application, `true` is returned; otherwise, `false` is returned.|

**Example**

```js
defaultAppMgr.isDefaultApplication(defaultAppMgr.ApplicationType.BROWSER)
.then((data) => {
    console.info('Operation successful. IsDefaultApplication ? ' + JSON.stringify(data));
}).catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
});
```

## defaultAppMgr.isDefaultApplication

isDefaultApplication(type: string, callback: AsyncCallback\<boolean>): void

Checks whether this application is the default application of a system-defined application type. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.BundleManager.BundleFramework

**Parameters**

| Name         | Type                             | Mandatory  | Description                                     |
| ----------- | ------------------------------- | ---- | --------------------------------------- |
| type  | string                          | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](#defaultappmgrapplicationtype).                           |
| callback    | AsyncCallback\<boolean> | Yes   | Callback used to return the result. If the application is the default application, `true` is returned; otherwise, `false` is returned.|

**Example**

```js
defaultAppMgr.isDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. IsDefaultApplication ? ' + JSON.stringify(data));
 });
```

## defaultAppMgr.getDefaultApplication

getDefaultApplication(type: string, userId?: number): Promise\<BundleInfo>

Obtains the default application based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses a promise to return the result.

**Required permissions**: ohos.permission.GET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name         | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| userId  | number | No   | User ID. The default value is the user ID of the caller.                        |

**Return value**

| Type                       | Description                |
| ------------------------- | ------------------ |
| Promise\<[BundleInfo](js-apis-bundle-BundleInfo.md)> | Promise used to return the default application.|

**Example**

```js
defaultAppMgr.getDefaultApplication(defaultAppMgr.ApplicationType.BROWSER)
.then((data) => {
    console.info('Operation successful. bundleInfo: ' + JSON.stringify(data));
})
.catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
});

defaultAppMgr.getDefaultApplication("image/png")
.then((data) => {
    console.info('Operation successful. bundleInfo: ' + JSON.stringify(data));
})
.catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
});
```

## defaultAppMgr.getDefaultApplication

getDefaultApplication(type: string, userId: number, callback: AsyncCallback\<BundleInfo>) : void

Obtains the default application of a user based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name         | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| userId  | number | Yes   | User ID.                          |
| callback    | AsyncCallback\<[BundleInfo](js-apis-bundle-BundleInfo.md)> | Yes   | Callback used to return the default application.                   |

**Example**

```js
defaultAppMgr.getDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, 100, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. bundleInfo:' + JSON.stringify(data));
});

defaultAppMgr.getDefaultApplication("image/png", 100, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. bundleInfo:' + JSON.stringify(data));
});
```

## defaultAppMgr.getDefaultApplication

getDefaultApplication(type: string, callback: AsyncCallback\<BundleInfo>) : void

Obtains the default application based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.GET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name         | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| callback    | AsyncCallback\<[BundleInfo](js-apis-bundle-BundleInfo.md)> | Yes   | Callback used to return the default application.                   |

**Example**

```js
defaultAppMgr.getDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. bundleInfo:' + JSON.stringify(data));
});

defaultAppMgr.getDefaultApplication("image/png", (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful. bundleInfo:' + JSON.stringify(data));
});
```

## defaultAppMgr.setDefaultApplication

setDefaultApplication(type: string, elementName: ElementName, userId?: number): Promise\<void>

Sets the default application based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses a promise to return the result.

**Required permissions**: ohos.permission.SET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name         | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| elementName  | [ElementName](js-apis-bundle-ElementName.md) | Yes   | Information about the element to be set as the default application.                          |
| userId  | number | No   | User ID. The default value is the user ID of the caller.                          |

**Example**

```js
defaultAppMgr.setDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, {
    bundleName: "com.test.app",
    moduleName: "module01",
    abilityName: "MainAbility"
})
.then((data) => {
    console.info('Operation successful.');
})
.catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
});

defaultAppMgr.setDefaultApplication("image/png", {
    bundleName: "com.test.app",
    moduleName: "module01",
    abilityName: "MainAbility"
})
.then((data) => {
    console.info('Operation successful.');
})
.catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
});
```

## defaultAppMgr.setDefaultApplication

setDefaultApplication(type: string, elementName: ElementName, userId: number, callback: AsyncCallback\<void>) : void;

Sets the default application for a user based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name         | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| elementName  | [ElementName](js-apis-bundle-ElementName.md) | Yes   | Information about the element to be set as the default application.                          |
| userId  | number | Yes   | User ID.                          |
| callback    | AsyncCallback\<void> | Yes   | Callback used to return the result.                   |

**Example**

```js
defaultAppMgr.setDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, {
    bundleName: "com.test.app",
    moduleName: "module01",
    abilityName: "MainAbility"
}, 100, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful.');
 });

defaultAppMgr.setDefaultApplication("image/png", {
    bundleName: "com.test.app",
    moduleName: "module01",
    abilityName: "MainAbility"
}, 100, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful.');
 });
```

## defaultAppMgr.setDefaultApplication

setDefaultApplication(type: string, elementName: ElementName, callback: AsyncCallback\<void>) : void;

Sets the default application based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name         | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| elementName  | [ElementName](js-apis-bundle-ElementName.md) | Yes   | Information about the element to be set as the default application.                          |
| callback    | AsyncCallback\<void> | Yes   | Callback used to return the result.                   |

**Example**

```js
defaultAppMgr.setDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, {
    bundleName: "com.test.app",
    moduleName: "module01",
    abilityName: "MainAbility"
}, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful.');
 });

defaultAppMgr.setDefaultApplication("image/png", {
    bundleName: "com.test.app",
    moduleName: "module01",
    abilityName: "MainAbility"
}, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful.');
 });
```

## defaultAppMgr.resetDefaultApplication

resetDefaultApplication(type: string, userId?: number): Promise\<void>

Resets the default application based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses a promise to return the result.

**Required permissions**: ohos.permission.SET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name         | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| userId  | number | No   | User ID. The default value is the user ID of the caller.                          |

**Example**

```js
defaultAppMgr.resetDefaultApplication(defaultAppMgr.ApplicationType.BROWSER)
.then((data) => {
    console.info('Operation successful.');
})
.catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
});

defaultAppMgr.resetDefaultApplication("image/png")
.then((data) => {
    console.info('Operation successful.');
})
.catch((error) => {
    console.error('Operation failed. Cause: ' + JSON.stringify(error));
});
```

## defaultAppMgr.resetDefaultApplication

resetDefaultApplication(type: string, userId: number, callback: AsyncCallback\<void>) : void;

Resets the default application for a user based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name         | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| userId  | number | Yes   | User ID.                         |
| callback    | AsyncCallback\<void> | Yes   | Callback used to return the result.                   |

**Example**

```js
defaultAppMgr.resetDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, 100, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful.');
});

defaultAppMgr.resetDefaultApplication("image/png", 100, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful.');
});
```

## defaultAppMgr.resetDefaultApplication

resetDefaultApplication(type: string, callback: AsyncCallback\<void>) : void;

Resets the default application based on a system-defined application type or a file type that complies with the media type format (either specified by **type** or **subtype**). This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_DEFAULT_APPLICATION

**System capability**: SystemCapability.BundleManager.BundleFramework

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name         | Type    | Mandatory  | Description                                     |
| ----------- | ------ | ---- | --------------------------------------- |
| type  | string | Yes   | Type of the target application. It must be set to a value defined by [ApplicationType](#defaultappmgrapplicationtype) or a file type that complies with the media type format.      |
| callback    | AsyncCallback\<void> | Yes   | Callback used to return the result.                   |

**Example**

```js
defaultAppMgr.resetDefaultApplication(defaultAppMgr.ApplicationType.BROWSER, (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful.');
});

defaultAppMgr.resetDefaultApplication("image/png", (err, data) => {
    if (err) {
        console.error('Operation failed. Cause: ' + JSON.stringify(err));
        return;
    }
    console.info('Operation successful.');
});
```
