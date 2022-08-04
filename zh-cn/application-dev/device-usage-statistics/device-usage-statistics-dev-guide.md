# 设备使用信息统计

## 场景介绍

设备使用信息统计，包括app usage/notification usage/system usage等使用统计。例如应用使用信息统计，用于保存和查询应用使用详情（app usage）、事件日志数据（event log）、应用分组（bundle group）情况。
部件缓存的应用记录（使用历史统计和使用事件记录）会在事件上报后30分钟内刷新到数据库持久化保存。

## 接口说明
注册相关接口包导入：
```js
import stats from '@ohos.bundleState';
```

**表1** 设备使用信息统计主要接口

| 接口名 | 描述 |
| -------- | -------- |
| function queryBundleActiveStates(begin: number, end: number, callback: AsyncCallback&lt;Array&lt;BundleActiveState&gt;&gt;): void | 通过指定起始和结束时间查询所有应用的事件集合。 |
| function queryBundleStateInfos(begin: number, end: number, callback: AsyncCallback&lt;BundleActiveInfoResponse&gt;): void | 通过指定起始和结束时间查询应用使用时长统计信息。 |
| function queryCurrentBundleActiveStates(begin: number, end: number, callback: AsyncCallback&lt;Array&lt;BundleActiveState&gt;&gt;): void | 通过指定起始和结束时间查询当前应用的事件集合。 |
| function queryBundleStateInfoByInterval(byInterval: IntervalType, begin: number, end: number, callback: AsyncCallback&lt;Array&lt;BundleStateInfo&gt;&gt;): void | 通过指定时间段间隔（天、周、月、年）查询应用使用时长统计信息。 |
| function queryAppUsagePriorityGroup(callback: AsyncCallback&lt;number&gt;): void | 查询当前应用的使用优先级群组。callback形式。 |
| function queryAppUsagePriorityGroup(): Promise&lt;number&gt;; | 查询当前应用的使用优先级群组。promise形式。 |
| function isIdleState(bundleName: string, callback: AsyncCallback&lt;boolean&gt;): void | 判断指定Bundle Name的应用当前是否是空闲状态。 |
| function getRecentlyUsedModules(maxNum? : number, callback: AsyncCallback&lt;BundleActiveModuleInfo&gt;): void | 根据maxNum，查询FA使用记录，返回不超过maxNum条FA使用记录，若不填写maxNum参数，则默认maxNum值为1000。 |
| function queryAppNotificationNumber(begin: number, end: number, callback: AsyncCallback&lt;Array&lt;BundleActiveEventState&gt;&gt;): void | 通过指定起始和结束时间查询所有应用的通知次数。 |
| function queryBundleActiveEventStates(begin: number, end: number, callback: AsyncCallback&lt;Array&lt;BundleActiveEventState&gt;&gt;): void | 通过指定起始和结束时间查询系统事件（休眠、唤醒、解锁、锁屏）统计信息。 |
| function queryAppUsagePriorityGroup(bundleName? : string, callback: AsyncCallback&lt;number&gt;): void | 查询当前调用者应用或者指定应用的使用优先级群组。callback形式。 |
| function queryAppUsagePriorityGroup(bundleName? : string): Promise&lt;number&gt;; | 查询当前调用者应用或者指定应用的使用优先级群组。promise形式。 |
| function setBundleGroup(bundleName : string, newGroup: GroupType, callback: AsyncCallback&gt;boolean&gt;): void | 给应用名是bundleName的应用分组设置成newGroup，返回设置结果是否成功，以callback形式返回。 |
| function setBundleGroup(bundleName : string, newGroup : GroupType): Promise&gt;boolean&gt;; | 给应用名是bundleName的应用分组设置成newGroup，返回设置结果是否成功，以promise形式返回。 |
| function registerGroupCallBack(callback: Callback&gt;BundleActiveGroupCallbackInfo&gt;, callback: AsyncCallback&gt;boolean&gt;): void | 注册应用分组变化监听回调，返回注册是否成功，当应用分组发生变化时，会给所有已注册的监听者返回回调信息，以callback形式返回。 |
| function registerGroupCallBack(callback: Callback&gt;BundleActiveGroupCallbackInfo&gt;): Promise&gt;boolean&gt;; | 注册应用分组变化监听回调，返回注册是否成功，当应用分组发生变化时，会给所有已注册的监听者返回回调信息，以promise形式返回。 |
| function unRegisterGroupCallBack(callback: AsyncCallback&gt;boolean&gt;): void | 解除应用分组监听回调，以callback形式返回。 |
| function unRegisterGroupCallBack(): Promise&gt;boolean&gt;; | 解除应用分组监听回调，以promise形式返回。 |

