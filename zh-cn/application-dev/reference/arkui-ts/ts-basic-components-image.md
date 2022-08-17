# Image

图片组件，支持本地图片和网络图片的渲染展示。

> **说明：**
> 该组件从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 权限说明

使用网络图片时，需要在config.json（FA模型）或者module.json5（Stage模型）对应的"abilities"中添加网络使用权限ohos.permission.INTERNET。

```
"abilities": [
  {
    ...
    "permissions": ["ohos.permission.INTERNET"],
    ...
  }
] 
```


## 子组件

无


## 接口

Image(src: string | PixelMap | Resource)

通过图片数据源获取图片，用于后续渲染展示。

**参数：** 

| 参数名  | 参数类型                                     | 必填   | 默认值  | 参数描述                                     |
| ---- | ---------------------------------------- | ---- | ---- | ---------------------------------------- |
| src  | string\|&nbsp;[PixelMap](../apis/js-apis-image.md#pixelmap7)\|&nbsp;[Resource](../../ui/ts-types.md#resource类型) | 是    | -    | 图片的数据源，支持本地图片和网络图片。<br/>当使用相对路径引用图片资源时，例如`Image("common/test.jpg")`，不支持该Image组件被跨包/跨模块调用，建议使用`$r`方式来管理需全局使用的图片资源。<br/>\- 支持的图片格式包括png、jpg、bmp、svg和gif。<br/>\- 支持`Base64`字符串。格式`data:image/[png\|jpeg\|bmp\|webp];base64,[base64 data]`, 其中`[base64 data]`为`Base64`字符串数据。<br/>\- 支持`dataability://`路径前缀的字符串，用于访问通过data&nbsp;ability提供的图片路径。 |

## 属性

除支持[通用属性](ts-universal-attributes-size.md)外，还支持以下属性：

| 名称                  | 参数类型                                                | 默认值                   | 描述                                                         |
| --------------------- | ------------------------------------------------------- | ------------------------ | ------------------------------------------------------------ |
| alt                   | string \| [Resource](../../ui/ts-types.md#resource类型) | -                        | 加载时显示的占位图，支持本地图片和网络图片。                 |
| objectFit             | [ImageFit](ts-appendix-enums.md#imagefit)                           | ImageFit.Cover           | 设置图片的缩放类型。                                         |
| objectRepeat          | [ImageRepeat](ts-appendix-enums.md#imagerepeat)         | NoRepeat                 | 设置图片的重复样式。<br/>> **说明：**<br/>>&nbsp;-&nbsp;svg类型图源不支持该属性。 |
| interpolation         | [ImageInterpolation](#imageinterpolation)               | ImageInterpolation.None  | 设置图片的插值效果，即减轻低清晰度图片在放大显示的时候出现的锯齿问题，仅针对图片放大插值。<br/>>&nbsp;**说明：**<br/>>&nbsp;-&nbsp;svg类型图源不支持该属性。<br/>>&nbsp;-&nbsp;PixelMap资源不支持该属性。 |
| renderMode            | [ImageRenderMode](#imagerendermode)                     | ImageRenderMode.Original | 设置图片渲染的模式。<br/>>&nbsp;**说明：**<br/>>&nbsp;-&nbsp;svg类型图源不支持该属性。 |
| sourceSize            | {<br/>width:&nbsp;number,<br/>height:&nbsp;number<br/>} | -                        | 设置图片裁剪尺寸，将原始图片解码成pixelMap，指定尺寸的图片，单位为px。<br/>>&nbsp;**说明：**<br/>>&nbsp;PixelMap资源不支持该属性。 |
| syncLoad<sup>8+</sup> | boolean                                  | false                    | 设置是否同步加载图片，默认是异步加载。同步加载时阻塞UI线程，不会显示占位图。  |
| copyOption<sup>9+</sup> | [CopyOptions](ts-appendix-enums.md#copyoptions9)  | CopyOptions.None | 设置图片是否可复制（SVG图片不支持复制）。 |

### ImageInterpolation

| 名称     | 描述                        |
| ------ | ------------------------- |
| None   | 不使用插值图片数据。                |
| High   | 插值图片数据的使用率高，可能会影响图片渲染的速度。 |
| Medium | 插值图片数据的使用率中。              |
| Low    | 插值图片数据的使用率低。              |

### ImageRenderMode

| 名称       | 描述                    |
| -------- | --------------------- |
| Original | 按照原图进行渲染，包括颜色。        |
| Template | 将图片渲染为模板图片，忽略图片的颜色信息。 |


## 事件

除支持[通用事件](ts-universal-events-click.md)外，还支持以下事件：

| 名称                                       | 功能描述                                     |
| ---------------------------------------- | ---------------------------------------- |
| onComplete(callback:&nbsp;(event?:&nbsp;{&nbsp;width:&nbsp;number,&nbsp;height:&nbsp;number,&nbsp;componentWidth:&nbsp;number,<br>&nbsp;componentHeight:&nbsp;number,&nbsp;loadingStatus:&nbsp;number&nbsp;})&nbsp;=&gt;&nbsp;void) | 图片成功加载时触发该回调，返回成功加载的图片尺寸。<br>- width：图片的宽，单位为像素。<br/>- height：图片的高，单位为像素。<br/>- componentWidth：组件的宽，单位为像素。<br/>- componentHeight：组件的高，单位为像素。<br/>- loadingStatus：图片加载成功的状态。<br/> |
| onError(callback:&nbsp;(event?:&nbsp;{&nbsp;componentWidth:&nbsp;number,&nbsp;componentHeight:&nbsp;number&nbsp;})&nbsp;=&gt;&nbsp;void) | 图片加载出现异常时触发该回调。<br>- componentWidth：组件的宽，单位为像素。<br/>- componentHeight：组件的高，单位为像素。<br/> |
| onFinish(callback:&nbsp;()&nbsp;=&gt;&nbsp;void) | 当加载的源文件为带动效的svg图片时，当svg动效播放完成时会触发这个回调，如果动效为无限循环动效，则不会触发这个回调。 |

## 示例

### 图片加载

加载显示不同类型的图片，并设置图片的缩放类型。

```ts
@Entry
@Component
struct ImageExample1 {
  private on: string = 'www.example.com' 
  @State src: string = this.on

  build() {
    Column() {
      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Start }) {
        Text('default').fontSize(16).fontColor(0xcccccc).height(30)
        Row({ space: 5 }) {
          Image($r('app.media.ic_png'))
            .width(110).height(110).border({ width: 1 }).borderStyle(BorderStyle.Dashed)
            .overlay('png', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
          Image($r('app.media.ic_gif'))
            .width(110).height(110).border({ width: 1 }).borderStyle(BorderStyle.Dashed)
            .overlay('gif', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
          Image($r('app.media.ic_svg'))
            .width(110).height(110).border({ width: 1 }).borderStyle(BorderStyle.Dashed)
            .overlay('svg', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
        }
        Row({ space: 5 }) {
          Image($r('app.media.img_example'))
            .width(110).height(110).border({ width: 1 }).borderStyle(BorderStyle.Dashed)
            .overlay('jpg', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
          Image(this.src)
            .width(110).height(110).border({ width: 1 }).borderStyle(BorderStyle.Dashed)
            .overlay('network', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
        }.margin({ top: 25, bottom: 10 })
      }

      Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Start }) {
        Text('objectFit').fontSize(16).fontColor(0xcccccc).height(30)
        Row({ space: 5 }) {
          Image($r('app.media.img_example'))
            .border({ width: 1 }).borderStyle(BorderStyle.Dashed)
            .objectFit(ImageFit.None).width(110).height(110)
            .overlay('None', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
          Image($r('app.media.img_example'))
            .border({ width: 1 }).borderStyle(BorderStyle.Dashed)
            .objectFit(ImageFit.Fill).width(110).height(110)
            .overlay('Fill', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
          Image($r('app.media.img_example'))
            .border({ width: 1 }).borderStyle(BorderStyle.Dashed)
            .objectFit(ImageFit.Cover).width(110).height(110)
            .overlay('Cover', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
        }
        Row({ space: 5 }) {
          Image($r('app.media.img_example_w250'))
            .border({ width: 1 }).borderStyle(BorderStyle.Dashed)
            .objectFit(ImageFit.Contain).width(110).height(110)
            .overlay('Contain', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
          Image($r('app.media.img_example_w250'))
            .border({ width: 1 }).borderStyle(BorderStyle.Dashed)
            .objectFit(ImageFit.ScaleDown).width(110).height(110)
            .overlay('ScaleDown', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
        }.margin({ top: 25 })
      }
    }.height(320).width(360).padding({ right: 10, top: 10 })
  }
}
```

![zh-cn_image_0000001250492613](figures/zh-cn_image_0000001250492613.gif)

### 设置属性

```ts
@Entry
@Component
struct ImageExample2 {

  build() {
    Column({ space: 10 }) {
      Text('renderMode').fontSize(12).fontColor(0xcccccc).width('96%').height(30)
      Row({ space: 50 }) {
        Image($r('app.media.img_example'))
          .renderMode(ImageRenderMode.Original).width(100).height(100)
          .border({ width: 1 }).borderStyle(BorderStyle.Dashed)
          .overlay('Original', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
        Image($r('app.media.img_example'))
          .renderMode(ImageRenderMode.Template).width(100).height(100)
          .border({ width: 1 }).borderStyle(BorderStyle.Dashed)
          .overlay('Template', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
      }
      
      Text('alt').fontSize(12).fontColor(0xcccccc).width('96%').height(30)
      Image('')
        .alt($r('app.media.Image_none'))
        .width(100).height(100).border({ width: 1 }).borderStyle(BorderStyle.Dashed)
        
      Text('sourceSize').fontSize(12).fontColor(0xcccccc).width('96%')
      Row({ space: 50 }) {
        Image($r('app.media.img_example'))
          .sourceSize({
            width: 150,
            height: 150
          })
          .objectFit(ImageFit.ScaleDown).width('25%').aspectRatio(1)
          .border({ width: 1 }).borderStyle(BorderStyle.Dashed)
          .overlay('w:150 h:150', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
        Image($r('app.media.img_example'))
          .sourceSize({
            width: 200,
            height: 200
          })
          .objectFit(ImageFit.ScaleDown).width('25%').aspectRatio(1)
          .border({ width: 1 }).borderStyle(BorderStyle.Dashed)
          .overlay('w:200 h:200', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
      }
      
      Text('objectRepeat').fontSize(12).fontColor(0xcccccc).width('96%').height(30)
      Row({ space: 5 }) {
        Image($r('app.media.ic_health_heart'))
          .width(120).height(125).border({ width: 1 }).borderStyle(BorderStyle.Dashed)
          .objectRepeat(ImageRepeat.XY).objectFit(ImageFit.ScaleDown)
          .overlay('ImageRepeat.XY', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
        Image($r('app.media.ic_health_heart'))
          .width(110).height(125).border({ width: 1 }).borderStyle(BorderStyle.Dashed)
          .objectRepeat(ImageRepeat.Y).objectFit(ImageFit.ScaleDown)
          .overlay('ImageRepeat.Y', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
        Image($r('app.media.ic_health_heart'))
          .width(110).height(125).border({ width: 1 }).borderStyle(BorderStyle.Dashed)
          .objectRepeat(ImageRepeat.X).objectFit(ImageFit.ScaleDown)
          .overlay('ImageRepeat.X', { align: Alignment.Bottom, offset: { x: 0, y: 20 } })
      }
    }.height(150).width('100%').padding({ right: 10 })
  }
}
```

![zh-cn_image_0000001205812616](figures/zh-cn_image_0000001205812616.png)

### 事件调用

```ts
@Entry
@Component
struct ImageExample3 {
  @State widthValue: number = 0
  @State heightValue: number = 0
  private on: Resource = $r('app.media.image_on')
  private off: Resource = $r('app.media.image_off')
  private on2off: Resource = $r('app.media.image_on2off')
  private off2on: Resource = $r('app.media.image_off2on')
  @State src: Resource = this.on

  build() {
    Column() {
      Row({ space: 20 }) {
        Column() {
          Image($r('app.media.img_example1'))
            .alt($r('app.media.ic_public_picture'))
            .sourceSize({
              width: 900,
              height: 900
            })
            .objectFit(ImageFit.Cover)
            .height(180).width(180)
            // 图片加载完成后，获取图片尺寸。
            .onComplete((msg: { width: number,height: number }) => {
              this.widthValue = msg.width
              this.heightValue = msg.height
            })
            .onError(() => {
              console.log('load image fail')
            })
            .overlay('\nwidth: ' + String(this.width) + ' height: ' + String(this.height), {
              align: Alignment.Bottom,
              offset: { x: 0, y: 20 }
            })
        }
        // 为图片添加点击事件，点击完成后加载特定图片。
        Image(this.src)
          .width(120).height(120)
          .onClick(() => {
            if (this.src == this.on || this.src == this.off2on) {
              this.src = this.on2off
            } else {
              this.src = this.off2on
            }
          })
          .onFinish(() => {
            if (this.src == this.off2on) {
              this.src = this.on
            } else {
              this.src = this.off
            }
          })
      }
    }.width('100%')
  }
}
```

![zh-cn_image_0000001205972610](figures/zh-cn_image_0000001205972610.gif)
