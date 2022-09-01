# AlphabetIndexer

字母索引条。

>  **说明：**
>
>  该组件从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。

## 权限列表

无


## 子组件

无


## 接口

AlphabetIndexer(value: {arrayValue: Array&lt;string&gt;, selected: number})

**参数：**

| 参数名        | 参数类型                | 必填   | 默认值  | 参数描述       |
| ---------- | ------------------- | ---- | ---- | ---------- |
| arrayValue | Array&lt;string&gt; | 是    | -    | 字母索引字符串数组。 |
| selected   | number              | 是    | -    | 初始选中项索引值。     |

## 属性

| 名称                      | 参数类型                                     | 描述                                  |
| ----------------------- | ---------------------------------------- | ----------------------------------- |
| color                   | [ResourceColor](ts-types.md#resourcecolor8) | 设置文字颜色。                           |
| selectedColor           | [ResourceColor](ts-types.md#resourcecolor8) | 设置选中项文字颜色。                           |
| popupColor              | [ResourceColor](ts-types.md#resourcecolor8) | 设置提示弹窗文字颜色。                         |
| selectedBackgroundColor | [ResourceColor](ts-types.md#resourcecolor8) | 设置选中项背景颜色。                           |
| popupBackground         | [ResourceColor](ts-types.md#resourcecolor8) | 设置提示弹窗背景色。                            |
| usingPopup              | boolean                                  | 设置是否使用提示弹窗。                         |
| selectedFont            | [Font](ts-types.md#font) | 设置选中项文字样式。                           |
| popupFont               | [Font](ts-types.md#font) | 设置提示弹窗字体样式。                         |
| font                    | [Font](ts-types.md#font) | 设置字母索引条默认字体样式。                      |
| itemSize                | string \| number                    | 设置字母索引条字母区域大小，字母区域为正方形，即正方形边长。       |
| alignStyle              | IndexerAlign                             | 设置字母索引条弹框的对齐样式，支持弹窗显示在索引条右侧和左侧。<br/>默认值：IndexerAlign.Right |
| selected | number | 设置选中项索引值。 |
| popupPosition | {<br/>x?:[Length](ts-types.md#length)<br/>y?:[Length](ts-types.md#length)<br/>} | 设置弹出窗口相对于索引器条上边框中点的位置。 |

## IndexerAlign枚举说明

| 名称    | 描述          |
| ----- | ----------- |
| Left  | 弹框显示在索引条右侧。 |
| Right | 弹框显示在索引条左侧。 |

## 事件

| 名称                                       | 功能描述                                     |
| ---------------------------------------- | ---------------------------------------- |
| onSelected(callback:&nbsp;(index:&nbsp;number)&nbsp;=&gt;&nbsp;void)<sup>(deprecated)</sup> | 索引条选中回调,返回值为当前选中索引。                                 |
| onSelect(callback:&nbsp;(index:&nbsp;number)&nbsp;=&gt;&nbsp;void)<sup>8+</sup> | 索引条选中回调,返回值为当前选中索引。                                 |
| onRequestPopupData(callback:&nbsp;(index:&nbsp;number)&nbsp;=&gt;&nbsp;Array&lt;string&gt;)<sup>8+</sup> | 选中字母索引后，请求索引提示弹窗显示内容回调。<br/>返回值：索引对应的字符串数组，此字符串数组在弹窗中竖排显示，字符串列表最多显示5个，超出部分可以滑动显示。 |
| onPopupSelect(callback:&nbsp;(index:&nbsp;number)&nbsp;=&gt;&nbsp;void)<sup>8+</sup> | 字母索引提示弹窗字符串列表选中回调。                            |


## 示例

```ts
// xxx.ets
@Entry
@Component
struct AlphabetIndexerSample {
  private value: string[] = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']

  build() {
    AlphabetIndexer({ arrayValue: this.value, selected: 0 })
      .selectedColor(0xffffff) // 选中颜色
      .popupColor(0xFFFAF0) // 弹出框颜色
      .selectedBackgroundColor(0xCCCCCC) // 选中背景颜色
      .popupBackground(0xD2B48C) // 弹出框背景颜色
      .usingPopup(true) // 是否显示弹出框
      .selectedFont({ size: 16, weight: FontWeight.Bolder }) // 选中的样式
      .popupFont({ size: 30, weight: FontWeight.Bolder }) // 弹出框的演示
      .itemSize(28) // 每一项的大小正方形
      .alignStyle(IndexerAlign.Left) // 左对齐
      .onSelect((index: number) => {
        console.info(this.value[index] + '被选中了') // 选中的事件
      })
      .margin({ left: 50 })
  }
}
```

![zh-cn_image_0000001174422922](figures/zh-cn_image_0000001174422922.gif)
