# FormExtensionContext

The **FormExtensionContext** module, inherited from **ExtensionContext**, provides context for Form Extension abilities.

You can use the APIs of this module to start abilities.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version. 
> The APIs of this module can be used only in the stage model.

## FormExtensionContext.updateForm

updateForm(formId: string, formBindingData: formBindingData.FormBindingData, callback: AsyncCallback\<void>): void

Updates a widget. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name         | Type                                                        | Mandatory| Description                                  |
| --------------- | ------------------------------------------------------------ | ---- | -------------------------------------- |
| formId          | string                                                       | Yes  | ID of the widget that requests to be updated.                    |
| formBindingData | [formBindingData.FormBindingData](js-apis-formbindingdata.md#formbindingdata) | Yes  | New data of the widget.                        |
| callback        | AsyncCallback\<void>                                         | Yes  | Callback used to return the result.|

**Example**

  ```js
  import formBindingData from '@ohos.application.formBindingData'
  export default class MyFormExtension extends FormExtension {
      onUpdate(formId) {
          console.log('FormExtension onUpdate, formId:' + formId);
          let obj2 = formBindingData.createFormBindingData({temperature:"22c", time:"22:00"});
          this.context.updateForm(formId, obj2, (data)=>{
              console.log('FormExtension context updateForm, data:' + data);
          });
      }
  }


  ```

## FormExtensionContext.updateForm

updateForm(formId: string, formBindingData: formBindingData.FormBindingData): Promise\<void>

Updates a widget. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.Form

**Parameters**

| Name         | Type                                                        | Mandatory| Description              |
| --------------- | ------------------------------------------------------------ | ---- | ------------------ |
| formId          | string                                                       | Yes  | ID of the widget that requests to be updated.|
| formBindingData | [formBindingData.FormBindingData](js-apis-formbindingdata.md#formbindingdata) | Yes  | New data of the widget.    |

**Return value**

| Type          | Description                             |
| -------------- | --------------------------------- |
| Promise\<void> | Promise used to return the result.|

**Example**

  ```js
  import formBindingData from '@ohos.application.formBindingData'
  export default class MyFormExtension extends FormExtension {
      onUpdate(formId) {
          console.log('FormExtension onUpdate, formId:' + formId);
          let obj2 = formBindingData.createFormBindingData({temperature:"22c", time:"22:00"});
          this.context.updateForm(formId, obj2)
              .then((data)=>{
                  console.log('FormExtension context updateForm, data:' + data);
              }).catch((error) => {
              console.error('Operation updateForm failed. Cause: ' + error);});
      }
  }

  ```
