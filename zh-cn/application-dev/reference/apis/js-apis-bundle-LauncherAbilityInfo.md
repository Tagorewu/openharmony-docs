# LauncherAbilityInfo



> ![icon-note.gif](public_sys-resources/icon-note.gif) **说明：**
> 本模块首批接口从API version 8 开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。



LauncherAbilityInfo信息

## LauncherAbilityInfo

 **系统能力:** 以下各项对应的系统能力均为SystemCapability.BundleManager.BundleFramework

| 名称            | 类型                                                 | 可读 | 可写 | 说明                                 |
| --------------- | ---------------------------------------------------- | ---- | ---- | ------------------------------------ |
| applicationInfo | [ApplicationInfo](js-apis-bundle-ApplicationInfo.md) | 是   | 否   | launcher ability的应用程序的配置信息 |
| elementName     | [ElementName](js-apis-bundle-ElementName.md)         | 是   | 否   | launcher ability的ElementName信息    |
| labelId         | number                                               | 是   | 否   | launcher ability的标签ID             |
| iconId          | number                                               | 是   | 否   | launcher ability的图标ID             |
| userId          | number                                               | 是   | 否   | launcher ability的用户ID             |
| installTime     | number                                               | 是   | 否   | launcher ability的安装时间           |