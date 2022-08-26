# Circle

圆形绘制组件。

>  **说明：**
>
>  该组件从API Version 7开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。


## 权限列表

无


## 子组件

无


## 接口

Circle(value?: {width: string&nbsp;|&nbsp;number, height: string&nbsp;|&nbsp;number})

**参数：**

| 参数名 | 参数类型                   | 必填 | 默认值 | 参数描述 |
| ------ | -------------------------- | ---- | ------ | -------- |
| width  | string&nbsp;\|&nbsp;number | 是   | -      | 宽度。   |
| height | string&nbsp;\|&nbsp;number | 是   | -      | 高度。   |

## 属性

| 参数名称 | 参数类型 | 默认值 | 必填 | 参数描述           |
| -------- | -------- | ------ | ---- | ------------------ |
| width    | Length   | 0      | 否   | 圆所在矩形的宽度。 |
| height   | Length   | 0      | 否   | 圆所在矩形的高度。 |


## 示例

```ts
// xxx.ets
@Entry
@Component
struct CircleExample {
  build() {
    Flex({ justifyContent: FlexAlign.SpaceAround }) {
      // 绘制一个直径为150的圆
      Circle({ width: 150, height: 150 })
      // 绘制一个直径为150的圆
      Circle().width(150).height(150)
    }.width('100%').margin({ top: 5 })
  }
}
```

![zh-cn_image_0000001219744191](figures/zh-cn_image_0000001219744191.png)
