# reminderAgentManager错误码

## 1700001 通知使能未开启

### 错误信息
Notification does not enable.

### 可能原因
1. 未申请通知使能。
2. 通知使能被关闭。

### 处理步骤
1. 申请通知使能弹窗[Notification.requestEnableNotification](../apis/js-apis-notification.md#notificationrequestenablenotification8)。
2. 检查通知使能是否被关闭。

## 1700002 提醒数量超出限制

### 错误信息
The number of reminders exceeds the limit.

### 可能原因
1. 当前系统提醒超过2000个。
2. 当前应用提醒超过30个。

### 处理步骤
删除不必要的提醒

## 1700003 提醒不存在

### 错误信息
The reminder does not exist.

### 可能原因
1. 提醒已过期。
2. 提醒已被删除。

### 处理步骤
1. 检查提醒是否有效。
2. 检查提醒是否已被删除。

## 1700004 包名不存在

### 错误信息
The package name does not exist.

### 可能原因
1. 包名不正确。
2. 应用未安装。

### 处理步骤
检查应用包名是否存在。
