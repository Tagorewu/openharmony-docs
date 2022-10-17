# 动画

本模块提供组件动画效果，包括定义动画、启动动画和以相反的顺序播放动画等。

> **说明：**
>
> 本模块首批接口从API version 6开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。


## 导入模块

```js
import animator from '@ohos.animator';
```
## create<sup>9+</sup>

create(options: AnimatorOptions): AnimatorResult

定义Animator类。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名     | 类型                                  | 必填   | 说明      |
| ------- | ----------------------------------- | ---- | ------- |
| options | [AnimatorOptions](#animatoroptions) | 是    | 定义动画选项。 |

**返回值：** 
| 类型                                | 说明            |
| --------------------------------- | ------------- |
| [AnimatorResult](#animatorresult) | Animator结果接口。 |

**示例：** 

  ```js
  var options = {
    duration: 1500,
    easing: 'friction',
    delay: 0,
    fill: 'forwards',
    direction: "normal",
    iterations: 3,
    begin: 200.0,
    end: 400.0,
  };
  animator.create(options);
  ```

## AnimatorResult

定义Animator结果接口。

<span id = "#resetsup9sup"></span>

### reset<sup>9+</sup>

reset(options: AnimatorOptions): void

更新当前动画器。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名     | 类型                                  | 必填   | 说明      |
| ------- | ----------------------------------- | ---- | ------- |
| options | [AnimatorOptions](#animatoroptions) | 是    | 定义动画选项。 |

**错误码：**

以下错误码的详细介绍请参见[ohos.animator(动画)](../errorcodes/errorcode-animator.md)错误码。

| 错误码ID   | 错误码信息 |
| --------- | ------- |
| 100001    | Internal error. |


**示例：**

```js
var options = {
  duration: 1500,
  easing: 'friction',
  delay: 0,
  fill: 'forwards',
  direction: "normal",
  iterations: 3,
  begin: 200.0,
  end: 400.0,
};
try {
  animator.reset(options);
} catch(error) {
  console.error(`Animator reset failed, error code: ${error.code}, message: ${error.message}.`);
}
```

### play

play(): void

启动动画。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**示例：**

```js
animator.play();
```

### finish

finish(): void

结束动画。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**示例：**

```js
animator.finish();
```

### pause

pause(): void

暂停动画。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**示例：**

```js
animator.pause();
```

### cancel

cancel(): void

删除动画。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**示例：**

```js
animator.cancel();
```

### reverse

reverse(): void

以相反的顺序播放动画。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**示例：**

```js
animator.reverse();
```

### onframe

onframe: (progress: number) => void

接收到帧时回调。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名      | 类型     | 必填   | 说明       |
| -------- | ------ | ---- | -------- |
| progress | number | 是    | 动画的当前进度。 |

**示例：**

```js
animator.onframe();
```

### onfinish

onfinish: () => void

动画完成时回调。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**示例：**

```js
animator.onfinish();
```

### oncancel

oncancel: () => void
不再维护
动画被取消时回调。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**示例：**

```js
animator.oncancel();
```

### onrepeat

onrepeat: () => void

动画重复时回调。

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**示例：**

```js
animator.onrepeat();
```



## AnimatorOptions

定义动画选项。

**系统能力：** SystemCapability.ArkUI.ArkUI.Full

| 名称         | 参数类型                                     | 必填   | 说明                                       |
| ---------- | ---------------------------------------- | ---- | ---------------------------------------- |
| duration   | number                                   | 是    | 动画播放的时长，单位毫秒，默认为0。                       |
| easing     | string                                   | 是    | 动画插值曲线，默认为'ease'。                        |
| delay      | number                                   | 是    | 动画延时播放时长，单位毫秒，默认为0，即不延时。                 |
| fill       | "none" \| "forwards" \| "backwards" \| "both" | 是    | 动画执行后是否恢复到初始状态，默认值为"none"。动画执行后，动画结束时的状态（在最后一个关键帧中定义）将保留。 |
| direction  | "normal" \| "reverse" \| "alternate" \| "alternate-reverse" | 是    | 动画播放模式，默认值"normal"。                      |
| iterations | number                                   | 是    | 动画播放次数，默认值1。设置为0时不播放，设置为-1时无限次播放。        |
| begin      | number                                   | 是    | 动画插值起点，默认为0。                             |
| end        | number                                   | 是    | 动画插值终点，默认为1。                             |


## 完整示例

```html
<!-- hml -->
<div class="container">
  <div class="Animation" style="height: {{divHeight}}px; width: {{divWidth}}px; background-color: red;" onclick="Show">
  </div>
</div>
```

```js
export default {
  data: {
    divWidth: 200,
    divHeight: 200,
    animator: null
  },
  onInit() {
    var options = {
      duration: 1500,
      easing: 'friction',
      delay: 0,
      fill: 'forwards',
      direction: "normal",
      iterations: 2,
      begin: 200.0,
      end: 400.0
    };
    this.animator = animator.create(options);
  },
  Show() {
    var options1 = {
      duration: 1500,
      easing: 'friction',
      delay: 0,
      fill: 'forwards',
      direction: "normal",
      iterations: 2,
      begin: 0,
      end: 400.0,
    };
    try {
      this.animator.reset(options1);
    } catch(error) {
      console.error(`Animator reset failed, error code: ${error.code}, message: ${error.message}.`);
    }
    var _this = this;
    this.animator.onframe = function(value) {
      _this.divWidth = value;
      _this.divHeight = value;
    };
    this.animator.play();
  }
}
```

  ![zh-cn_image_00007](figures/zh-cn_image_00007.gif)

## update<sup>(deprecated)</sup>

update(options: AnimatorOptions): void

更新当前动画器。

从API version9开始不再维护，建议使用[reset<sup>9+</sup>](#reset9)

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名     | 类型                                  | 必填   | 说明      |
| ------- | ----------------------------------- | ---- | ------- |
| options | [AnimatorOptions](#animatoroptions) | 是    | 定义动画选项。 |

**示例：**

```js
animator.update(options);
```

## createAnimator<sup>(deprecated)</sup>

createAnimator(options: AnimatorOptions): AnimatorResult

定义Animator类。

从API version9开始不再维护，建议使用[create<sup>9+</sup>](#create9)

**系统能力：**  SystemCapability.ArkUI.ArkUI.Full

**参数：** 

| 参数名     | 类型                                  | 必填   | 说明      |
| ------- | ----------------------------------- | ---- | ------- |
| options | [AnimatorOptions](#animatoroptions) | 是    | 定义动画选项。 |

**返回值：** 

| 类型                                | 说明            |
| --------------------------------- | ------------- |
| [AnimatorResult](#animatorresult) | Animator结果接口。 |

**示例：** 

```js
var options = {
  duration: 1500,
  easing: 'friction',
  delay: 0,
  fill: 'forwards',
  direction: "normal",
  iterations: 3,
  begin: 200.0,
  end: 400.0,
};
this.animator = animator.createAnimator(options);
```