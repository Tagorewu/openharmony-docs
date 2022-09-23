# TextInput

可以输入单行文本并支持响应输入事件的组件。

>  **说明：**
>
>  该组件从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 子组件

无


## 接口

TextInput(value?:{placeholder?: ResourceStr, text?: ResourceStr, controller?: TextInputController})

**参数：**

| 参数名                     | 参数类型                                     | 必填   | 参数描述            |
| ----------------------- | ---------------------------------------- | ---- | --------------- |
<<<<<<< Updated upstream
| placeholder   | [ResourceStr](ts-types.md#resourcestr)       | 否    | 无输入时的提示文本。      |
| text          | [ResourceStr](ts-types.md#resourcestr)       | 否    | 设置输入框当前的文本内容。     |
| controller<sup>8+</sup> | [TextInputController](#textinputcontroller8) | 否    | 设置TextInput控制器。 |


## 属性

除支持通用属性以及[文本样式设置](ts-universal-attributes-text-style.md)的属性外，还支持以下属性：

| 名称                       | 参数类型                                     | 描述                                       |
| ------------------------ | ---------------------------------------- | ---------------------------------------- |
| type                     | InputType                                | 设置输入框类型。<br/>默认值：InputType.Normal        |
| placeholderColor         | [ResourceColor](ts-types.md#resourcecolor8)     | 设置placeholder颜色。|
| placeholderFont          | [Font](ts-types.md#font) | 设置placeholder文本样式。 |
| enterKeyType             | EnterKeyType                             | 设置输入法回车键类型。<br/>默认值：EnterKeyType.Done    |
| caretColor               | [ResourceColor](ts-types.md#resourcecolor8)    | 设置输入框光标颜色。                               |
| maxLength                | number                                   | 设置文本的最大输入字符数。                            |
<<<<<<< Updated upstream
| inputFilter<sup>8+</sup>      | {<br/>value:&nbsp;[ResourceStr](ts-types.md#resourcestr),<br/>error?:&nbsp;(value:&nbsp;string)&nbsp;=&gt;&nbsp;void<br/>} | 正则表达式，满足表达式的输入允许显示，不满足正则表达式的输入被忽略。仅支持单个字符匹配，不支持字符串匹配。例如：^(?=.\*\d)(?=.\*[a-z])(?=.\*[A-Z]).{8,10}$，8到10位的强密码不支持过滤。<br/>-&nbsp;value：设置正则表达式。<br/>-&nbsp;error：正则匹配失败时，返回被忽略的内容。 |
=======
| inputFilter<sup>8+</sup>      | {<br/>value:&nbsp;[ResourceStr](ts-types.md#resourcestr8)<sup>8+</sup>,<br/>error?:&nbsp;(value:&nbsp;string)&nbsp;=&gt;&nbsp;void<br/>} | 正则表达式，满足表达式的输入允许显示，不满足正则表达式的输入被忽略。仅支持单个字符匹配，不支持字符串匹配。例如：^(?=.\*\d)(?=.\*[a-z])(?=.\*[A-Z]).{8,10}$，8到10位的强密码不支持过滤。<br/>-&nbsp;value：设置正则表达式。<br/>-&nbsp;error：正则匹配失败时，返回被忽略的内容。 |
>>>>>>> Stashed changes
| copyOption<sup>9+</sup> | [CopyOptions](ts-appendix-enums.md#copyoptions9) | 设置文本是否可复制。 |
| showPasswordIcon<sup>9+</sup> | boolean | 密码输入模式时，密码框末尾的图标是否显示。<br/>默认值：true |
| style<sup>9+</sup> | TextInputStyle | TextInput风格。<br/>默认值：TextInputStyle.Default |
| textAlign<sup>9+</sup>   | [TextAlign](ts-appendix-enums.md#textalign) | 设置文本水平对齐式。<br/>默认值：TextAlign.Start  |

## EnterKeyType枚举说明

| 名称                  | 描述        |
| ------------------- | --------- |
| Go     | 显示Go文本。   |
| Search | 显示为搜索样式。  |
| Send   | 显示为发送样式。  |
| Next   | 显示为下一个样式。 |
| Done   | 标准样式。     |

## InputType枚举说明

| 名称                 | 描述            |
| ------------------ | ------------- |
| Normal   | 基本输入模式。<br/>支持输入数字、字母、下划线、空格、特殊字符。 |
| Password | 密码输入模式。       |
| Email    | e-mail地址输入模式。 |
| Number   | 纯数字输入模式。      |
| PhoneNumber<sup>9+</sup> | 电话号码输入模式。<br/>支持输入数字、+ 、-、*、#，长度不限。 |

## TextInputStyle<sup>9+</sup>枚举说明

| 名称                 | 描述            |
| ------------------ | ------------- |
| Default   | 默认风格，光标宽1.5vp，光标高度和字体大小高度相关，字体越大光标越高。       |
| Inline | 内联输入风格。文字选中时底板与输入框同高。      |

## 事件

| 名称                                       | 功能描述                                     |
| ---------------------------------------- | ---------------------------------------- |
| onChange(callback:&nbsp;(value:&nbsp;string)&nbsp;=&gt;&nbsp;void) | 输入发生变化时，触发回调。              |
| onSubmit(callback:&nbsp;(enterKey:&nbsp;EnterKeyType)&nbsp;=&gt;&nbsp;void) | 回车键或者软键盘回车键触发该回调，参数为当前软键盘回车键类型。          |
| onEditChanged(callback:&nbsp;(isEditing:&nbsp;boolean)&nbsp;=&gt;&nbsp;void)<sup>(deprecated) </sup> | 输入状态变化时，触发回调。                            |
| onEditChange(callback:&nbsp;(isEditing:&nbsp;boolean)&nbsp;=&gt;&nbsp;void) <sup>8+</sup> | 输入状态变化时，触发回调。                            |
| onCopy<sup>8+</sup>(callback:(value:&nbsp;string)&nbsp;=&gt;&nbsp;void) | 长按输入框内部区域弹出剪贴板后，点击剪切板复制按钮，触发回调。<br/>value：复制的文本内容。 |
| onCut<sup>8+</sup>(callback:(value:&nbsp;string)&nbsp;=&gt;&nbsp;void) | 长按输入框内部区域弹出剪贴板后，点击剪切板剪切按钮，触发回调。<br/>value：剪切的文本内容。 |
| onPaste<sup>8+</sup>(callback:(value:&nbsp;string)&nbsp;=&gt;&nbsp;void) | 长按输入框内部区域弹出剪贴板后，点击剪切板粘贴按钮，触发回调。<br/>value：粘贴的文本内容。 |

## TextInputController<sup>8+</sup>

TextInput组件的控制器。

### 导入对象
```
controller: TextInputController = new TextInputController()
```
### caretPosition

caretPosition(value:&nbsp;number): void

设置输入光标的位置。

**参数：**

| 参数名 | 参数类型 | 必填 | 参数描述                               |
| ------ | -------- | ---- | -------------------------------------- |
| value  | number   | 是   | 从字符串开始到光标所在位置的字符长度。 |


## 示例


### 单行文本输入

```ts
// xxx.ets
@Entry
@Component
struct TextInputExample1 {
  @State text: string = ''

  build() {
    Column() {
      TextInput({ placeholder: 'input your word' })
        .placeholderColor("rgb(0,0,225)")
        .placeholderFont({ size: 30, weight: 100, family: 'cursive', style: FontStyle.Italic })
        .caretColor(Color.Blue)
        .height(50)
        .fontSize(30)
        .fontWeight(FontWeight.Bold)
        .fontFamily("sans-serif")
        .fontStyle(FontStyle.Normal)
        .fontColor(Color.Red)
        .onChange((value: string) => {
          this.text = value
        })
      Text(this.text).width('90%')
    }
  }
}
```


![zh-cn_image_0000001252769643](figures/zh-cn_image_0000001252769643.gif)


### 设置光标

```ts
// xxx.ets
@Entry
@Component
struct TextInputExample2 {
    @State text: string = ''
    controller: TextInputController = new TextInputController()
    build() {
        Column() {
            TextInput({ placeholder: 'Please input your words.', controller:this.controller})
            Button('caretPosition')
                .onClick(() => {
                this.controller.caretPosition(4)
            })
        }
    }
}
```

![zh-cn_image_0000001208256092](figures/zh-cn_image_0000001208256092.png)
