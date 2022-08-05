# HiSysEvent Tool Usage


## Overview

The HiSysEvent tool is a command line tool preconfigured in the **/system/bin** directory of the system. You can use this tool to subscribe to real-time system events or query historical system vents.

## Subscribing to Real-Time System Events

- Command for subscribing to real-time system events:

    ```
    hisysevent -r
    ```

    Description of command options:

    | Option| Description|
    | -------- | -------- |
    | -r | Subscribes to real-time system events based on the default settings. When this option is specified, any real-time system event will be printed on the console.|

- Command for enabling the debugging mode:

    ```
    hisysevent -r -d
    ```

    Description of command options:

    | Option| Description|
    | -------- | -------- |
    | -d | Subscribes to real-time system events in debugging mode.|

- Command for subscribing to real-time system events by event tag:

    ```
    hisysevent -r -t <tag> [-c [WHOLE_WORD|PREFIX|REGULAR]]
    ```

    Description of command options:

    | Option| Description|
    | -------- | -------- |
    | -t | Event tag used to filter subscribed real-time system events.|
    | -c | Matching rule for event tags. The options can be **WHOLE_WORD**, **PREFIX**, or **REGULAR**.|

    Example:

    ```
	# hisysevent -r -t "STA" -c PREFIX
    {"domain_":"RELIABILITY","name_":"APP_FREEZE","type_":1,"time_":1501963670809,"pid_":1505,"uid_":10002,"FAULT_TYPE":"4","MODULE":"com.ohos.screenlock","REASON":"NO_DRAW","SUMMARY":"SUMMARY:\n","LOG_PATH":"/data/log/faultlog/faultlogger/appfreeze-com.ohos.screenlock-10002-20170805200750","HAPPEN_TIME":1501963670809,"VERSION":"1.0.0","level_":"CRITICAL","tag_":"STABILITY","id_":"4973863135535405472","info_":""}
    # hisysevent -r -t "STAw{0,6}" -c REGULAR
    {"domain_":"RELIABILITY","name_":"APP_FREEZE","type_":1,"time_":1501963793206,"pid_":1505,"uid_":10002,"FAULT_TYPE":"4","MODULE":"com.ohos.screenlock","REASON":"NO_DRAW","SUMMARY":"SUMMARY:\n","LOG_PATH":"/data/log/faultlog/faultlogger/appfreeze-com.ohos.screenlock-10002-20170805200953","HAPPEN_TIME":1501963793206,"VERSION":"1.0.0","level_":"CRITICAL","tag_":"STABILITY","id_":"16367997008075110557","info_":""}
    # hisysevent -r -t "STA\w+" -c REGULAR
    {"domain_":"RELIABILITY","name_":"APP_FREEZE","type_":1,"time_":1501963863393,"pid_":1505,"uid_":10002,"FAULT_TYPE":"4","MODULE":"com.ohos.screenlock","REASON":"NO_DRAW","SUMMARY":"SUMMARY:\n","LOG_PATH":"/data/log/faultlog/faultlogger/appfreeze-com.ohos.screenlock-10002-20170805201103","HAPPEN_TIME":1501963863393,"VERSION":"1.0.0","level_":"CRITICAL","tag_":"STABILITY","id_":"5522352691813553392","info_":""}
    ```

