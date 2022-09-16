# LongPressGesture

>  **说明：**
>
>  从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 接口

LongPressGesture(options?: { fingers?: number, repeat?: boolean, duration?: number })

**参数：**

| 参数名称 | 参数类型 | 必填 | 参数描述                                                     |
| -------- | -------- | ---- | ------------------------------------------------------------ |
| fingers  | number   | 否   | 触发长按的最少手指数，最小取值为1指，&nbsp;最大取值为10指。<br/>默认值：1 |
| repeat   | boolean  | 否   | 是否连续触发事件回调。<br/>默认值：false                     |
| duration | number   | 否   | 触发长按的最小时间，单位为毫秒（ms）。<br/>默认值：500       |

## 事件

| 名称                                       | 功能描述                           |
| ---------------------------------------- | ------------------------------ |
| onAction((event?:&nbsp;GestureEvent)&nbsp;=&gt;&nbsp;void) | LongPress手势识别成功回调。             |
| onActionEnd((event?:&nbsp;GestureEvent)&nbsp;=&gt;&nbsp;void) | LongPress手势识别成功，手指抬起后触发回调。     |
| onActionCancel(event:&nbsp;()&nbsp;=&gt;&nbsp;void) | LongPress手势识别成功，接收到触摸取消事件触发回调。 |

## GestureEvent对象中与LongPress手势相关的属性

| 属性名称   | 属性类型    | 描述           |
| ------ | ------- | ------------ |
| repeat | boolean | 事件是否为重复触发事件。 |

## 示例

```ts
// xxx.ets
@Entry
@Component
struct LongPressGestureExample {
  @State count: number = 0

  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.SpaceBetween }) {
      Text('LongPress onAction:' + this.count)
    }
    .height(200).width(300).padding(60).border({ width:1 }).margin(30)
    .gesture(
      LongPressGesture({ repeat: true })
        //长按动作存在会连续触发
        .onAction((event: GestureEvent) => {
          if (event.repeat) { this.count++ }
        })
        //长按动作一结束触发
        .onActionEnd(() => {
          this.count = 0
        })
    )
  }
}
```

![zh-cn_image_0000001174264380](figures/zh-cn_image_0000001174264380.gif)
