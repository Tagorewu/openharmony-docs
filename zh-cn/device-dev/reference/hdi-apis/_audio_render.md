# AudioRender


## **概述**

**所属模块:**

[Audio](_audio.md)


## **汇总**


### Public 属性

  | Public&nbsp;属性 | 描述 | 
| -------- | -------- |
| control | 音频控制能力接口，详情参考[AudioControl](_audio_control.md) | 
| attr | 音频属性能力接口，详情参考[AudioAttribute](_audio_attribute.md) | 
| scene | 音频场景能力接口，详情参考[AudioScene](_audio_scene.md) | 
| volume | 音频音量能力接口，详情参考[AudioVolume](_audio_volume.md) | 
| (&nbsp;[GetLatency](#getlatency)&nbsp;)(struct&nbsp;AudioRender&nbsp;\*render,&nbsp;uint32_t&nbsp;\*ms) | 获取音频硬件驱动估计的延迟时间&nbsp;[更多...](#getlatency) | 
| (&nbsp;[RenderFrame](#renderframe)&nbsp;)(struct&nbsp;AudioRender&nbsp;\*render,&nbsp;const&nbsp;void&nbsp;\*frame,&nbsp;uint64_t&nbsp;requestBytes,&nbsp;uint64_t&nbsp;\*replyBytes) | 往音频驱动中播放（render）一帧输出数据（放音，音频下行数据）&nbsp;[更多...](#renderframe) | 
| (&nbsp;[GetRenderPosition](#getrenderposition)&nbsp;)(struct&nbsp;AudioRender&nbsp;\*render,&nbsp;uint64_t&nbsp;\*frames,&nbsp;struct&nbsp;[AudioTimeStamp](_audio_time_stamp.md)&nbsp;\*time) | 获取音频输出帧数的上一次计数&nbsp;[更多...](#getrenderposition) | 
| (&nbsp;[SetRenderSpeed](#setrenderspeed)&nbsp;)(struct&nbsp;AudioRender&nbsp;\*render,&nbsp;float&nbsp;speed) | 设置一个音频的播放速度&nbsp;[更多...](#setrenderspeed) | 
| (&nbsp;[GetRenderSpeed](#getrenderspeed)&nbsp;)(struct&nbsp;AudioRender&nbsp;\*render,&nbsp;float&nbsp;\*speed) | 获取一个音频当前的播放速度&nbsp;[更多...](#getrenderspeed) | 
| (&nbsp;[SetChannelMode](#setchannelmode)&nbsp;)(struct&nbsp;AudioRender&nbsp;\*render,&nbsp;enum&nbsp;[AudioChannelMode](_audio.md#audiochannelmode)&nbsp;mode) | 设置音频播放的通道模式&nbsp;[更多...](#setchannelmode) | 
| (&nbsp;[GetChannelMode](#getchannelmode)&nbsp;)(struct&nbsp;AudioRender&nbsp;\*render,&nbsp;enum&nbsp;[AudioChannelMode](_audio.md#audiochannelmode)&nbsp;\*mode) | 获取音频播放当前的通道模式&nbsp;[更多...](#getchannelmode) | 
| (&nbsp;[RegCallback](#regcallback)&nbsp;)(struct&nbsp;AudioRender&nbsp;\*render,&nbsp;[RenderCallback](_audio.md#rendercallback)&nbsp;callback,&nbsp;void&nbsp;\*cookie) | 注册音频回调函数，用于放音过程中缓冲区数据写、DrainBuffer完成通知&nbsp;[更多...](#regcallback) | 
| (&nbsp;[DrainBuffer](#drainbuffer)&nbsp;)(struct&nbsp;AudioRender&nbsp;\*render,&nbsp;enum&nbsp;[AudioDrainNotifyType](_audio.md#audiodrainnotifytype)&nbsp;\*type) | 排空缓冲区中的数据&nbsp;[更多...](#drainbuffer) | 


## **详细描述**

AudioRender音频播放接口

提供音频播放支持的驱动能力，包括音频控制、音频属性、音频场景、音频音量、获取硬件延迟时间、播放音频帧数据（render frame）等

**参见：**

[AudioControl](_audio_control.md)

[AudioAttribute](_audio_attribute.md)

[AudioScene](_audio_scene.md)

[AudioVolume](_audio_volume.md)

**Since：**

1.0

**Version：**

1.0


## **类成员变量说明**


### DrainBuffer

  
```
int32_t(* AudioRender::DrainBuffer) (struct AudioRender *render, enum AudioDrainNotifyType *type)
```

**描述：**

排空缓冲区中的数据

**参数：**

  | 名称 | 描述 | 
| -------- | -------- |
| render | 待操作的音频播放接口对象 | 
| type | DrainBuffer的操作类型，详情请参考[AudioDrainNotifyType](_audio.md#audiodrainnotifytype) | 

**返回：**

成功返回值0，失败返回负值

**参见：**

[RegCallback](#regcallback)


### GetChannelMode

  
```
int32_t(* AudioRender::GetChannelMode) (struct AudioRender *render, enum AudioChannelMode *mode)
```

**描述：**

获取音频播放当前的通道模式

**参数：**

  | 名称 | 描述 | 
| -------- | -------- |
| render | 待操作的音频播放接口对象 | 
| mode | 获取的通道模式保存到mode中 | 

**返回：**

成功返回值0，失败返回负值

**参见：**

[SetChannelMode](#setchannelmode)


### GetLatency

  
```
int32_t(* AudioRender::GetLatency) (struct AudioRender *render, uint32_t *ms)
```

**描述：**

获取音频硬件驱动估计的延迟时间

**参数：**

  | 名称 | 描述 | 
| -------- | -------- |
| render | 待操作的音频播放接口对象 | 
| ms | 获取的延迟时间（单位：毫秒）保存到ms中 | 

**返回：**

成功返回值0，失败返回负值


### GetRenderPosition

  
```
int32_t(* AudioRender::GetRenderPosition) (struct AudioRender *render, uint64_t *frames, struct AudioTimeStamp *time)
```

**描述：**

获取音频输出帧数的上一次计数

**参数：**

  | 名称 | 描述 | 
| -------- | -------- |
| render | 待操作的音频播放接口对象 | 
| frames | 获取的音频帧计数保存到frames中 | 
| time | 获取的关联时间戳保存到time中 | 

**返回：**

成功返回值0，失败返回负值

**参见：**

[RenderFrame](#renderframe)


### GetRenderSpeed

  
```
int32_t(* AudioRender::GetRenderSpeed) (struct AudioRender *render, float *speed)
```

**描述：**

获取一个音频当前的播放速度

**参数：**

  | 名称 | 描述 | 
| -------- | -------- |
| render | 待操作的音频播放接口对象 | 
| speed | 获取的播放速度保存到speed中 | 

**返回：**

成功返回值0，失败返回负值

**参见：**

[SetRenderSpeed](#setrenderspeed)


### RegCallback

  
```
int32_t(* AudioRender::RegCallback) (struct AudioRender *render, RenderCallback callback, void *cookie)
```

**描述：**

注册音频回调函数，用于放音过程中缓冲区数据写、DrainBuffer完成通知

**参数：**

  | 名称 | 描述 | 
| -------- | -------- |
| render | 待操作的音频播放接口对象 | 
| callback | 注册的回调函数 | 
| cookie | 回调函数的入参 | 

**返回：**

成功返回值0，失败返回负值

**参见：**

[RegCallback](#regcallback)


### RenderFrame

  
```
int32_t(* AudioRender::RenderFrame) (struct AudioRender *render, const void *frame, uint64_t requestBytes, uint64_t *replyBytes)
```

**描述：**

往音频驱动中播放（render）一帧输出数据（放音，音频下行数据）

**参数：**

  | 名称 | 描述 | 
| -------- | -------- |
| render | 待操作的音频播放接口对象 | 
| frame | 待写入的输出数据的音频frame | 
| requestBytes | 待写入的输出数据的音频frame大小（字节数） | 
| replyBytes | 实际写入的音频数据长度（字节数），获取后保存到replyBytes中 | 

**返回：**

成功返回值0，失败返回负值


### SetChannelMode

  
```
int32_t(* AudioRender::SetChannelMode) (struct AudioRender *render, enum AudioChannelMode mode)
```

**描述：**

设置音频播放的通道模式

**参数：**

  | 名称 | 描述 | 
| -------- | -------- |
| render | 待操作的音频播放接口对象 | 
| speed | 待设置的通道模式 | 

**返回：**

成功返回值0，失败返回负值

**参见：**

[GetChannelMode](#getchannelmode)


### SetRenderSpeed

  
```
int32_t(* AudioRender::SetRenderSpeed) (struct AudioRender *render, float speed)
```

**描述：**

设置一个音频的播放速度

**参数：**

  | 名称 | 描述 | 
| -------- | -------- |
| render | 待操作的音频播放接口对象 | 
| speed | 待设置的播放速度 | 

**返回：**

成功返回值0，失败返回负值

**参见：**

[GetRenderSpeed](#getrenderspeed)
