# InputMethodExtensionAbility

InputMethodExtensionAbility模块，提供生态输入法应用开发者通过InputMethodExtensionAbility、InputMethodExtensionContext接口创作输入法应用，并管理输入法应用生命周期。

> **说明：**
> 
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> 本模块接口仅可在Stage模型下使用。

## 导入模块

```
import InputMethodExtension from '@ohos.inputmethodextensionability';
```

## 属性

**系统能力**：SystemCapability.MiscServices.InputMethodFramework

| 名称 | 参数类型 | 可读 | 可写 | 说明 |
| -------- | -------- | -------- | -------- | -------- |
| context | [InputMethodExtensionContext](js-apis-inputmethod-extension-context.md) | 是 | 否 | InputMethodExtension的上下文环境，继承自ExtensionContext。 |


## InputMethodExtensionAbility.onCreate()

onCreate(want: Want): void;

Extension生命周期回调，在拉起Extension输入法应用时调用，执行初始化输入法应用操作。

**系统能力**：SystemCapability.MiscServices.InputMethodFramework

**参数：**

  | 参数名 | 类型 | 必填 | 说明 | 
  | -------- | -------- | -------- | -------- |
  | want |  [Want](js-apis-application-Want.md) | 是 | 当前Extension相关的Want类型信息，包括ability名称、bundle名称等。 | 

**示例：**

  ```js
  class InputMethodExt extends InputMethodExtensionAbility {
    onCreate(want) {
      console.log('onCreate, want:' + want.abilityName);
    }
  }
  ```


## InputMethodExtensionAbility.onDestroy()

onDestroy(): void;

Extension生命周期回调，在销毁输入法应用时回调，执行资源清理等操作。

**系统能力**：SystemCapability.MiscServices.InputMethodFramework

**示例：**

  ```js
  class InputMethodExt extends InputMethodExtensionAbility {
    onDestroy() {
      console.log('onDestroy');
    }
  }
  ```