- Command for subscribing to real-time system events by event domain and event name:

    ```
    hisysevent -r -o <domain> -n <eventName> [-c [WHOLE_WORD|PREFIX|REGULAR]]
    ```

    Description of command options:

    | Option| Description|
    | -------- | -------- |
    | -o | Event domain used to filter subscribed real-time system events.|
    | -n | Event name used to filter subscribed real-time system events.|
    | -c | Matching rule for event domains and event names. The options can be **WHOLE_WORD**, PREFIX, or **REGULAR**.|

    Example:

    ```
    # hisysevent -r -o "RELIABILITY" -n "APP_FREEZE"
    {"domain_":"RELIABILITY","name_":"APP_FREEZE","type_":1,"time_":1501963989773,"pid_":1505,"uid_":10002,"FAULT_TYPE":"4","MODULE":"com.ohos.screenlock","REASON":"NO_DRAW","SUMMARY":"SUMMARY:\n","LOG_PATH":"/data/log/faultlog/faultlogger/appfreeze-com.ohos.screenlock-10002-20170805201309","HAPPEN_TIME":1501963989773,"VERSION":"1.0.0","level_":"CRITICAL","tag_":"STABILITY","id_":"16367997008075110557","info_":""}
    # hisysevent -r -o "RELIABI\w{0,8}" -n "APP_FREEZE" -c REGULAR
    {"domain_":"RELIABILITY","name_":"APP_FREEZE","type_":1,"time_":1501964144383,"pid_":1505,"uid_":10002,"FAULT_TYPE":"4","MODULE":"com.ohos.screenlock","REASON":"NO_DRAW","SUMMARY":"SUMMARY:\n","LOG_PATH":"/data/log/faultlog/faultlogger/appfreeze-com.ohos.screenlock-10002-20170805201544","HAPPEN_TIME":1501964144383,"VERSION":"1.0.0","level_":"CRITICAL","tag_":"STABILITY","id_":"13456525196455104060","info_":""}
    # hisysevent -r -o "RELIABI\w+" -c REGULAR
    {"domain_":"RELIABILITY","name_":"APP_FREEZE","type_":1,"time_":1501964193466,"pid_":1505,"uid_":10002,"FAULT_TYPE":"4","MODULE":"com.ohos.screenlock","REASON":"NO_DRAW","SUMMARY":"SUMMARY:\n","LOG_PATH":"/data/log/faultlog/faultlogger/appfreeze-com.ohos.screenlock-10002-20170805201633","HAPPEN_TIME":1501964193466,"VERSION":"1.0.0","level_":"CRITICAL","tag_":"STABILITY","id_":"12675246910904037271","info_":""}
    ```

    > **NOTE**
    > If **-t**, **-o**, and **-n** are specified, the system checks whether the configured event tag is null. If the event tag is not null, the system filters system events based on the matching rules for the event tag. Otherwise, the system filters system events based on the matching rules for the event domain and event name.


## Querying Historical System Events

- Command for querying historical system events:

    ```
    hisysevent -l
    ```

    Description of command options:

    | Option| Description|
    | -------- | -------- |
    | -l | Queries historical system events based on the default settings. A maximum of 1,000 latest system events will be returned.|

- Command for querying historical system events within the specified period of time:

    ```
    hisysevent -l -s <begin time> -e <end time>
    ```

    Description of command options:

    | Option| Description|
    | -------- | -------- |
    | -s | Start time for querying historical system events. Only system events generated after the start time are returned.|
    | -e | End time for querying historical system events. Only system events generated before the end time are returned.|

    Example:

    ```
    # hisysevent -l -s 1501964222980 -e 1501964222996
    {"domain_":"RELIABILITY","name_":"APP_FREEZE","type_":1,"time_":1501964222980,"pid_":1505,"uid_":10002,"FAULT_TYPE":"4","MODULE":"com.ohos.screenlock","REASON":"NO_DRAW","SUMMARY":"SUMMARY:\n","LOG_PATH":"/data/log/faultlog/faultlogger/appfreeze-com.ohos.screenlock-10002-20170805201702","HAPPEN_TIME":1501964222980,"VERSION":"1.0.0","level_":"CRITICAL","tag_":"STABILITY","id_":"10435592800188571430","info_":""}
    {"domain_":"GRAPHIC","name_":"NO_DRAW","type_":1,"time_":1501964222980,"tz_":"+0000","pid_":1505,"tid_":1585,"uid_":10002,"PID":1505,"UID":10002,"ABILITY_NAME":"","MSG":"It took 1957104259905ns to draw, UI took 0ns to draw, RSRenderThread took 8962625ns to draw, RSRenderThread dropped 0 UI Frames","level_":"MINOR","id_":"1708287249901948387","info_":"isResolved,eventId:0"}
    {"domain_":"RELIABILITY","name_":"APP_FREEZE","type_":1,"time_":1501964222994,"tz_":"+0000","pid_":623,"tid_":1445,"uid_":1201,"SUB_EVENT_TYPE":"NO_DRAW","EVENT_TIME":"20170805201702","MODULE":"NO_DRAW","PNAME":"NO_DRAW","REASON":"NO_DRAW","DIAG_INFO":"","STACK":"SUMMARY:\n","HIVIEW_LOG_FILE_PATHS":["/data/log/faultlog/faultlogger/appfreeze-NO_DRAW-10002-20170805201702"],"DOMAIN":"GRAPHIC","STRING_ID":"NO_DRAW","PID":1505,"UID":10002,"PACKAGE_NAME":"NO_DRAW","PROCESS_NAME":"","MSG":"It took 1956945826265ns to draw, UI took 0ns to draw, RSRenderThread took 9863293ns to draw, RSRenderThread dropped 0 UI Frames\n","level_":"CRITICAL","tag_":"STABILITY","id_":"10448522101019619655","info_":""}
    ```

