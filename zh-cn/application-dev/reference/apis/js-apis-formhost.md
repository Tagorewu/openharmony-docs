# FormHost

FormHost模块提供了卡片使用方相关接口的能力，包括删除、释放、请求更新卡片，发送通知到指定卡片，获取卡片信息、状态等。

> **说明：**
> 
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。  
> 本模块接口均为系统接口，三方应用不支持调用。

## 导入模块

```
import formHost from '@ohos.application.formHost';
```

## 权限

ohos.permission.REQUIRE_FORM

ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

## deleteForm

deleteForm(formId: string, callback: AsyncCallback&lt;void&gt;): void;

删除指定的卡片。调用此方法后，应用程序将无法使用该卡片，卡片管理器服务不再保留有关该卡片的信息。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formId | string | 是   | 卡片标识 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回结果 |

**示例：**

  ```js
  var formId = "12400633174999288";
  formHost.deleteForm(formId, (error, data) => {
      if (error.code) {
          console.log('formHost deleteForm, error:' + JSON.stringify(error));
      }
  });
  ```

## deleteForm

deleteForm(formId: string): Promise&lt;void&gt;;

删除指定的卡片。调用此方法后，应用程序将无法使用该卡片，卡片管理器服务不再保留有关该卡片的信息。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

  | 参数名 | 类型    | 必填 | 说明    |
  | ------ | ------ | ---- | ------- |
  | formId | string | 是   | 卡片标识 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 返回一个Promise，包含接口的结果 |

**参数：**

  ```js
  var formId = "12400633174999288";
  formHost.deleteForm(formId).then(() => {
      console.log('formHost deleteForm success');
  }).catch((error) => {
      console.log('formHost deleteForm, error:' + JSON.stringify(error));
  });
  ```

## releaseForm

releaseForm(formId: string, callback: AsyncCallback&lt;void&gt;): void;

释放指定的卡片。调用此方法后，应用程序将无法使用该卡片，但卡片管理器服务仍然保留有关该卡片的缓存信息和存储信息。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formId | string | 是   | 卡片标识 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回结果 |

**示例：**

  ```js
  var formId = "12400633174999288";
  formHost.releaseForm(formId, (error, data) => {
      if (error.code) {
          console.log('formHost releaseForm, error:' + JSON.stringify(error));
      }
  });
  ```

## releaseForm

releaseForm(formId: string, isReleaseCache: boolean, callback: AsyncCallback&lt;void&gt;): void;

释放指定的卡片。调用此方法后，应用程序将无法使用该卡片，卡片管理器服务保留有关该卡片的存储信息，可以选择是否保留缓存信息。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名         | 类型     | 必填 | 说明        |
| -------------- | ------  | ---- | ----------- |
| formId         | string  | 是   | 卡片标识     |
| isReleaseCache | boolean | 是   | 是否释放缓存 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回结果 |

**示例：**

  ```js
  var formId = "12400633174999288";
  formHost.releaseForm(formId, true, (error, data) => {
      if (error.code) {
          console.log('formHost releaseForm, error:' + JSON.stringify(error));
      }
  });
  ```

## releaseForm

releaseForm(formId: string, isReleaseCache?: boolean): Promise&lt;void&gt;;

释放指定的卡片。调用此方法后，应用程序将无法使用该卡片，卡片管理器服务保留有关该卡片的存储信息，可以选择是否保留缓存信息。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

  | 参数名         | 类型     | 必填 | 说明        |
  | -------------- | ------  | ---- | ----------- |
  | formId         | string  | 是   | 卡片标识     |
  | isReleaseCache | boolean | 否   | 是否释放缓存 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 返回一个Promise，包含接口的结果 |

**示例：**

  ```js
  var formId = "12400633174999288";
  formHost.releaseForm(formId, true).then(() => {
      console.log('formHost releaseForm success');
  }).catch((error) => {
      console.log('formHost releaseForm, error:' + JSON.stringify(error));
  });
  ```

## requestForm

requestForm(formId: string, callback: AsyncCallback&lt;void&gt;): void;

请求卡片更新。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formId | string | 是   | 卡片标识 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回结果 |

**示例：**

  ```js
  var formId = "12400633174999288";
  formHost.requestForm(formId, (error, data) => {
      if (error.code) {
          console.log('formHost requestForm, error:' + JSON.stringify(error));
      }
  });
  ```

## requestForm

requestForm(formId: string): Promise&lt;void&gt;;

