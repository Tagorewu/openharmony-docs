# ShortcutInfo<sup>(deprecated)<sup>

The **ShortcutInfo** module provides shortcut information defined in the configuration file. For details about the configuration in the FA model, see [config.json](../../quick-start/package-structure.md). For details about the configuration in the stage model, see [Internal Structure of the shortcuts Attribute](../../quick-start/stage-structure.md#internal-structure-of-the-shortcuts-attribute).

> **NOTE**
>
> This module is deprecated since API version 9. You are advised to use [ShortcutInfo](js-apis-bundleManager-shortcutInfo.md) instead.
>
> The initial APIs of this module are supported since API version 7. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## ShortcutWant<sup>(deprecated)<sup>

> This API is deprecated since API version 9. You are advised to use [ShortcutWant](js-apis-bundleManager-shortcutInfo.md) instead.

 **System capability**: SystemCapability.BundleManager.BundleFramework

 **System API**: This is a system API and cannot be called by third-party applications.

| Name                     | Type  | Readable| Writable| Description                |
| ------------------------- | ------ | ---- | ---- | -------------------- |
| targetBundle              | string | Yes  | No  | Target bundle of the shortcut.|
| targetClass               | string | Yes  | No  | Target class required by the shortcut.|

## ShortcutInfo<sup>(deprecated)<sup>

> This API is deprecated since API version 9. You are advised to use [ShortcutInfo](js-apis-bundleManager-shortcutInfo.md) instead.


 **System capability**: SystemCapability.BundleManager.BundleFramework

| Name                   | Type                                      | Readable| Writable| Description                        |
| ----------------------- | ------------------------------------------ | ---- | ---- | ---------------------------- |
| id                      | string                                     | Yes  | No  | ID of the application to which the shortcut belongs.    |
| bundleName              | string                                     | Yes  | No  | Name of the bundle that contains the shortcut.        |
| hostAbility             | string                                     | Yes  | No  | Local ability information of the shortcut.   |
| icon                    | string                                     | Yes  | No  | Icon of the shortcut.              |
| iconId<sup>8+</sup>     | number                                     | Yes  | No  | Icon ID of the shortcut.            |
| label                   | string                                     | Yes  | No  | Label of the shortcut.              |
| labelId<sup>8+</sup>    | number                                     | Yes  | No  | Label ID of the shortcut.            |
| disableMessage          | string                                     | Yes  | No  | Message displayed when the shortcut is disabled.          |
| wants                   | Array&lt;[ShortcutWant](#shortcutwant)&gt; | Yes  | No  | Want information required for the shortcut.        |
| isStatic                | boolean                                    | Yes  | No  | Whether the shortcut is static.          |
| isHomeShortcut          | boolean                                    | Yes  | No  | Whether the shortcut is a home shortcut.|
| isEnabled               | boolean                                    | Yes  | No  | Whether the shortcut is enabled.            |