- Command for setting the maximum number of historical events that can be queried:

    ```
    hisysevent -l -m <max hisysevent count>
    ```

    Description of command options:

    | Option| Description|
    | -------- | -------- |
    | -m | Maximum number of historical system events that can be queried. The value ranges from **0** to **1000**. The number of returned system events is not more than the value of this parameter.|

    Example:

    ```
    # hisysevent -l -s 1501964222980 -e 1501964222996 -m 1
    {"domain_":"RELIABILITY","name_":"APP_FREEZE","type_":1,"time_":1501964222980,"pid_":1505,"uid_":10002,"FAULT_TYPE":"4","MODULE":"com.ohos.screenlock","REASON":"NO_DRAW","SUMMARY":"SUMMARY:\n","LOG_PATH":"/data/log/faultlog/faultlogger/appfreeze-com.ohos.screenlock-10002-20170805201702","HAPPEN_TIME":1501964222980,"VERSION":"1.0.0","level_":"CRITICAL","tag_":"STABILITY","id_":"10435592800188571430","info_":""}
    ```

## System Event Validity Check

- Enabling system event validity check

    ```
    hisysevent -v
    ```
	
    Description of command options:

    | Option| Description|
    | -------- | -------- |
    | -v | Used with the subscription command **-r** and query command **-l**. If system event validity check is enabled, invalid content contained in system events will be highlighted in red.|

    Example:

    ```
    # hisysevent -v -l -s 1501964222980 -e 1501964222996
    # The **HAPPEN_TIME** and **VERSION** fields are not configured in the YAML file for the **APP_FREEZE** event that belongs to the **RELIABILITY** domain. Therefore, the two fields are highlighted in red.
    {"domain_":"RELIABILITY","name_":"APP_FREEZE","type_":1,"time_":1501964222980,"pid_":1505,"uid_":10002,"FAULT_TYPE":"4","MODULE":"com.ohos.screenlock","REASON":"NO_DRAW","SUMMARY":"SUMMARY:\n","LOG_PATH":"/data/log/faultlog/faultlogger/appfreeze-com.ohos.screenlock-10002-20170805201702","HAPPEN_TIME":1501964222980,"VERSION":"1.0.0","level_":"CRITICAL","tag_":"STABILITY","id_":"10435592800188571430","info_":""}
    # hisysevent -v -r -o "RELIABILITY" -n "APP_FREEZE"
    {"domain_":"RELIABILITY","name_":"APP_FREEZE","type_":1,"time_":1501964644584,"pid_":1505,"uid_":10002,"FAULT_TYPE":"4","MODULE":"com.ohos.screenlock","REASON":"NO_DRAW","SUMMARY":"SUMMARY:\n","LOG_PATH":"/data/log/faultlog/faultlogger/appfreeze-com.ohos.screenlock-10002-20170805202404","HAPPEN_TIME":1501964644584,"VERSION":"1.0.0","level_":"CRITICAL","tag_":"STABILITY","id_":"11097868872446282676","info_":""}
    ```