## 开发步骤

1. 在config.json文件中配置设备使用信息统计权限。

    ```json
    "module": {
        "package": "com.example.deviceUsageStatistics",
        ...,
        "reqPermissions": [
            {
                "name": "ohos.permission.BUNDLE_ACTIVE_INFO"
            }
        ]
    }
    ```

2. 通过指定起始和结束时间查询所有应用的事件集合，config.json中需要配置权限：ohos.permission.BUNDLE_ACTIVE_INFO。

    ```js
    import stats from '@ohos.bundleState'

    // 异步方法promise方式
    stats.queryBundleActiveStates(0, 20000000000000).then(res => {
        console.log('BUNDLE_ACTIVE queryBundleActiveStates promise success.');
        for (let i = 0; i < res.length; i++) {
            console.log('BUNDLE_ACTIVE queryBundleActiveStates promise number : ' + (i + 1));
            console.log('BUNDLE_ACTIVE queryBundleActiveStates promise result ' + JSON.stringify(res[i]));
        }
    }).catch(err => {
        console.log('BUNDLE_ACTIVE queryBundleActiveStates promise failed, because: ' + err.code);
    });

    // 异步方法callback方式
    stats.queryBundleActiveStates(0, 20000000000000, (err, res) => {
        if (err) {
            console.log('BUNDLE_ACTIVE queryBundleActiveStates callback failed, because: ' + err.code);
        } else {
            console.log('BUNDLE_ACTIVE queryBundleActiveStates callback success.');
            for (let i = 0; i < res.length; i++) {
                console.log('BUNDLE_ACTIVE queryBundleActiveStates callback number : ' + (i + 1));
                console.log('BUNDLE_ACTIVE queryBundleActiveStates callback result ' + JSON.stringify(res[i]));
            }
        }
    });
    ```

3. 通过指定起始和结束时间查询应用使用时长统计信息，config.json中需要配置权限：ohos.permission.BUNDLE_ACTIVE_INFO。

    ```js
    import stats from '@ohos.bundleState'

    // 异步方法promise方式
    stats.queryBundleStateInfos(0, 20000000000000).then(res => {
        console.log('BUNDLE_ACTIVE queryBundleStateInfos promise success.');
        let i = 1;
        for (let key in res){
            console.log('BUNDLE_ACTIVE queryBundleStateInfos promise number : ' + i);
            console.log('BUNDLE_ACTIVE queryBundleStateInfos promise result ' + JSON.stringify(res[key]));
            i++;
        }
    }).catch(err => {
        console.log('BUNDLE_ACTIVE queryBundleStateInfos promise failed, because: ' + err.code);
    });

    // 异步方法callback方式
    stats.queryBundleStateInfos(0, 20000000000000, (err, res) => {
        if (err) {
            console.log('BUNDLE_ACTIVE queryBundleStateInfos callback failed, because: ' + err.code);
        } else {
            console.log('BUNDLE_ACTIVE queryBundleStateInfos callback success.');
            let i = 1;
            for(let key in res){
                console.log('BUNDLE_ACTIVE queryBundleStateInfos callback number : ' + i);
                console.log('BUNDLE_ACTIVE queryBundleStateInfos callback result ' + JSON.stringify(res[key]));
                i++;
            }
        }
    });
    ```

