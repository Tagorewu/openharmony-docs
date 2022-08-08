# AbilityConstant

The **AbilityConstant** module provides ability launch parameters.

The parameters include the initial launch reasons, reasons for the last exit, and ability continuation results.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version. 
> The APIs of this module can be used only in the stage model.

## Modules to Import

```js
import AbilityConstant from '@ohos.application.AbilityConstant';
```

## Attributes

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name| Type| Readable| Writable| Description| 
| -------- | -------- | -------- | -------- | -------- |
| launchReason | LaunchReason| Yes| Yes| Ability launch reason.| 
| lastExitReason | LastExitReason | Yes| Yes| Reason for the last exit.| 

## AbilityConstant.LaunchReason

Enumerates ability launch reasons.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name                         | Value  | Description                                                        |
| ----------------------------- | ---- | ------------------------------------------------------------ |
| UNKNOWN          | 0    | Unknown reason.|
| START_ABILITY          | 1    | Ability startup.|
| CALL | 2    | Call.|
| CONTINUATION           | 3    | Ability continuation.|


## AbilityConstant.LastExitReason

Enumerates reasons for the last exit.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name                         | Value  | Description                                                        |
| ----------------------------- | ---- | ------------------------------------------------------------ |
| UNKNOWN          | 0    | Unknown reason.|
| ABILITY_NOT_RESPONDING          | 1    | The ability does not respond.|
| NORMAL | 2    | Normal status.|


## AbilityConstant.OnContinueResult 

Enumerates ability continuation results.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name                         | Value  | Description                                                        |
| ----------------------------- | ---- | ------------------------------------------------------------ |
| AGREE           | 0    | Continuation agreed.|
| REJECT           | 1    | Continuation denied.|
| MISMATCH  | 2    | Mismatch.|

## AbilityConstant.WindowMode

Enumerates the window modes when an ability is started.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

| Name                       | Value| Description                |
| ---                         | --- | ---                  |
| WINDOW_MODE_UNDEFINED       | 0   | Undefined window mode.      |
| WINDOW_MODE_FULLSCREEN      | 1   | The ability is displayed in full screen.           |
| WINDOW_MODE_SPLIT_PRIMARY   | 100 | The ability is displayed in the primary window in split-screen mode.  |
| WINDOW_MODE_SPLIT_SECONDARY | 101 | The ability is displayed in the secondary window in split-screen mode.  |
| WINDOW_MODE_FLOATING        | 102 | The ability is displayed in a floating window.|
