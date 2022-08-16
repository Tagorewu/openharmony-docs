# 概述


本文档从芯片适配的端到端视角，为芯片/模组制造商提供基于OpenHarmony的芯片适配指导。典型的芯片架构，例如cortex-m、risc-v系列都可以按照本文档进行适配移植。


## 约束与限制

本文档适用于OpenHarmony LTS 3.0.1及之前版本的轻量系统的适配。

> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本文仅对OpenHarmony移植适配过程中需要关注的文件和配置项进行介绍，其他文件以及配置项开发者无需关注，故不作详细介绍。


## 适配流程

  主要开展基于伙伴硬件平台面向OpenHarmony系统的移植适配工作，具体细分为：移植准备、移植内核、移植子系统和移植验证四个环节，见表1芯片适配步骤。

  **表1** 芯片适配步骤

| 步骤 | 介绍 | 
| -------- | -------- |
| 移植准备 | 从OpenHarmony开源社区下载代码，并完成编译环境搭建，基于此初步熟悉和了解OpenHarmony的编译构建框架。 | 
| 移植内核 | 将伙伴的SDK移植到OpenHarmony平台，同时根据芯片arch支持情况确认是否需要开展arch的适配工作。 | 
| 移植子系统 | 开展包括启动子系统、文件子系统、安全子系统、通信子系统和外设驱动的移植。 | 
| 移植验证 | 在适配完成之后使用OpenHarmony社区提供的兼容性测试套件对适配的工程进行基本接口的测试验证，同时伙伴需要使用自有测试能力对适配工程开展质量验证活动。 | 


  **图1** 业务总体流程 
 
  ![zh-cn_image_0000001378282213](figures/zh-cn_image_0000001378282213.png)


## 基本概念

  **表2** 基本概念

| 名词 | 介绍 | 
| -------- | -------- |
| 子系统 | 是一个逻辑概念，它由一个或多个具体的组件组成。OpenHarmony整体遵从分层设计，从下向上依次为：内核层、系统服务层、框架层和应用层。系统功能按照“系统&nbsp;&gt;&nbsp;子系统&nbsp;&gt;&nbsp;组件”逐级展开，在多设备部署场景下，支持根据实际需求裁剪某些非必要的子系统或组件。 | 
| 部件 | 系统最小的可复用、可配置、可裁剪的功能单元。部件具备目录独立可并行开发、可独立编译、可独立测试的特征。 | 
| hb | OpenHarmony的命令行工具，用来执行编译命令。 | 
| DP平台 | Devicepartner缩写，即华为智能硬件合作伙伴平台，为生态合作伙伴提供产品开发、认证、发布等一站式服务的平台。 | 
| IR平台 | Developers&nbsp;IssueReporter缩写，是由华为运营的、面向所有华为开发者用户的产品服务平台。 | 
| HOBT | HiLink&nbsp;SDK&nbsp;OHOS&nbsp;Basic&nbsp;Test缩写，是HiLink&nbsp;SDK&nbsp;接入&nbsp;OpenHarmony的基础功能测试，检验HiLink&nbsp;SDK依赖的相关接口功能是否完善。 | 
| Token | 伙伴从合作伙伴平台（https://devicepartner.huawei.com/cn/）申请的设备身份凭据，每个设备唯一；需要在产线上逐个设备写入，用来标识设备是经过华为授权的。 | 
| Kit&nbsp;Framework | Kit&nbsp;Framework是Kit的基础框架，包含了OpenHarmony的安全组件，不可裁剪。 | 
| HiLink&nbsp;SDK | HarmonyOS&nbsp;Connect套件的一个关键组成部分，用于实现设备的联网，以及设备与HarmonyOS&nbsp;Connect云和智慧生活App的互联互通。 | 
| kv | 键值对(key-value)，描述数据存储的格式。 | 