4. 通过指定起始和结束时间查询当前应用的事件集合，config.json中不需要配置权限。

    ```js
    import stats from '@ohos.bundleState'

    // 异步方法promise方式
    stats.queryCurrentBundleActiveStates(0, 20000000000000).then(res => {
        console.log('BUNDLE_ACTIVE queryCurrentBundleActiveStates promise success.');
        for (let i = 0; i < res.length; i++) {
            console.log('BUNDLE_ACTIVE queryCurrentBundleActiveStates promise number : ' + (i + 1));
            console.log('BUNDLE_ACTIVE queryCurrentBundleActiveStates promise result ' + JSON.stringify(res[i]));
        }
    }).catch(err => {
        console.log('BUNDLE_ACTIVE queryCurrentBundleActiveStates promise failed, because: ' + err.code);
    });

    // 异步方法callback方式
    stats.queryCurrentBundleActiveStates(0, 20000000000000, (err, res) => {
        if (err) {
            console.log('BUNDLE_ACTIVE queryCurrentBundleActiveStates callback failed, because: ' + err.code);
        } else {
            console.log('BUNDLE_ACTIVE queryCurrentBundleActiveStates callback success.');
            for (let i = 0; i < res.length; i++) {
                console.log('BUNDLE_ACTIVE queryCurrentBundleActiveStates callback number : ' + (i + 1));
                console.log('BUNDLE_ACTIVE queryCurrentBundleActiveStates callback result ' + JSON.stringify(res[i]));
            }
        }
    });
    ```

5. 通过指定时间段间隔（天、周、月、年）查询应用使用时长统计信息，config.json中需要配置权限：ohos.permission.BUNDLE_ACTIVE_INFO。

    ```js
    import stats from '@ohos.bundleState'

    // 异步方法promise方式
    stats.queryBundleStateInfoByInterval(0, 0, 20000000000000).then(res => {
        console.log('BUNDLE_ACTIVE queryBundleStateInfoByInterval promise success.');
        for (let i = 0; i < res.length; i++) {
            console.log('BUNDLE_ACTIVE queryBundleStateInfoByInterval promise number : ' + (i + 1));
            console.log('BUNDLE_ACTIVE queryBundleStateInfoByInterval promise result ' + JSON.stringify(res[i]));
        }
    }).catch(err => {
        console.log('BUNDLE_ACTIVE queryBundleStateInfoByInterval promise failed, because: ' + err.code);
    });

    // 异步方法callback方式
    stats.queryBundleStateInfoByInterval(0, 0, 20000000000000, (err, res) => {
        if (err) {
            console.log('BUNDLE_ACTIVE queryBundleStateInfoByInterval callback failed, because: ' + err.code);
        } else {
            console.log('BUNDLE_ACTIVE queryBundleStateInfoByInterval callback success.');
            for (let i = 0; i < res.length; i++) {
                console.log('BUNDLE_ACTIVE queryBundleStateInfoByInterval callback number : ' + (i + 1));
                console.log('BUNDLE_ACTIVE queryBundleStateInfoByInterval callback result ' + JSON.stringify(res[i]));
            }
        }
    });
    ```

6. 查询（无参）当前调用者应用的使用优先级群组，config.json中不需要配置权限。

    ```js
    import stats from '@ohos.bundleState'

    // promise方式
    stats.queryAppUsagePriorityGroup().then(res => {
        console.log('BUNDLE_ACTIVE queryAppUsagePriorityGroup promise succeeded. result: ' + JSON.stringify(res));
    }).catch(err => {
        console.log('BUNDLE_ACTIVE queryAppUsagePriorityGroup promise failed. because: ' + err.code);
    });

    // callback方式
    stats.queryAppUsagePriorityGroup((err, res) => {
        if (err) {
            console.log('BUNDLE_ACTIVE queryAppUsagePriorityGroup callback failed. because: ' + err.code);
        } else {
            console.log('BUNDLE_ACTIVE queryAppUsagePriorityGroup callback succeeded. result: ' + JSON.stringify(res));
        }
    });
    ```

