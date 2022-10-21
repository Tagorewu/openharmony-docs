# 输入法子类型

本模块提供对输入法子类型的属性管理

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
>
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```
import inputMethodEngine from '@ohos.inputMethodSubtype';
```

## InputMethodSubtype

属性值。

**系统能力**：以下各项对应的系统能力均为SystemCapability.MiscServices.InputMethodFramework

| 名称 | 参数类型 | 可读 | 可写 | 必选 | 说明 |
| -------- | -------- | -------- | -------- | -------- | -------- |
| label | string | 是 | 否 | 否 | 输入法子类型的标签。 |
| name | string | 是 | 否 | 是 | 输入法子类型的名字。 |
| id | string | 是 | 否 | 是 | 输入法子类型的id。 |
| mode | string | 是 | 否 | 否 | 输入法子类型的模式，包括upper和lower。 |
| locale | string | 是 | 否 | 是 | 输入法子类型的locale。 |
| language | string | 是 | 否 | 是 | 输入法子类型的语言。 |
| icon | string | 是 | 否 | 否 | 输入法子类型的图标。 |
| iconId | number | 是 | 否 | 否 | 输入法子类型的图标id。 |
| extra | object | 是 | 是 | 是 | 输入法子类型的其他信息。 |