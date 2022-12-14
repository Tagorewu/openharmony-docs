# ErrorManager

ErrorManager模块提供对错误观察器的注册和注销的能力。

> **说明：**
> 
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块
```
import errorManager from '@ohos.application.errorManager'
```

## ErrorManager.registerErrorObserver

registerErrorObserver(observer: ErrorObserver): number;

注册错误观测器。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**
 
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| observer | [ErrorObserver](#errorobserver) | 否 | 返回观察者的数字代码。 |

**示例：**
    
```js
var observer = {
    onUnhandledException(errorMsg) {
        console.log('onUnhandledException, errorMsg: ', errorMsg)
    }
}
errorManager.registerErrorObserver(observer)
```

## ErrorManager.unregisterErrorObserver

unregisterErrorObserver(observerId: number,  callback: AsyncCallback\<void>): void;

注销错误观测器。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**
 
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| observerId | number | 否 | 返回观察者的数字代码。 |
| callback | AsyncCallback\<void> | 否 | 表示指定的回调方法。 |

**示例：**
    
```js
var observerId = 100;

function unregisterErrorObserverCallback(err) {
    if (err) {
        console.log('------------ unregisterErrorObserverCallback ------------', err);
    }
}
errorManager.unregisterErrorObserver(observerId, unregisterErrorObserverCallback);

```

## ErrorManager.unregisterErrorObserver

unregisterErrorObserver(observerId: number): Promise\<void>;

注销错误观测器。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**
 
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| observerId | number | 否 | 返回观察者的数字代码。 |

**返回值：**

| 类型 | 说明 |
| -------- | -------- |
| Promise\<void> | 返回执行结果。 |

**示例：**
    
```js
var observerId = 100;
errorManager.unregisterErrorObserver(observerId)
.then((data) => {
    console.log('----------- unregisterErrorObserver success ----------', data);
})
.catch((err) => {
    console.log('----------- unregisterErrorObserver fail ----------', err);
})

```

## ErrorObserver

onUnhandledException(errMsg: string): void;

将在js运行时引发用户未捕获的异常时调用。

**系统能力**：SystemCapability.Ability.AbilityRuntime.Core

**参数：**
 
| 参数名 | 类型 | 必填 | 说明 |
| -------- | -------- | -------- | -------- |
| errMsg | string | 否 | 有关异常的消息和错误堆栈跟踪。 |

**示例：**
    
```js
var observer = {
    onUnhandledException(errorMsg) {
        console.log('onUnhandledException, errorMsg: ', errorMsg)
    }
}
errorManager.registerErrorObserver(observer)
```