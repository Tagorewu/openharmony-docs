# AudioMmapBufferDescripter


## **概述**

**所属模块:**

[Audio](_audio.md)


## **汇总**


### Public 属性

  | Public&nbsp;属性 | 描述 | 
| -------- | -------- |
| [memoryAddress](_audio.md#memoryaddress) | 指向mmap缓冲区的指针。 | 
| [memoryFd](_audio.md#memoryfd) | mmap缓冲区的文件描述符。 | 
| [totalBufferFrames](_audio.md#totalbufferframes) | 缓冲区总大小，单位：帧。 | 
| [transferFrameSize](_audio.md#transferframesize) | 传输大小，单位：帧。 | 
| [isShareable](_audio.md#isshareable) | mmap缓冲区是否可以在进程间共享。 | 


## **详细描述**

mmap缓冲区描述符。
