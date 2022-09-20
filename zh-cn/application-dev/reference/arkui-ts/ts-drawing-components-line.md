# Line

直线绘制组件。

>  **说明：**
>
>  该组件从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 权限列表

无


## 子组件

无


## 接口

Line(options?: {width?: string | number, height?: string | number})

- 参数
  | 参数名 | 参数类型 | 必填 | 默认值 | 参数描述 | 
  | -------- | -------- | -------- | -------- | -------- |
  | width | string \| number | 否 | 0 | 宽度。 | 
  | height | string \| number | 否 | 0 | 高度。 | 


## 属性

除支持[通用属性](ts-universal-attributes-size.md)外，还支持以下属性：

| 参数名称 | 参数类型 | 默认值 | 必填 | 参数描述 | 
| -------- | -------- | -------- | -------- | -------- |
| startPoint | Array | [0,&nbsp;0] | 是   | 直线起点坐标点(相对坐标)。 |
| endPoint   | Array | [0,&nbsp;0] | 是   | 直线终点坐标点(相对坐标)。 |
| fill | [ResourceColor](../../ui/ts-types.md) | Color.Black | 否 | 设置填充区域颜色。 |
| fillOpacity | number&nbsp;\|&nbsp;string&nbsp;\|&nbsp;[Resource](../../ui/ts-types.md#resource类型) | 1 | 否 | 设置填充区域透明度。 |
| stroke | [ResourceColor](../../ui/ts-types.md) | Color.Black | 否 | 设置线条颜色。 |
| strokeDashArray | Array&lt;Length&gt; | [] | 否 | 设置线条间隙。 |
| strokeDashOffset | number&nbsp;\|&nbsp;string | 0 | 否 | 线条绘制起点的偏移量。 |
| strokeLineCap | [LineCapStyle](ts-appendix-enums.md#linecapstyle) | LineCapStyle.Butt | 否 | 设置线条端点绘制样式。 |
| strokeLineJoin | [LineJoinStyle](ts-appendix-enums.md#linejoinstyle) | LineJoinStyle.Miter | 否 | 设置线条拐角绘制样式。 |
| strokeMiterLimit | number&nbsp;\|&nbsp;string | 4 | 否 | 设置锐角绘制成斜角的极限值。 |
| strokeOpacity | number&nbsp;\|&nbsp;string&nbsp;\|&nbsp;[Resource](../../ui/ts-types.md#resource类型) | 1 | 否 | 设置线条透明度。 |
| strokeWidth | Length | 1 | 否 | 设置线条宽度。 |
| antiAlias | boolean | true | 否 | 是否开启抗锯齿效果。 |


## 示例

```ts
// xxx.ets
@Entry
@Component
struct LineExample {
  build() {
    Column() {
      Line({ width: 50, height: 100 }).startPoint([0, 0]).endPoint([50, 100])
      Line().width(200).height(200).startPoint([50, 50]).endPoint([150, 150])
    }.margin({ top: 5 })
  }
}
```

![zh-cn_image_0000001219982725](figures/zh-cn_image_0000001219982725.jpg)
