# WLAN

> **NOTE**<br>
> The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.
The APIs described in this document are used only for non-universal products, such as routers.
The APIs of this module are not supported by OpenHarmony 3.1 Release.


## Modules to Import

```js
import wifiext from '@ohos.wifiext';
```

## wifiext.enableHotspot

enableHotspot(): boolean;

Enables the WLAN hotspot.

- **Required permissions**:
  ohos.permission.MANAGE_WIFI_HOTSPOT_EXT

- **System capability**:
  SystemCapability.Communication.WiFi.AP.Extension

- **Return value**:
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifiext.disableHotspot

disableHotspot(): boolean;

Disables the WLAN hotspot.

- **Required permissions**:
  ohos.permission.MANAGE_WIFI_HOTSPOT_EXT

- **System capability**:
  SystemCapability.Communication.WiFi.AP.Extension

- **Return value**:
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|


## wifiext.getSupportedPowerModel

getSupportedPowerModel(): Promise&lt;Array&lt;PowerModel&gt;&gt;

Obtains the supported power models. The API uses a promise to return the result.

- **Required permissions**:
  ohos.permission.GET_WIFI_INFO

- **System capability**:
  SystemCapability.Communication.WiFi.AP.Extension

- **Return value**:
  | Type| Description|
  | -------- | -------- |
  | Promise&lt;Array&lt;[PowerModel](#PowerModel)&gt;&gt; | Promise used to return the power models obtained.|


## PowerModel

Enumerates the power models.

| Name| Default Value| Description|
| -------- | -------- | -------- |
| SLEEPING | 0 | Sleeping|
| GENERAL | 1 | General|
| THROUGH_WALL | 2 | Through_wall|


## wifiext.getSupportedPowerModel

getSupportedPowerModel(callback: AsyncCallback&lt;Array&lt;PowerModel&gt;&gt;): void

Obtains the supported power models. The API uses an asynchronous callback to return the result.

- **Required permissions**:
  ohos.permission.GET_WIFI_INFO

- **System capability**:
  SystemCapability.Communication.WiFi.AP.Extension

- **Parameters**
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[PowerModel](#PowerModel)&gt; | Yes| Callback invoked to return the power models obtained.|


## wifiext.getPowerModel

getPowerModel(): Promise&lt;PowerModel&gt;

Obtains the power model. The API uses a promise to return the result.

- **Required permissions**:
  ohos.permission.GET_WIFI_INFO

- **System capability**:
  SystemCapability.Communication.WiFi.AP.Extension

- **Return value**:
  | Type| Description|
  | -------- | -------- |
  | Promise&lt;[PowerModel](#PowerModel)&gt; | Promise used to return the power model obtained.|


## wifiext.getPowerModel

getPowerModel(callback: AsyncCallback&lt;PowerModel&gt;): void

Obtains the power model. The API uses an asynchronous callback to return the result.

- **Required permissions**:
  ohos.permission.GET_WIFI_INFO

- **System capability**:
  SystemCapability.Communication.WiFi.AP.Extension

- **Parameters**
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | callback | AsyncCallback&lt;[PowerModel](#PowerModel)&gt; | Yes| Callback invoked to return the power mode obtained.|


## wifiext.setPowerModel

setPowerModel(model: PowerModel) : boolean;

 Sets the power model.

- **Required permissions**:
  ohos.permission.MANAGE_WIFI_HOTSPOT_EXT

- **System capability**:
  SystemCapability.Communication.WiFi.AP.Extension

- **Parameters**
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | model | AsyncCallback&lt;[PowerModel](#PowerModel)&gt; | Yes| Power model to set.|

- **Return value**:
  | **Type**| **Description**|
  | -------- | -------- |
  | boolean | Returns **true** if the operation is successful; returns **false** otherwise.|
