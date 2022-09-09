# 鼠标事件

>  **说明：**
>
>  从API Version 8开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 事件

| 名称                                                         | 支持冒泡 | 描述                                                         |
| ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
| onHover(event:&nbsp;(isHover:&nbsp;boolean)&nbsp;=&gt;&nbsp;void) | 否       | 鼠标进入或退出组件时触发该回调。<br/>isHover：表示鼠标是否悬浮在组件上，鼠标进入时为true,&nbsp;退出时为false。 |
| onMouse(event:&nbsp;(event?:&nbsp;MouseEvent)&nbsp;=&gt;&nbsp;void) | 是       | 当前组件被鼠标按键点击时或者鼠标在组件上移动时，触发该回调，event参数包含触发事件时的时间戳、鼠标按键、动作、点击触点在整个屏幕上的坐标和点击触点相对于当前组件的坐标。 |


## MouseEvent对象说明
| 属性名称      | 属性类型                            | 描述                   |
| --------- | ------------------------------- | -------------------- |
| timestamp | number                          | 触发事件时的时间戳。           |
| screenX   | number                          | 点击触点相对于屏幕左上角的x轴坐标。   |
| screenY   | number                          | 点击触点相对于屏幕左上角的y轴坐标。   |
| x         | number                          | 点击触点相对于当前组件左上角的x轴坐标。 |
| y         | number                          | 点击触点相对于当前组件左上角的y轴坐标。 |
| button    | [MouseButton](ts-appendix-enums.md#mousebutton) | 鼠标按键。                |
| action    | [MouseAction](ts-appendix-enums.md#mouseaction) | 事件动作。                |

## 示例

```ts
// xxx.ets
@Entry
@Component
struct MouseEventExample {
  @State hoverText: string = 'no hover'
  @State mouseText: string = 'MouseText'
  @State color: Color = Color.Blue

  build() {
    Column({ space:20 }) {
      Button(this.hoverText)
        .onHover((isHover: boolean) => {
          if (isHover) {
            this.hoverText = 'on hover'
            this.color = Color.Pink
          } else {
            this.hoverText = 'no hover'
            this.color = Color.Blue
          }
        })
        .backgroundColor(this.color)
      Button('onMouse')
        .onMouse((event: MouseEvent) => {
          console.log(this.mouseText = 'onMouse:\nButton = ' + event.button + 
          '\nAction = ' + event.action + '\nlocalXY=(' + event.x + ',' + event.y + ')' + 
          '\nscreenXY=(' + event.screenX + ',' + event.screenY + ')')
        })
      Text(this.mouseText)
    }.padding({ top: 20 }).width('100%')
  }
}
```
