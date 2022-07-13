# 定时器


## setTimeout

setTimeout(handler[,delay[,…args]]): number

设置一个定时器，该定时器在定时器到期后执行一个函数。

- 参数
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | handler | Function | 是 | 定时器到期后执行函数。 |
  | delay | number | 否 | 延迟的毫秒数，函数的调用会在该延迟之后发生。如果省略该参数，delay取默认值0，意味着“马上”执行，或尽快执行。 |
  | ...args | Array&lt;any&gt; | 否 | 附加参数，一旦定时器到期，它们会作为参数传递给handler。 |

- 返回值
  | 类型 | 说明 |
  | -------- | -------- |
  | number | timeout定时器的ID。 |

- 示例
  ```js
  export default {    
    setTimeOut() {        
      var timeoutID = setTimeout(function() {            
        console.log('delay 1s');
      }, 1000);    
    }
  }
  ```


## clearTimeout

clearTimeout(timeoutID: number): void

取消了先前通过调用setTimeout()建立的定时器。

- 参数
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | timeoutID | number | 是 | 要取消定时器的ID，&nbsp;是由setTimeout()返回的。 |

- 示例
  ```js
  export default {    
    clearTimeOut() {        
      var timeoutID = setTimeout(function() {            
        console.log('do after 1s delay.');        
      }, 1000);        
      clearTimeout(timeoutID);    
    }
  }
  ```


## setInterval

setInterval(handler[, delay[, ...args]]): number

重复调用一个函数，在每次调用之间具有固定的时间延迟。

- 参数
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | handler | Function | 是 | 要重复调用的函数。 |
  | delay | number | 否 | 延迟的毫秒数（一秒等于1000毫秒），函数的调用会在该延迟之后发生。 |
  | ...args | Array&lt;any&gt; | 否 | 附加参数，一旦定时器到期，他们会作为参数传递给handler。 |

- 返回值
  | 类型 | 说明 |
  | -------- | -------- |
  | number | intervalID重复定时器的ID。 |

- 示例
  ```js
  export default {    
    setInterval() {        
      var intervalID = setInterval(function() {            
        console.log('do very 1s.');        
      }, 1000);    
    }
  }
  ```


## clearInterval

clearInterval(intervalID: number): void

可取消先前通过 setInterval() 设置的重复定时任务。

- 参数
  | 参数名 | 类型 | 必填 | 说明 |
  | -------- | -------- | -------- | -------- |
  | intervalID | number | 是 | 要取消的重复定时器的ID，是由&nbsp;setInterval()&nbsp;返回的。 |

- 示例
  ```js
  export default {    
    clearInterval() {        
      var intervalID = setInterval(function() {
        console.log('do very 1s.');
      }, 1000);
      clearInterval(intervalID);
    }
  }
  ```

