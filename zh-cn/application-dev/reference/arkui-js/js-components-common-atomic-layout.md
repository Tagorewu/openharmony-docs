# 原子布局

>  **说明：**
> 从API version 5开始支持。后续版本如有新增内容，则采用上角标单独标记该内容的起始版本。

在屏幕形态和规格不同等情况下，布局效果需要实现自适应，因此系统提供了面向不同屏幕尺寸界面自适应适配的布局能力，称为原子布局。设计师可以考虑使用原子能力，定义元素在不同形态的尺寸界面上体现的自适应规则。开发者可以使用原子布局能力，快速实现让应用在多形态屏幕上有与设计效果相匹配的自适应效果。


## 隐藏能力

在非折行flex布局基础上，增加了显示优先级标记，可以调整组件内元素水平/垂直方向的显示优先级，根据当前组件容器的可用空间来显示内容。

| 样式 | 类型 | 说明 |
| -------- | -------- | -------- |
| display-index | number | 适用于div等支持flex布局的容器组件中的子组件，当容器组件在flex主轴上尺寸不足以显示全部内容时，按照display-index值从小到大的顺序进行隐藏，具有相同display-index值的组件同时隐藏。<br/>默认值：0（表示不隐藏） |


## 占比能力

在非折行的flex布局中，定义了占比能力的组件，保证指定组件始终在容器的某一个比例空间中进行布局。

| 样式 | 类型 | 说明 |
| -------- | -------- | -------- |
| flex-weight | number | 指明当前元素在flex主轴方向上尺寸权值。如果容器组件中所有节点均设置此属性，当前元素尺寸为：&nbsp;容器主轴尺寸&nbsp;\*&nbsp;当前权值&nbsp;/&nbsp;所有子元素权值和。如果容器组件中某几个节点设置此属性，则容器会对其他未设置此属性的节点进行布局，再将剩余空间分配给设置了此属性的节点，如果未设置此属性的节点设置了超过父元素的宽度，那么将没有剩余空间分配给设置了此属性的节点。设置了此属性的节点的尺寸为：容器剩余空间&nbsp;\*&nbsp;该元素权值&nbsp;/&nbsp;所有子元素权值和。 |


## 固定比例

定义了组件固定比例调整尺寸的能力。

| 样式 | 类型 | 说明 |
| -------- | -------- | -------- |
| aspect-ratio | number | 1.&nbsp;接受任意大于0的浮点值，定义为该节点的宽度与高度比，设置该属性后，该元素尺寸宽高比按照此属性值进行调整。<br/>2.&nbsp;遵守最大值与最小值的限制。<br/>3.&nbsp;在flex布局中，主轴尺寸先进行调整，后根据该尺寸调整交叉轴。 |
