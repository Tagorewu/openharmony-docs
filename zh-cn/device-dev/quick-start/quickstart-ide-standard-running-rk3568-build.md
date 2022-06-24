# 编译


1. 在菜单栏中点击**Project Settings**按钮，进入RK3568工程配置界面。

   ![zh-cn_image_0000001265492885](figures/zh-cn_image_0000001265492885.png)

2. 在Toolchain页签中，DevEco Device Tool会自动检测依赖的编译工具链是否完备，如果提示部分工具缺失，可点击**Install**按钮，自动安装所需工具链。

   > ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
   > 如果出现安装pip组件失败，可参考[修改Python源的方法](https://device.harmonyos.com/cn/docs/documentation/guide/ide-set-python-source-0000001227639986)进行修改，完成尝试重新安装。

   ![zh-cn_image_0000001221356692](figures/zh-cn_image_0000001221356692.png)

   安装RK3568相关工具链，部分工具的安装需要使用root权限，请在“TERMINAL”窗口输入用户密码进行安装。

   ![zh-cn_image_0000001327429541.png](figures/zh-cn_image_0000001327429541.png)

   工具链自动安装完成后如下图所示。

   ![zh-cn_image_0000001265676877](figures/zh-cn_image_0000001265676877.png)

3. 在“hh_scdy200”配置页签中，设置源码的编译类型**build_type**，默认为"debug类型，请根据需要进行修改。然后点击**Save**按钮进行保存。

   ![zh-cn_image_0000001276354454.png](figures/zh-cn_image_0000001276354454.png) 

4. 在DevEco Device Tool界面的“PROJECT TASKS”中，点击对应开发板下的**Build**按钮，执行编译。

   ![zh-cn_image_0000001265516901](figures/zh-cn_image_0000001265516901.png)

5. 等待编译完成，在**TERMINAL**窗口输出“SUCCESS”，编译完成。

   ![zh-cn_image_0000001222361042](figures/zh-cn_image_0000001222361042.png)

   编译完成后，可以在工程的**out**目录下，查看编译生成的文件，用于后续的[RK3568开发板烧录](quickstart-standard-running-rk3568-burning.md)。