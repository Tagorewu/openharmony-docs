# Kernel Overview


## Overview

The OpenHarmony LiteOS-M kernel is a lightweight operating system (OS) kernel designed for the IoT field. It features small size, low power consumption, and high performance. The LiteOS-M kernel has simple code structure, including the minimum function set, kernel abstraction layer (KAL), optional components, and project directory. It supports the Hardware Driver Foundation (HDF), which provides unified driver standards and access mode for device vendors to simplify porting of drivers and allow one-time development for multi-device deployment.

The OpenHarmony LiteOS-M kernel architecture consists of the hardware layer and hardware-irrelevant layers, as shown in the figure below. The hardware layer is classified based on the compiler toolchain and chip architecture, and provides a unified Hardware Abstraction Layer (HAL) interface to improve hardware adaptation and facilitate the expansion of various types of AIoT hardware and compilation toolchains. The other modules are irrelevant to the hardware. The basic kernel module provides basic kernel capabilities. The extended modules provide capabilities of components, such as the network and file systems, as well as exception handling and debug tools. The KAL provides unified standard APIs.

  **Figure 1** Kernel architecture

  ![](figures/kernel-architecture.png "kernel-architecture")


## CPU Architecture Support

The CPU architecture includes two layers: general architecture definition layer and specific architecture definition layer. The former provides interfaces supported and implemented by all architectures. The latter is specific to an architecture. For a new architecture to be added, the general architecture definition layer must be implemented first and the architecture-specific functions can be implemented at the specific architecture definition layer.

  **Table 1** CPU architecture rules

| Rule| General Architecture Layer| Specific Architecture Layer|
| -------- | -------- | -------- |
| Header file location| arch/include | arch/&lt;arch&gt;/&lt;arch&gt;/&lt;toolchain&gt;/ |
| Header file name| los_&lt;function&gt;.h | los_arch_&lt;function&gt;.h |
| Function name| Halxxxx | Halxxxx |

LiteOS-M supports mainstream architectures, such as ARM Cortex-M3, ARM Cortex-M4, ARM Cortex-M7, ARM Cortex-M33, and RISC-V. If you need to expand the CPU architecture, see [Chip Architecture Adaptation](../porting/porting-chip-kernel-overview.md).


## Working Principles

In the  **target\_config.h**  file of the development board, configure the system clock and number of ticks per second, and configure the task, memory, inter-process communication (IPC), and exception handling modules based on service requirements. When the system boots, the modules are initialized based on the configuration. The kernel startup process includes peripheral initialization, system clock configuration, kernel initialization, and OS boot, as shown in the figure below.

  **Figure 2** Kernel startup process<br>
  ![](figures/kernel-startup-process.png "kernel-startup-process")
