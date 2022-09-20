# ImageAnimator

提供帧动画组件来实现逐帧播放图片的能力，可以配置需要播放的图片列表，每张图片可以配置时长。

>  **说明：**
>
>  该组件从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 权限列表

无


## 子组件

无


## 接口

ImageAnimator()


## 属性

| 参数名称   | 参数类型                                                     | 默认值   | 必填 | 参数描述                                                     |
| ---------- | ------------------------------------------------------------ | -------- | ---- | ------------------------------------------------------------ |
| images     | Array&lt;{<br/>src: string,<br/>width?: number \| string,<br/>height?: number \| string,<br/>top?: number \| string,<br/>left?: number \| string,<br/>duration?: number<br/>}&gt; | []       | 是   | 设置图片帧信息集合。每一帧的帧信息包含图片路径、图片大小、图片位置和图片播放时长信息。详细说明：<br/>- src：图片路径，图片格式为svg，png和jpg。<br/>- width：图片宽度。<br/>- height：图片高度。<br/>- top：图片相对于组件左上角的纵向坐标。<br/>- left：图片相对于组件左上角的横向坐标。<br/>- duration：每一帧图片的播放时长，单位毫秒。 |
| state      | [AnimationStatus](ts-appendix-enums.md#animationstatus)      | Initial  | 否   | 默认为初始状态，用于控制播放状态。                           |
| duration   | number                                                       | 1000     | 否   | 单位为毫秒，默认时长为1000ms。<br/>duration为0时，不播放图片。<br/>值的改变只会在下一次循环开始时生效。<br/>当images中设置了单独的duration后，该属性设置无效。 |
| reverse    | boolean                                                      | false    | 否   | 设置播放顺序。false表示从第1张图片播放到最后1张图片；&nbsp;true表示从最后1张图片播放到第1张图片。 |
| fixedSize  | boolean                                                      | true     | 否   | 设置图片大小是否固定为组件大小。&nbsp;true表示图片大小与组件大小一致，此时设置图片的width&nbsp;、height&nbsp;、top&nbsp;和left属性是无效的。false表示每一张图片的&nbsp;width&nbsp;、height&nbsp;、top和left属性都要单独设置。 |
| preDecode  | number                                                       | 0        | 否   | 是否启用预解码，默认值为0，即不启用预解码，如该值设为2，则播放当前页时会提前加载后面两张图片至缓存以提升性能。 |
| fillMode   | [FillMode](ts-appendix-enums.md#fillmode)                    | Forwards | 否   | 设置动画开始前和结束后的状态，可选值参见FillMode说明。       |
| iterations | number                                                       | 1        | 否   | 默认播放一次，设置为-1时表示无限次播放。                     |

## 事件

| 名称                              | 功能描述            |
| ------------------------------- | --------------- |
| onStart(event:&nbsp;()&nbsp;=&gt;&nbsp;void)  | 状态回调，动画开始播放时触发。 |
| onPause(event:&nbsp;()&nbsp;=&gt;&nbsp;void)  | 状态回调，动画暂停播放时触发。 |
| onRepeat(event:&nbsp;()&nbsp;=&gt;&nbsp;void) | 状态回调，动画重新播放时触发。 |
| onCancel(event:&nbsp;()&nbsp;=&gt;&nbsp;void) | 状态回调，动画取消播放时触发。 |
| onFinish(event:&nbsp;()&nbsp;=&gt;&nbsp;void) | 状态回调，动画播放完成时触发。 |


## 示例

```ts
// xxx.ets
@Entry
@Component
struct ImageAnimatorExample {
  @State state: AnimationStatus = AnimationStatus.Initial
  @State reverse: boolean = false
  @State iterations: number = 1

  build() {
    Column({ space:5 }) {
      ImageAnimator()
        .images([
          { 
            //comment文件夹与pages同级
            src: '/comment/bg1.jpg',
            duration: 500,
            width: 325,
            height: 200,
            top: 0,
            left: 0
          },
          {
            src: '/comment/bg2.jpg',
            duration: 500,
            width: 325,
            height: 200,
            top: 0,
            left: 0
          },
          {
            src: '/comment/bg3.jpg',
            duration: 500,
            width: 325,
            height: 200,
            top: 0,
            left: 0
          },
          {
            src: '/comment/bg4.jpg',
            duration: 500,
            width: 325,
            height: 200,
            top: 0,
            left: 0
          }
        ])
        .state(this.state).reverse(this.reverse).fixedSize(false).preDecode(2)
        .fillMode(FillMode.None).iterations(this.iterations).width(325).height(210)
        .margin({top:100})
        .onStart(() => { // 当帧动画开始播放后触发
          console.info('Start')
        })
        .onPause(() => {
          console.info('Pause')
        })
        .onRepeat(() => {
          console.info('Repeat')
        })
        .onCancel(() => {
          console.info('Cancel')
        })
        .onFinish(() => { // 当帧动画播放完成后触发
          console.info('Finish')
        })
      Row() {
        Button('start').width(100).padding(5).onClick(() => {
          this.state = AnimationStatus.Running
        })
        Button('pause').width(100).padding(5).onClick(() => {
          this.state = AnimationStatus.Paused
        })
        Button('stop').width(100).padding(5).onClick(() => {
          this.state = AnimationStatus.Stopped
        })
      }
      Row() {
        Button('reverse').width(100).padding(5).onClick(() => {
          this.reverse = !this.reverse
        })
        Button('once').width(100).padding(5).onClick(() => {
          this.iterations = 1
        })
        Button('iteration').width(100).padding(5).onClick(() => {
          this.iterations = -1
        })
      }
    }.width('100%').height('100%').backgroundColor(0xF1F3F5)
  }
}
```

![zh-cn_image_0000001219662643](figures/zh-cn_image_0000001219662643.gif)
