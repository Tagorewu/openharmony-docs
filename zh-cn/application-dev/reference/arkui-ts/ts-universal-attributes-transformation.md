# 图形变换

用于对组件进行旋转、平移、缩放、矩阵变换等操作。

> **说明：**
>
> 从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。

## 属性


| 名称        | 参数类型                                                           | 描述                                       |
| --------- | ------------------------------------------------------------------------ | ---------------------------------------- |
| rotate    | {<br/>x?:&nbsp;number,<br/>y?:&nbsp;number,<br/>z?:&nbsp;number,<br/>angle?:&nbsp;Angle,<br/>centerX?:&nbsp;number \| string,<br/>centerY?:&nbsp;number \| string<br/>} | (x,&nbsp;y,&nbsp;z)指定一个矢量，表示旋转轴，正角度为顺时针转动，负角度为逆时针转动，默认值为0，同时可以通过centerX和centerY设置旋转的中心点。<br>默认值:<br>{<br/>x:&nbsp;0,<br/>y:&nbsp;0,<br/>z:&nbsp;0,<br/>angle:&nbsp;0,<br/>centerX:&nbsp;'50%',<br/>centerY:&nbsp;'50%'<br/>} |
| translate | {<br/>x?:&nbsp;number \| string,<br/>y?:&nbsp;number \| string,<br/>z?&nbsp;:&nbsp;number \| string<br/>}  | 可以分别设置X轴、Y轴、Z轴的平移距离，距离的正负控制平移的方向。不支持百分比形式的输入。<br>默认值:<br>{<br/>x:&nbsp;0,<br/>y:&nbsp;0,<br/>z:&nbsp;0<br/>}|
| scale     | {<br/>x?:&nbsp;number,<br/>y?:&nbsp;number,<br/>z?:&nbsp;number,<br/>centerX?:&nbsp;number \| string,<br/>centerY?:&nbsp;number \| string<br/>} | 可以分别设置X轴、Y轴、Z轴的缩放比例，默认值为1，同时可以通过centerX和centerY设置缩放的中心点。<br>默认值:<br>{<br/>x:&nbsp;1,<br/>y:&nbsp;1,<br/>z:&nbsp;1,<br/>centerX:'50%',<br/>centerY:'50%'<br/>} |
| transform | Matrix4Transit                                                 | 设置当前组件的变换矩阵。                             |


## 示例

```ts
// xxx.ets
import Matrix4 from '@ohos.matrix4'

@Entry
@Component
struct TransformExample {
  build() {
    Column() {
      Text('rotate').width('90%').fontColor(0xCCCCCC).padding(15).fontSize(30)
      Row()
        .rotate({
          x: 1,
          y: 1,
          z: 1,
          centerX: '50%',
          centerY: '50%',
          angle: 300
        }) // 组件以(1,1,1)为旋转轴，中心点顺时针旋转 300度
        .width(100).height(100).backgroundColor(0xAFEEEE)

      Text('translate').width('90%').fontColor(0xCCCCCC).padding(10).fontSize(30)
      Row()
        .translate({ x: 100, y: 5 }) // x轴平移100，y轴平移5
        .width(100).height(100).backgroundColor(0xAFEEEE).margin({bottom:10})

      Text('scale').width('90%').fontColor(0xCCCCCC).padding(15).fontSize(30)
      Row()
        .scale({ x: 2, y: 0.5 }) // 高度缩小一倍，宽度放大一倍，z轴在2D下无效果
        .width(100).height(100).backgroundColor(0xAFEEEE)

      Text('Matrix4').width('90%').fontColor(0xCCCCCC).padding(15).fontSize(30)
      Row()
        .width(100).height(100).backgroundColor(0xAFEEEE)
        .transform(Matrix4.identity().translate({ x: 100, y: 100, z: 30 }))
    }.width('100%').margin({ top: 5 })
  }
}
```

![zh-cn_image_0000001219864137](figures/zh-cn_image_0000001219864137.png)
