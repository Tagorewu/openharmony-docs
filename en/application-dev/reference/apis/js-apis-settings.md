# Settings

The **Settings** module provides APIs for setting data items.

> **NOTE**
>
> The initial APIs of this module are supported since API version 8. Updates will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```ts
import settings from '@ohos.settings';
```



## settings.getUriSync

getUriSync(name: string): string

Obtains the URI of a data item.

**System capability**: SystemCapability.Applictaions.settings.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| settings.display.SCREEN_BRIGHTNESS_STATUS | string | Yes| Brightness of the target data item.|
| settings.date.TIME_FORMAT | string | Yes| Time format of the target data item. Data |

**Return value**

| Type| Description|
| -------- | -------- |
| string | URI of the data item.|

**Example**

```ts
 // Obtain the URI of a data item.
 let urivar = settings.getUriSync(settings.display.SCREEN_BRIGHTNESS_STATUS);  
```


## settings.getValueSync

getValueSync(dataAbilityHelper: DataAbilityHelper, name: string, defValue: string): string

Obtains the value of a data item.

**System capability**: SystemCapability.Applictaions.settings.Core

**Parameters**
| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| dataAbilityHelper | [DataAbilityHelper](js-apis-dataAbilityHelper.md) | Yes| **DataAbilityHelper** class.|
| name | string | Yes| Name of the target data item. Data items can be classified as follows:<br> <ul><li>Existing data items in the database, for example:<br></li> <ul><li>Brightness: **settings.display.SCREEN_BRIGHTNESS_STATUS**<br> </li>  <li>Time format: **settings.date.TIME_FORMAT**<br> </li></ul> <li>Custom data items</li></ul> |
| defValue | string | Yes| Default value This parameter is user-defined. If it is not found in the database, the default value is returned.|

**Return value**

| Type| Description|
| -------- | -------- |
| string | Value of the data item.|

**Example**

```ts
  import featureAbility from '@ohos.ability.featureAbility';

// Obtain the value of settings.display.SCREEN_BRIGHTNESS_STATUS (this data item already exists in the database).
let uri = settings.getUriSync(settings.display.SCREEN_BRIGHTNESS_STATUS);
let helper = featureAbility.acquireDataAbilityHelper(uri);
let value = settings.getValueSync(helper, settings.display.SCREEN_BRIGHTNESS_STATUS, '10');
```


## settings.setValueSync

setValueSync(dataAbilityHelper: DataAbilityHelper, name: string, value: string): boolean

Sets the value of a data item.

If the specified data item exists in the database, the **setValueSync** method updates the value of the data item. If the data item does not exist in the database, the **setValueSync** method inserts the data item into the database.

**Required permissions**: ohos.permission.MODIFY_SETTINGS

**System capability**: SystemCapability.Applictaions.settings.Core

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| dataAbilityHelper | [DataAbilityHelper](js-apis-dataAbilityHelper.md) | Yes| **DataAbilityHelper** class.|
| name | string | Yes| Name of the target data item. Data items can be classified as follows:<br> <ul><li>Existing data items in the database, for example:<br></li> <ul><li>Brightness: **settings.display.SCREEN_BRIGHTNESS_STATUS**<br> </li>  <li>Time format: **settings.date.TIME_FORMAT**<br> </li></ul> <li>Custom data items</li></ul> |
| value | string | Yes| Value of the data item.The value of range with the service.|

**Return value**

| Type| Description|
| -------- | -------- |
| boolean | Result indicating whether the value is set successfully. Returns **true** if the value is set successfully; returns **false** otherwise.|

**Example**

```ts
  import featureAbility from '@ohos.ability.featureAbility';

// Update the value of settings.display.SCREEN_BRIGHTNESS_STATUS. (As this data item exists in the database, the setValueSync 
   method will update the value of the data item.)
let uri = settings.getUriSync(settings.display.SCREEN_BRIGHTNESS_STATUS);
let helper = featureAbility.acquireDataAbilityHelper(uri);
let ret = settings.setValueSync(helper, settings.display.SCREEN_BRIGHTNESS_STATUS, '100');
```