7. 判断指定Bundle Name的应用当前是否是空闲状态，config.json中不需要配置权限，三方应用只能查询自身的空闲状态。

    ```js
    import stats from '@ohos.bundleState'

    // 异步方法promise方式
    stats.isIdleState("com.ohos.camera").then(res => {
        console.log('BUNDLE_ACTIVE isIdleState promise succeeded, result: ' + JSON.stringify(res));
    }).catch(err => {
        console.log('BUNDLE_ACTIVE isIdleState promise failed, because: ' + err.code);
    });

    // 异步方法callback方式
    stats.isIdleState("com.ohos.camera", (err, res) => {
        if (err) {
            console.log('BUNDLE_ACTIVE isIdleState callback failed, because: ' + err.code);
        } else {
            console.log('BUNDLE_ACTIVE isIdleState callback succeeded, result: ' + JSON.stringify(res));
        }
    });
    ```

8. 查询FA使用记录。返回数量最大不超过maxNum设置的值，若不传入maxNum参数，则默认maxNum为1000。config.json中需要配置权限：ohos.permission.BUNDLE_ACTIVE_INFO。

    ```js
    import stats from '@ohos.bundleState'

    // 异步方法promise方式
    stats.getRecentlyUsedModules(1000).then(res => {
        console.log('BUNDLE_ACTIVE getRecentlyUsedModules promise succeeded');
        for (let i = 0; i < res.length; i++) {
            console.log('BUNDLE_ACTIVE getRecentlyUsedModules promise number : ' + (i + 1));
            console.log('BUNDLE_ACTIVE getRecentlyUsedModules promise result ' + JSON.stringify(res[i]));
        }
    }).catch(err=> {
        console.log('BUNDLE_ACTIVE getRecentlyUsedModules promise failed, because: ' + err.code);
    });

    // 无maNum参数异步方法promise方式
    stats.getRecentlyUsedModules().then(res => {
        console.log('BUNDLE_ACTIVE getRecentlyUsedModules promise succeeded');
        for (let i = 0; i < res.length; i++) {
            console.log('BUNDLE_ACTIVE getRecentlyUsedModules promise number : ' + (i + 1));
            console.log('BUNDLE_ACTIVE getRecentlyUsedModules promise result ' + JSON.stringify(res[i]));
        }
    }).catch( err=> {
        console.log('BUNDLE_ACTIVE getRecentlyUsedModules promise failed, because: ' + err.code);
    });

    // 异步方法callback方式
    stats.getRecentlyUsedModules(1000, (err, res) => {
        if(err) {
            console.log('BUNDLE_ACTIVE getRecentlyUsedModules callback failed, because: ' + err.code);
        } else {
            console.log('BUNDLE_ACTIVE getRecentlyUsedModules callback succeeded.');
                for (let i = 0; i < res.length; i++) {
                    console.log('BUNDLE_ACTIVE getRecentlyUsedModules callback number : ' + (i + 1));
                    console.log('BUNDLE_ACTIVE getRecentlyUsedModules callback result ' + JSON.stringify(res[i]));
                }
            }
    });

    // 无maNum参数异步方法callback方式
    stats.getRecentlyUsedModules((err, res) => {
        if (err) {
            console.log('BUNDLE_ACTIVE getRecentlyUsedModules callback failed, because: ' + err.code);
        } else {
            console.log('BUNDLE_ACTIVE getRecentlyUsedModules callback succeeded.');
                for (let i = 0; i < res.length; i++) {
                    console.log('BUNDLE_ACTIVE getRecentlyUsedModules callback number : ' + (i + 1));
                    console.log('BUNDLE_ACTIVE getRecentlyUsedModules callback result ' + JSON.stringify(res[i]));
                }
            }
    });
    ```

9. 通过指定起始和结束时间查询所有应用的通知次数，config.json中需要配置权限：ohos.permission.BUNDLE_ACTIVE_INFO。

    ```js
    import stats from '@ohos.bundleState'

    // 异步方法promise方式
    stats.queryAppNotificationNumber(0, 20000000000000).then(res => {
        console.log('BUNDLE_ACTIVE queryAppNotificationNumber promise success.');
        console.log('BUNDLE_ACTIVE queryAppNotificationNumber promise result ' + JSON.stringify(res));
    }).catch(err => {
        console.log('BUNDLE_ACTIVE queryAppNotificationNumber promise failed, because: ' + err.code);
    });

    // 异步方法callback方式
    stats.queryAppNotificationNumber(0, 20000000000000, (err, res) => {
        if (err) {
            console.log('BUNDLE_ACTIVE queryAppNotificationNumber callback failed, because: ' + err.code);
        } else {
            console.log('BUNDLE_ACTIVE queryAppNotificationNumber callback success.');
            console.log('BUNDLE_ACTIVE queryAppNotificationNumber callback result ' + JSON.stringify(res));
        }
    });
    ```