请求卡片更新。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

  | 参数名 | 类型    | 必填 | 说明    |
  | ------ | ------ | ---- | ------- |
  | formId | string | 是   | 卡片标识 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 返回一个Promise，包含接口的结果 |

**示例：**

  ```js
  var formId = "12400633174999288";
  formHost.requestForm(formId).then(() => {
      console.log('formHost requestForm success');
  }).catch((error) => {
      console.log('formHost requestForm, error:' + JSON.stringify(error));
  });
  ```

## castTempForm

castTempForm(formId: string, callback: AsyncCallback&lt;void&gt;): void;

将指定的临时卡片转换为普通卡片。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formId | string | 是   | 卡片标识 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回结果 |

**示例：**

  ```js
  var formId = "12400633174999288";
  formHost.castTempForm(formId, (error, data) => {
      if (error.code) {
          console.log('formHost castTempForm, error:' + JSON.stringify(error));
      }
  });
  ```

## castTempForm

castTempForm(formId: string): Promise&lt;void&gt;;

将指定的临时卡片转换为普通卡片。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

  | 参数名 | 类型    | 必填 | 说明    |
  | ------ | ------ | ---- | ------- |
  | formId | string | 是   | 卡片标识 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 返回一个Promise，包含接口的结果 |

**示例：**

  ```js
  var formId = "12400633174999288";
  formHost.castTempForm(formId).then(() => {
      console.log('formHost castTempForm success');
  }).catch((error) => {
      console.log('formHost castTempForm, error:' + JSON.stringify(error));
  });
  ```

## notifyVisibleForms

notifyVisibleForms(formIds: Array&lt;string&gt;, callback: AsyncCallback&lt;void&gt;): void;

向卡片框架发送通知以使指定的卡片可见。该方法调用成功后，会调用onVisibilityChange通知卡片提供方。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formIds  | Array&lt;string&gt;       | 是   | 卡片标识列表         |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回结果 |

**示例：**

  ```js
  var formId = ["12400633174999288"];
  formHost.notifyVisibleForms(formId, (error, data) => {
      if (error.code) {
          console.log('formHost notifyVisibleForms, error:' + JSON.stringify(error));
      }
  });
  ```

## notifyVisibleForms

notifyVisibleForms(formIds: Array&lt;string&gt;): Promise&lt;void&gt;;

向卡片框架发送通知以使指定的卡片可见。该方法调用成功后，会调用onVisibilityChange通知卡片提供方。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formIds | Array&lt;string&gt; | 是   | 卡片标识列表 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 返回一个Promise，包含接口的结果 |

**示例：**

  ```js
  var formId = ["12400633174999288"];
  formHost.notifyVisibleForms(formId).then(() => {
      console.log('formHost notifyVisibleForms success');
  }).catch((error) => {
      console.log('formHost notifyVisibleForms, error:' + JSON.stringify(error));
  });
  ```

## notifyInvisibleForms

notifyInvisibleForms(formIds: Array&lt;string&gt;, callback: AsyncCallback&lt;void&gt;): void;

向卡片框架发送通知以使指定的卡片不可见。该方法调用成功后，会调用onVisibilityChange通知卡片提供方。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formIds  | Array&lt;string&gt;       | 是   | 卡片标识列表         |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回结果 |

**示例：**

  ```js
  var formId = ["12400633174999288"];
  formHost.notifyInvisibleForms(formId, (error, data) => {
      if (error.code) {
          console.log('formHost notifyInvisibleForms, error:' + JSON.stringify(error));
      }
  });
  ```

## notifyInvisibleForms

notifyInvisibleForms(formIds: Array&lt;string&gt;): Promise&lt;void&gt;;

向卡片框架发送通知以使指定的卡片不可见。该方法调用成功后，会调用onVisibilityChange通知卡片提供方。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formIds | Array&lt;string&gt; | 是   | 卡片标识列表 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 返回一个Promise，包含接口的结果 |

**示例：**

  ```js
  var formId = ["12400633174999288"];
  formHost.notifyInvisibleForms(formId).then(() => {
      console.log('formHost notifyInvisibleForms success');
  }).catch((error) => {
      console.log('formHost notifyInvisibleForms, error:' + JSON.stringify(error));
  });
  ```

## enableFormsUpdate

enableFormsUpdate(formIds: Array&lt;string&gt;, callback: AsyncCallback&lt;void&gt;): void;

向卡片框架发送通知以使指定的卡片可以更新。该方法调用成功后，卡片刷新状态设置为使能，卡片可以接收来自卡片提供方的更新。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formIds  | Array&lt;string&gt;       | 是   | 卡片标识列表         |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回结果 |

