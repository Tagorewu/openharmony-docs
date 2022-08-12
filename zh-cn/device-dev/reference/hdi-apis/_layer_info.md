# LayerInfo


## **概述**

**所属模块:**

[Display](_display.md)


## **汇总**


### Public 属性

  | Public&nbsp;属性 | 描述 | 
| -------- | -------- |
| [width](_display.md#width-27) | 图层宽度 | 
| [height](_display.md#height-27) | 图层高度 | 
| [type](_display.md#type-13) | 图层类型，包括图形层、视频层和媒体播放模式。 | 
| [bpp](_display.md#bpp) | 每像素所占bit数 | 
| [pixFormat](_display.md#pixformat-12) | 图层像素格式 | 


## **详细描述**

定义图层信息结构体。

在创建图层时，需要将LayerInfo传递给创建图层接口，创建图层接口根据图层信息创建相应图层。