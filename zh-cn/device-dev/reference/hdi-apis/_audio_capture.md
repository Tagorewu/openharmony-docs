# AudioCapture


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
| (&nbsp;[CaptureFrame](#captureframe)&nbsp;)(struct&nbsp;AudioCapture&nbsp;\*capture,&nbsp;void&nbsp;\*frame,&nbsp;uint64_t&nbsp;requestBytes,&nbsp;uint64_t&nbsp;\*replyBytes) | 从音频驱动中录制（capture）一帧输入数据（录音，音频上行数据）&nbsp;[更多...](#captureframe) | 
| (&nbsp;[GetCapturePosition](#getcaptureposition)&nbsp;)(struct&nbsp;AudioCapture&nbsp;\*capture,&nbsp;uint64_t&nbsp;\*frames,&nbsp;struct&nbsp;[AudioTimeStamp](_audio_time_stamp.md)&nbsp;\*time) | 获取音频输入帧数的上一次计数&nbsp;[更多...](#getcaptureposition) | 


## **详细描述**

AudioCapture音频录音接口。


## **类成员变量说明**


### CaptureFrame

  
```
int32_t(* AudioCapture::CaptureFrame) (struct AudioCapture *capture, void *frame, uint64_t requestBytes, uint64_t *replyBytes)
```

**描述：**

从音频驱动中录制（capture）一帧输入数据（录音，音频上行数据）

**参数：**

  | 名称 | 描述 | 
| -------- | -------- |
| capture | 待操作的音频录音接口对象 | 
| frame | 待存放输入数据的音频frame | 
| requestBytes | 待存放输入数据的音频frame大小（字节数） | 
| replyBytes | 实际读取到的音频数据长度（字节数），获取后保存到replyBytes中 | 

**返回：**

成功返回值0，失败返回负值


### GetCapturePosition

  
```
int32_t(* AudioCapture::GetCapturePosition) (struct AudioCapture *capture, uint64_t *frames, struct AudioTimeStamp *time)
```

**描述：**

获取音频输入帧数的上一次计数

**参数：**

  | 名称 | 描述 | 
| -------- | -------- |
| capture | 待操作的音频录音接口对象 | 
| frames | 获取的音频帧计数保存到frames中 | 
| time | 获取的关联时间戳保存到time中 | 

**返回：**

成功返回值0，失败返回负值

**参见：**

[CaptureFrame](#captureframe)