10. 通过指定起始和结束时间查询系统事件（休眠、唤醒、解锁、锁屏）统计信息，config.json中需要配置权限：ohos.permission.BUNDLE_ACTIVE_INFO。

    ```js
    import stats from '@ohos.bundleState'

    // 异步方法promise方式
    stats.queryBundleActiveEventStates(0, 20000000000000).then(res => {
        console.log('BUNDLE_ACTIVE queryBundleActiveEventStates promise success.');
        console.log('BUNDLE_ACTIVE queryBundleActiveEventStates promise result ' + JSON.stringify(res));
    }).catch(err => {
        console.log('BUNDLE_ACTIVE queryBundleActiveEventStates promise failed, because: ' + err.code);
    });

    // 异步方法callback方式
    stats.queryBundleActiveEventStates(0, 20000000000000, (err, res) => {
        if (err) {
            console.log('BUNDLE_ACTIVE queryBundleActiveEventStates callback failed, because: ' + err.code);
        } else {
            console.log('BUNDLE_ACTIVE queryBundleActiveEventStates callback success.');
            console.log('BUNDLE_ACTIVE queryBundleActiveEventStates callback result ' + JSON.stringify(res));
        }
    });
    ```

11. 查询（无参）当前调用者应用的使用优先级群组，config.json中不需要配置权限。查询（有参）指定应用的使用优先级群组，config.json中需要配置权限：ohos.permission.BUNDLE_ACTIVE_INFO。

     ```js
     import stats from '@ohos.bundleState'

     // 无参异步方法promise方式
     stats.queryAppUsagePriorityGroup().then(res => {
         console.log('BUNDLE_ACTIVE queryAppUsagePriorityGroup promise succeeded. result: ' + JSON.stringify(res));
     }).catch(err => {
         console.log('BUNDLE_ACTIVE queryAppUsagePriorityGroup promise failed. because: ' + err.code);
     });

     // 无参异步方法callback方式
     stats.queryAppUsagePriorityGroup((err, res) => {
         if (err) {
             console.log('BUNDLE_ACTIVE queryAppUsagePriorityGroup callback failed. because: ' + err.code);
         } else {
             console.log('BUNDLE_ACTIVE queryAppUsagePriorityGroup callback succeeded. result: ' + JSON.stringify(res));
         }
     });

     // 有参异步promise方式
     stats.queryAppUsagePriorityGroup(this.bundleName).then(res => {
         console.log('BUNDLE_ACTIVE QueryPackageGroup promise succeeded. result: ' + JSON.stringify(res));
     }).catch(err => {
         console.log('BUNDLE_ACTIVE QueryPackageGroup promise failed. because: ' + err.code);
     });

     // 有参异步方法callback方式
     stats.queryAppUsagePriorityGroup(this.bundleName, (err, res) => {
         if (err) {
             console.log('BUNDLE_ACTIVE QueryPackageGroup callback failed. because: ' + err.code);
         } else {
             console.log('BUNDLE_ACTIVE QueryPackageGroup callback succeeded. result: ' + JSON.stringify(res));
         }
     });
     ```

11. 给应用名是bundleName的应用分组设置成newGroup，返回设置结果是否成功

    ```javascript
    import stats from '@ohos.bundleState'

    // 异步方法promise
    stats.setBundleGroup(this.bundleName, this.newGroup).then(() => {
        console.log('BUNDLE_ACTIVE SetBundleGroup promise succeeded.');
    }).catch( err => {
        console.log('BUNDLE_ACTIVE SetBundleGroup promise failed. because: ' + err.code);
    });
    // 异步方法callback
    stats.setBundleGroup(this.bundleName, this.newGroup, (err) => {
        if (err) {
            console.log('BUNDLE_ACTIVE SetBundleGroup callback failed. because: ' + err.code);
        } else {
            console.log('BUNDLE_ACTIVE SetBundleGroup callback succeeded.');
        }
    });
    ```