**示例：**

  ```js
  var formId = ["12400633174999288"];
  formHost.enableFormsUpdate(formId, (error, data) => {
      if (error.code) {
          console.log('formHost enableFormsUpdate, error:' + JSON.stringify(error));
      }
  });
  ```

## enableFormsUpdate

enableFormsUpdate(formIds: Array&lt;string&gt;): Promise&lt;void&gt;;

向卡片框架发送通知以使指定的卡片可以更新。该方法调用成功后，卡片刷新状态设置为使能，卡片可以接收来自卡片提供方的更新。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formIds | Array&lt;string&gt; | 是   | 卡片标识列表 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 返回一个Promise，包含接口的结果 |

**示例：**

  ```js
  var formId = ["12400633174999288"];
  formHost.enableFormsUpdate(formId).then(() => {
      console.log('formHost enableFormsUpdate success');
  }).catch((error) => {
      console.log('formHost enableFormsUpdate, error:' + JSON.stringify(error));
  });
  ```

## disableFormsUpdate

disableFormsUpdate(formIds: Array&lt;string&gt;, callback: AsyncCallback&lt;void&gt;): void;

向卡片框架发送通知以使指定的卡片不可以更新。该方法调用成功后，卡片刷新状态设置为去使能，卡片不可以接收来自卡片提供方的更新。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formIds  | Array&lt;string&gt;       | 是   | 卡片标识列表         |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回结果 |

**示例：**

  ```js
  var formId = ["12400633174999288"];
  formHost.disableFormsUpdate(formId, (error, data) => {
      if (error.code) {
          console.log('formHost disableFormsUpdate, error:' + JSON.stringify(error));
      }
  });
  ```

## disableFormsUpdate

disableFormsUpdate(formIds: Array&lt;string&gt;): Promise&lt;void&gt;;

向卡片框架发送通知以使指定的卡片不可以更新。该方法调用成功后，卡片刷新状态设置为去使能，卡片不可以接收来自卡片提供方的更新。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formIds | Array&lt;string&gt; | 是   | 卡片标识列表 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 返回一个Promise，包含接口的结果 |

**示例：**

  ```js
  var formId = ["12400633174999288"];
  formHost.disableFormsUpdate(formId).then(() => {
      console.log('formHost disableFormsUpdate success');
  }).catch((error) => {
      console.log('formHost disableFormsUpdate, error:' + JSON.stringify(error));
  });
  ```

## isSystemReady

isSystemReady(callback: AsyncCallback&lt;void&gt;): void;

检查系统是否准备好。

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回结果 |

**示例：**

  ```js
  var formId = "12400633174999288";
  formHost.isSystemReady((error, data) => {
      if (error.code) {
          console.log('formHost isSystemReady, error:' + JSON.stringify(error));
      }
  });
  ```

## isSystemReady

isSystemReady(): Promise&lt;void&gt;;

检查系统是否准备好。

**系统能力**：SystemCapability.Ability.Form

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 返回一个Promise，包含接口的结果 |

**示例：**

  ```js
  var formId = "12400633174999288";
  formHost.isSystemReady().then(() => {
      console.log('formHost isSystemReady success');
  }).catch((error) => {
      console.log('formHost isSystemReady, error:' + JSON.stringify(error));
  });
  ```

## getAllFormsInfo

getAllFormsInfo(callback: AsyncCallback&lt;Array&lt;formInfo.FormInfo&gt;&gt;): void;

获取设备上所有应用提供的卡片信息。

**需要权限**：ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力**：SystemCapability.Ability.Form

