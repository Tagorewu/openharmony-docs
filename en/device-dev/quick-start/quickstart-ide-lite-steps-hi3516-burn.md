# Burning


Burning is the process of downloading compiled program files to a development board to provide a basis for subsequent debugging. With the one-click burning function of DevEco Device Tool, you can burn images on development boards quickly and efficiently.


Hi3516D V300 supports burning through the USB port, network port, and serial port. This document describes how to burn source code through the USB port. The operations are performed in Windows.


1. Connect the computer and the target development board through the serial port and USB port. For details, see [Introduction to the Hi3516D V300 Development Board](quickstart-lite-introduction-hi3516.md).
   > ![icon-note.gif](../public_sys-resources/icon-note.gif) **NOTE**
   > If you are using the remote access mode (Windows + Ubuntu on the local VM), disable the USB control of the VM as follows to ensure that the development board is connected to the USB port of the host:
   > 
   > - VMware: Configure the device to connect to the host under **Preferences** > **USB** and remove the USB controller from the VM settings.
   > 
   > - VirtualBox: Deselect **Enable USB Controller** in the USB device options under Ubuntu settings.

2. If your computer does not have the USB port driver or USB-to-serial driver, install it by following the instructions in [Installing the USB Port Driver on the Hi3516D V300 or Hi3518E V300 Development Board](Installing the USB Port Driver on the Hi3516D V300 or Hi3518E V300 Development Board) or [Installing the Serial Port Driver on the Hi3516D V300 or Hi3518E V300 Development Board](https://device.harmonyos.com/en/docs/documentation/guide/hi3516_hi3518-drivers-0000001050743695), depending on the missing driver.

3. In DevEco Device Tool, choose **REMOTE DEVELOPMENT** > **Local PC** to check the connection status between the remote computer (Ubuntu build environment) and the local computer (Windows build environment).
   - If ![en-us_image_0000001261315939](figures/en-us_image_0000001261315939.png) is displayed on the right of **Local PC**, the remote computer is connected to the local computer. In this case, no further action is required.
   - If ![en-us_image_0000001261515989](figures/en-us_image_0000001261515989.png) is displayed, click the connect icon.

   ![en-us_image_0000001261395999](figures/en-us_image_0000001261395999.png)

   > ![icon-note.gif](../public_sys-resources/icon-note.gif) **NOTE**
   > This operation is required only in remote access mode (in the Windows+Ubuntu hybrid build environment). If the local access mode (Windows or Ubuntu build environment) is used, skip this step.

4. Check the serial port number in **QUICK ACCESS** > **DevEco Home** > **Device** in DevEco Device Tool.

   ![en-us_image_0000001216516128](figures/en-us_image_0000001216516128.png)

5. Choose **QUICK ACCESS** > **DevEco Home** > **Projects**, and then click **Settings**.

   ![en-us_image_0000001198566364](figures/en-us_image_0000001198566364.png)

6. On the **hi3516dv300** tab page, set the burning options.
   - **upload_partitions**: Select the file to be burnt. By default, the **fastboot**, **kernel**, **rootfs**, and **userfs** files are burnt at the same time.
   - **upload_port**: Select the serial port number obtained.
   - **upload_protocol**: Select the burning protocol **hiburn-usb**.

   ![en-us_image_0000001223190441](figures/en-us_image_0000001223190441.png)

7. In **Partitions**, check the preset burning settings of the files to be burnt.

   ![en-us_image_0000001312778829](figures/en-us_image_0000001312778829.png)

    To modify the burning settings for a specific file, click ![en-us_image_0000001312898911](figures/en-us_image_0000001312898911.png) next to the file.
   > ![icon-note.gif](../public_sys-resources/icon-note.gif) **NOTE**
   > Set the start address and length of the partition based on the size of the files to be burnt. Make sure the size of the partition is greater than that of the files to be burnt and the partition addresses of the files to be burnt do not overlap.

   ![en-us_image_0000001312780249](figures/en-us_image_0000001312780249.png)

8. When you finish modifying, click **Save** on the top.

9. Go to **hi3516dv300** > **Upload** to transfer the files to be burnt from Ubuntu to Windows. When the "Operation paused, Please press Enter key to continue" message is displayed, which indicates that the transfer is complete, press **Enter** to start burning.

   ![en-us_image_0000001266887264](figures/en-us_image_0000001266887264.png)

10. When the following information is displayed in the **TERMINAL** window, press and hold the reset button within 15 seconds, remove and insert the USB cable, and release the reset button to start burning.

    ![en-us_image_0000001114129426](figures/en-us_image_0000001114129426.png)

    If the following message is displayed, it indicates that the burning is successful.

    ![en-us_image_0000001160649343](figures/en-us_image_0000001160649343.png)

11. When the burning is successful, perform the operations in Running to start the system.