12. 注册应用分组变化监听回调，返回注册是否成功，当应用分组发生变化时，会给所有已注册的监听者返回回调信息

    ```javascript
    import stats from '@ohos.bundleState'

    // 异步方法promise形式
    let onBundleGroupChanged = (err,res) => {
        console.log('BUNDLE_ACTIVE onBundleGroupChanged RegisterGroupCallBack callback success.');
        console.log('BUNDLE_ACTIVE onBundleGroupChanged RegisterGroupCallBack result oldGroup is : ' + res.oldGroup);
        console.log('BUNDLE_ACTIVE onBundleGroupChanged RegisterGroupCallBack result newGroup is : ' + res.newGroup);
        console.log('BUNDLE_ACTIVE onBundleGroupChanged RegisterGroupCallBack result changeReason is : ' + res.newGroup);
        console.log('BUNDLE_ACTIVE onBundleGroupChanged RegisterGroupCallBack result userId is : ' + res.userId);
        console.log('BUNDLE_ACTIVE onBundleGroupChanged RegisterGroupCallBack result bundleName is : ' + res.bundleName);
    };
    stats.registerGroupCallBack(onBundleGroupChanged).then(() => {
        console.log('BUNDLE_ACTIVE RegisterGroupCallBack promise succeeded.');
    }).catch(err => {
        console.log('BUNDLE_ACTIVE RegisterGroupCallBack promise failed. because: ' + err.code);
    });
    // 异步方法callback形式
    let onBundleGroupChanged = (err,res) => {
        console.log('BUNDLE_ACTIVE onBundleGroupChanged RegisterGroupCallBack callback success.');
        console.log('BUNDLE_ACTIVE onBundleGroupChanged RegisterGroupCallBack result‘s oldGroup is : ' + res.oldGroup);
        console.log('BUNDLE_ACTIVE onBundleGroupChanged RegisterGroupCallBack result‘s newGroup is : ' + res.newGroup);
        console.log('BUNDLE_ACTIVE onBundleGroupChanged RegisterGroupCallBack result‘s changeReason is : ' + res.newGroup);
        console.log('BUNDLE_ACTIVE onBundleGroupChanged RegisterGroupCallBack result‘s userId is : ' + res.userId);
        console.log('BUNDLE_ACTIVE onBundleGroupChanged RegisterGroupCallBack result‘s bundleName is : ' + res.bundleName);
    };
    stats.registerGroupCallBack(onBundleGroupChanged, (err) => {
        if (err) {
            console.log('BUNDLE_ACTIVE RegisterGroupCallBack callback failed, because: ' + err.code);
        } else {
            console.log('BUNDLE_ACTIVE RegisterGroupCallBack callback success.');
        }
    });
    ```

13. 解除应用分组监听回调

    ```javascript
    import stats from '@ohos.bundleState'

    // promise
    stats.unRegisterGroupCallBack().then(() => {
        console.log('BUNDLE_ACTIVE UnRegisterGroupCallBack promise succeeded.');
    }).catch(err => {
        console.log('BUNDLE_ACTIVE UnRegisterGroupCallBack promise failed. because: ' + err.code);
    });
    // callback
    stats.unRegisterGroupCallBack((err) => {
        if (err) {
            console.log('BUNDLE_ACTIVE UnRegisterGroupCallBack callback failed, because: ' + err.code);
        } else {
            console.log('BUNDLE_ACTIVE UnRegisterGroupCallBack callback success.');
        }
    });
    ```
## 相关实例
针对设备使用信息统计，有以下相关实例可供参考：
- [`DeviceUsageStatistics`：设备使用信息统计（eTS）（API8）](https://gitee.com/openharmony/app_samples/tree/master/device/DeviceUsageStatistics)

