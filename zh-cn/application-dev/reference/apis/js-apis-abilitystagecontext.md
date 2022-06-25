# AbilityStageContext

> **说明：**
> 
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。  
> 本模块接口仅可在Stage模型下使用。

AbilityStage的上下文环境，继承自[Context](js-apis-application-context.md)。

## 导入模块

```js
import AbilityStage from '@ohos.application.AbilityStage';
```

## 使用说明

通过AbilityStage实例来获取。

```js
import AbilityStage from '@ohos.application.AbilityStage';
class MyAbilityStage extends AbilityStage {
    onCreate() {
        let abilityStageContext = this.context;
    }
}
```

## 属性

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

| 名称 | 参数类型 | 可读 | 可写 | 说明 | 
| -------- | -------- | -------- | -------- | -------- |
| currentHapModuleInfo | HapModuleInfo | 是 | 否 | AbilityStage对应的ModuleInfo对象。 | 
| config | [Configuration](js-apis-configuration.md) | 是 | 否 | 环境变化对象。 | 