**参数：**

  | 参数名 | 类型    | 必填 | 说明    |
  | ------ | ------ | ---- | ------- |
  | callback | AsyncCallback&lt;Array&lt;[FormInfo](./js-apis-formInfo.md#forminfo-1)&gt;&gt; | 是 | callback形式返回查询到的卡片信息 |

**示例：**

  ```js
  formHost.getAllFormsInfo((error, data) => {
      if (error.code) {
          console.log('formHost getAllFormsInfo, error:' + JSON.stringify(error));
      } else {
          console.log('formHost getAllFormsInfo, data:' + JSON.stringify(data));
      }
  });
  ```

## getAllFormsInfo

getAllFormsInfo(): Promise&lt;Array&lt;formInfo.FormInfo&gt;&gt;;


获取设备上所有应用提供的卡片信息。

**需要权限**：ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力**：SystemCapability.Ability.Form

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;Array&lt;[FormInfo](./js-apis-formInfo.md#forminfo-1)&gt;&gt; | Promise实例，用于获取异步返回查询到的卡片信息 |

**示例：**

  ```js
  formHost.getAllFormsInfo().then((data) => {
      console.log('formHost getAllFormsInfo data:' + JSON.stringify(data));
  }).catch((error) => {
      console.log('formHost getAllFormsInfo, error:' + JSON.stringify(error));
  });
  ```

## getFormsInfo

getFormsInfo(bundleName: string, callback: AsyncCallback&lt;Array&lt;formInfo.FormInfo&gt;&gt;): void;


获取设备上指定应用程序提供的卡片信息。

**需要权限**：ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力**：SystemCapability.Ability.Form

**参数：**

  | 参数名 | 类型    | 必填 | 说明    |
  | ------ | ------ | ---- | ------- |
  | bundleName | string | 是 |  要查询的应用程序包名称 |
  | callback | AsyncCallback&lt;Array&lt;[FormInfo](./js-apis-formInfo.md#forminfo-1)&gt;&gt; | 是 | callback形式返回查询到的卡片信息 |

**示例：**

  ```js
  formHost.getFormsInfo("com.example.ohos.formjsdemo", (error, data) => {
      if (error.code) {
          console.log('formHost getFormsInfo, error:' + JSON.stringify(error));
      } else {
          console.log('formHost getFormsInfo, data:' + JSON.stringify(data));
      }
  });
  ```

## getFormsInfo

getFormsInfo(bundleName: string, moduleName: string, callback: AsyncCallback&lt;Array&lt;formInfo.FormInfo&gt;&gt;): void;


获取设备上指定应用程序提供的卡片信息。

**需要权限**：ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力**：SystemCapability.Ability.Form

**参数：**

  | 参数名 | 类型    | 必填 | 说明    |
  | ------ | ------ | ---- | ------- |
  | bundleName | string | 是 |  要查询的应用程序包名称 |
  | moduleName | string | 是 |  要查询的模块名称 |
  | callback | AsyncCallback&lt;Array&lt;[FormInfo](./js-apis-formInfo.md#forminfo-1)&gt;&gt; | 是 | callback形式返回查询到的卡片信息 |

**示例：**

  ```js
  formHost.getFormsInfo("com.example.ohos.formjsdemo", "entry", (error, data) => {
      if (error.code) {
          console.log('formHost getFormsInfo, error:' + JSON.stringify(error));
      } else {
          console.log('formHost getFormsInfo, data:' + JSON.stringify(data));
      }
  });
  ```

## getFormsInfo

getFormsInfo(bundleName: string, moduleName?: string): Promise&lt;Array&lt;formInfo.FormInfo&gt;&gt;;


获取设备上指定应用程序提供的卡片信息。

**需要权限**：ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力**：SystemCapability.Ability.Form

**参数：**

  | 参数名 | 类型    | 必填 | 说明    |
  | ------ | ------ | ---- | ------- |
  | bundleName | string | 是 |  要查询的应用程序包名称 |
  | moduleName | string | 否 |  要查询的模块名称 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;Array&lt;[FormInfo](./js-apis-formInfo.md#forminfo-1)&gt;&gt; | Promise实例，用于获取异步返回查询到的卡片信息 |

**示例：**

  ```js
  formHost.getFormsInfo("com.example.ohos.formjsdemo", "entry").then((data) => {
      console.log('formHost getFormsInfo, data:' + JSON.stringify(data));
  }).catch((error) => {
      console.log('formHost getFormsInfo, error:' + JSON.stringify(error));
  });
  ```

## deleteInvalidForms

deleteInvalidForms(formIds: Array&lt;string&gt;, callback: AsyncCallback&lt;number&gt;): void;

根据列表删除应用程序的无效卡片。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formIds | Array&lt;string&gt; | 是   | 有效卡片标识列表 |
| callback | AsyncCallback&lt;number&gt; | 是 | callback形式返回删除的卡片个数 |

**示例：**

  ```js
  var formIds = new Array("12400633174999288", "12400633174999289");
  formHost.deleteInvalidForms(formIds, (error, data) => {
      if (error.code) {
          console.log('formHost deleteInvalidForms, error:' + JSON.stringify(error));
      } else {
          console.log('formHost deleteInvalidForms, data:' + JSON.stringify(data));
      }
  });
  ```

## deleteInvalidForms

deleteInvalidForms(formIds: Array&lt;string&gt;): Promise&lt;number&gt;;

根据列表删除应用程序的无效卡片。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formIds | Array&lt;string&gt; | 是   | 有效卡片标识列表 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;number&gt; | Promise实例，用于获取异步返回删除的卡片个数 |

**示例：**

  ```js
  var formIds = new Array("12400633174999288", "12400633174999289");
  formHost.deleteInvalidForms(formIds).then((data) => {
      console.log('formHost deleteInvalidForms, data:' + JSON.stringify(data));
  }).catch((error) => {
      console.log('formHost deleteInvalidForms, error:' + JSON.stringify(error));
  });
  ```

## acquireFormState

acquireFormState(want: Want, callback: AsyncCallback&lt;formInfo.FormStateInfo&gt;): void;

获取卡片状态

**需要权限**：ohos.permission.REQUIRE_FORM 和 ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| want | [Want](js-apis-application-Want.md) | 是   | 查询卡片状态时携带的want信息 |
| callback | AsyncCallback&lt;[FormStateInfo](js-apis-formInfo.md#formstateinfo)&gt; | 是 | callback形式返回卡片状态 |

**示例：**

  ```js
  var want = {
      "deviceId": "",
      "bundleName": "ohos.samples.FormApplication",
      "abilityName": "FormAbility",
      "parameters": {
          "ohos.extra.param.key.module_name": "entry",
          "ohos.extra.param.key.form_name": "widget",
          "ohos.extra.param.key.form_dimension": 2
      }
  };
  formHost.acquireFormState(want, (error, data) => {
      if (error.code) {
          console.log('formHost acquireFormState, error:' + JSON.stringify(error));
      } else {
          console.log('formHost acquireFormState, data:' + JSON.stringify(data));
      }
  });
  ```

## acquireFormState

acquireFormState(want: Want): Promise&lt;formInfo.FormStateInfo&gt;;

获取卡片状态。

**需要权限**：ohos.permission.REQUIRE_FORM 和 ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| want   | [Want](js-apis-application-Want.md) | 是   | 查询卡片状态时携带的want信息 |

**返回值：**

| 类型          | 说明                                |
| :------------ | :---------------------------------- |
| Promise&lt;[FormStateInfo](js-apis-formInfo.md#formstateinfo)&gt; | Promise实例，用于返回卡片状态 |

**示例：**

  ```js
  var want = {
      "deviceId": "",
      "bundleName": "ohos.samples.FormApplication",
      "abilityName": "FormAbility",
      "parameters": {
          "ohos.extra.param.key.module_name": "entry",
          "ohos.extra.param.key.form_name": "widget",
          "ohos.extra.param.key.form_dimension": 2
      }
  };
  formHost.acquireFormState(want).then((data) => {
      console.log('formHost acquireFormState, data:' + JSON.stringify(data));
  }).catch((error) => {
      console.log('formHost acquireFormState, error:' + JSON.stringify(error));
  });
  ```

## on("formUninstall")

on(type: "formUninstall", callback: Callback&lt;string&gt;): void;

订阅卡片卸载事件。

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| type | string | 是   | 填写"formUninstall"，表示卡片卸载事件 |
| callback | Callback&lt;string&gt; | 是 | 需要注册的事件回调方法 |

**示例：**

  ```js
  let callback = function(formId) {
      console.log('formHost on formUninstall, formId:' + formId);
  }
  formHost.on("formUninstall", callback);
  ```

## off("formUninstall")

off(type: "formUninstall", callback?: Callback&lt;string&gt;): void;

取消订阅卡片卸载事件。

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| type | string | 是   | 填写"formUninstall"，表示卡片卸载事件 |
| callback | Callback&lt;string&gt; | 否 | 需要注销的事件回调方法。缺省时，表示注销所有已注册事件回调 |

**示例：**

  ```js
  let callback = function(formId) {
      console.log('formHost on formUninstall, formId:' + formId);
  }
  formHost.off("formUninstall", callback);
  ```

## notifyFormsVisible

notifyFormsVisible(formIds: Array&lt;string&gt;, isVisible: boolean, callback: AsyncCallback&lt;void&gt;): void;

通知卡片是否可见。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formIds | Array&lt;string&gt; | 是   | 卡片标识列表 |
| isVisible | boolean | 是   | 是否可见 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回结果 |

**示例：**

  ```js
  var formIds = new Array("12400633174999288", "12400633174999289");
  formHost.notifyFormsVisible(formIds, true, (error, data) => {
      if (error.code) {
          console.log('formHost notifyFormsVisible, error:' + JSON.stringify(error));
      }
  });
  ```

## notifyFormsVisible

notifyFormsVisible(formIds: Array&lt;string&gt;, isVisible: boolean): Promise&lt;void&gt;;

通知卡片是否可见。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

  | 参数名 | 类型    | 必填 | 说明    |
  | ------ | ------ | ---- | ------- |
  | formIds | Array&lt;string&gt; | 是   | 卡片标识列表 |
  | isVisible | boolean | 是   | 是否可见 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 返回一个Promise，包含接口的结果 |

**示例：**

  ```js
  var formIds = new Array("12400633174999288", "12400633174999289");
  formHost.notifyFormsVisible(formIds, true).then(() => {
      console.log('formHost notifyFormsVisible success');
  }).catch((error) => {
      console.log('formHost notifyFormsVisible, error:' + JSON.stringify(error));
  });
  ```

## notifyFormsEnableUpdate

notifyFormsEnableUpdate(formIds: Array&lt;string&gt;, isEnableUpdate: boolean, callback: AsyncCallback&lt;void&gt;): void;

通知卡片是否启用更新状态。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formIds | Array&lt;string&gt; | 是   | 卡片标识列表 |
| isEnableUpdate | boolean | 是   | 是否使能更新 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回结果 |

**示例：**

  ```js
  var formIds = new Array("12400633174999288", "12400633174999289");
  formHost.notifyFormsEnableUpdate(formIds, true, (error, data) => {
      if (error.code) {
          console.log('formHost notifyFormsEnableUpdate, error:' + JSON.stringify(error));
      }
  });
  ```

## notifyFormsEnableUpdate

notifyFormsEnableUpdate(formIds: Array&lt;string&gt;, isEnableUpdate: boolean): Promise&lt;void&gt;;

通知卡片是否启用更新状态。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

  | 参数名 | 类型    | 必填 | 说明    |
  | ------ | ------ | ---- | ------- |
  | formIds | Array&lt;string&gt; | 是   | 卡片标识列表 |
  | isEnableUpdate | boolean | 是   | 是否使能更新 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 返回一个Promise，包含接口的结果 |

**示例：**

  ```js
  var formIds = new Array("12400633174999288", "12400633174999289");
  formHost.notifyFormsEnableUpdate(formIds, true).then(() => {
      console.log('formHost notifyFormsEnableUpdate success');
  }).catch((error) => {
      console.log('formHost notifyFormsEnableUpdate, error:' + JSON.stringify(error));
  });
  ```
## shareForm<sup>9+</sup>

shareForm(formId: string, deviceId: string, callback: AsyncCallback&lt;void&gt;): void;

指定formId和远程设备Id进行卡片分享。

此接口为系统接口。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

| 参数名 | 类型    | 必填 | 说明    |
| ------ | ------ | ---- | ------- |
| formId | string | 是   | 卡片标识 |
| deviceId | string | 是   | 远程设备标识 |
| callback | AsyncCallback&lt;void&gt; | 是 | callback形式返回结果 |

**示例：**

  ```js
  var formId = "12400633174999288";
  var deviceId = "EFC11C0C53628D8CC2F8CB5052477E130D075917034613B9884C55CD22B3DEF2";
  formHost.shareForm(formId, deviceId, (error, data) => {
      if (error.code) {
          console.log('formHost shareForm, error:' + JSON.stringify(error));
      }
  });
  ```

## shareForm<sup>9+</sup>

shareForm(formId: string, deviceId: string): Promise&lt;void&gt;;

指定formId和远程设备Id进行卡片分享。

此接口为系统接口。

**需要权限**：ohos.permission.REQUIRE_FORM

**系统能力**：SystemCapability.Ability.Form

**参数：**

  | 参数名 | 类型    | 必填 | 说明    |
  | ------ | ------ | ---- | ------- |
  | formId | string | 是   | 卡片标识 |
  | deviceId | string | 是   | 远程设备标识 |

**返回值：**

  | 类型 | 说明 |
  | -------- | -------- |
  | Promise&lt;void&gt; | 返回一个Promise，包含接口的结果 |

**参数：**

  ```js
  var formId = "12400633174999288";
  var deviceId = "EFC11C0C53628D8CC2F8CB5052477E130D075917034613B9884C55CD22B3DEF2";
  formHost.shareForm(formId, deviceId).then(() => {
      console.log('formHost shareForm success');
  }).catch((error) => {
      console.log('formHost shareForm, error:' + JSON.stringify(error));
  });
  ```