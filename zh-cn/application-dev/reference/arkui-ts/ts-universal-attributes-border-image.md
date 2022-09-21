# 图片边框设置

设置组件图片边框样式。

>  **说明：**
>
>  从API Version 9开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。

## 属性

| 名称         | 参数类型                                     | 描述                                      |
| ---------- | ---------------------------------------- | --------------------------------------- |
| source     | string \| [Resource](ts-types.md#resource) \| [linearGradient](ts-universal-attributes-gradient-color.md) | 边框图源或者渐变色设置。                            |
| slice      | [Length](ts-types.md#length)\| EdgeWidth | 设置图片边框切割宽度。<br/>默认值：0                   |
| width      | [Length](ts-types.md#length)\| EdgeWidth | 设置图片边框宽度。<br/>默认值：0                     |
| outset     | [Length](ts-types.md#length)\| EdgeWidth | 设置边框图片向外延伸距离。<br/>默认值：0                 |
| RepeatMode | RepeatMode                               | 设置边框图片的重复方式。<br/>默认值：RepeatMode.Stretch |
| fill       | boolean                                  | 设置边框图片中心填充。<br/>默认值：false               |

## EdgeWidth枚举说明  

引用该对象时，至少传入一个参数。

| 名称     | 参数类型                         | 必填   | 描述      |
| ------ | ---------------------------- | ---- | ------- |
| left   | [Length](ts-types.md#length) | 否    | 左侧距离参数。 |
| right  | [Length](ts-types.md#length) | 否    | 右侧距离参数。 |
| top    | [Length](ts-types.md#length) | 否    | 上侧距离参数。 |
| bottom | [Length](ts-types.md#length) | 否    | 下侧距离参数。 |

## RepeatMode枚举说明

| 名称      | 描述                                  |
| ------- | ----------------------------------- |
| Repeat  | 被切割图片重复铺平在图片边框上，超出的部分会被剪裁。          |
| Stretch | 被切割图片以拉伸填充的方式铺满图片边框。                |
| Round   | 被切割图片以整数次平铺在图片边框上，无法以整数次平铺时压缩被切割图片。 |
| Space   | 被切割图片以整数次平铺在图片边框上，无法以整数次平铺时以空白填充。   |


## 示例

```ts
// xxx.ets
@Entry
@Component
struct Index {

  build() {
    Row() {
      Column() {
        Text('This is\nborderImage.').textAlign(TextAlign.Center)
          .borderImage({
            source: "borderOrigin.png",
            slice: {top:"31%", bottom:"31%", left:"31%", right:"31%"},
            width: {top:"20px", bottom:"20px", left:"20px", right:"20px"},
            outset: {top:"5px", bottom:"5px", left:"5px", right:"5px"},
            repeat: RepeatMode.Repeat,
            fill: false
          });
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

![zh-cn_image_borderImage](figures/borderImage.png)


```ts
// xxx.ets
@Entry
@Component
struct Index {

  build() {
    Row() {
      Column() {
        Text('This is\ngradient color.').textAlign(TextAlign.Center)
          .borderImage({
            source: {angle:90,
              direction: GradientDirection.Left,
              colors: [[0xAEE1E1, 0.0], [0xD3E0DC, 0.3], [0xFCD1D1, 1.0]]},
            slice: {top:10, bottom:10, left:10, right:10},
            width: {top:"10px", bottom:"10px", left: "10px", right:"10px"},
            repeat: RepeatMode.Stretch,
            fill: false
          });
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

![zh-cn_image_borderImageGradient](figures/borderImageGradient.png)
