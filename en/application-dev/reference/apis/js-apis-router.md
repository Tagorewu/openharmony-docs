# Page Routing

The **Router** module provides APIs to access pages through URLs. You can use the APIs to navigate to a specified page in an application, replace the current page with another one in an application, and return to the previous page or a specified page.

> **NOTE**
>
> - The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> - Page routing APIs can be invoked only after page rendering is complete. Do not call these APIs in **onInit** and **onReady** when the page is still in the rendering phase.

## Modules to Import

```
import router from '@ohos.router'
```

## router.push

push(options: RouterOptions): void

Navigates to a specified page in the application.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**
| Name    | Type                             | Mandatory  | Description       |
| ------- | ------------------------------- | ---- | --------- |
| options | [RouterOptions](#routeroptions) | Yes   | Page routing parameters.|


**Example**
```js
router.push({
  url: 'pages/routerpage2',
  params: {
    data1: 'message',
    data2: {
      data3: [123, 456, 789]
    },
  },
});
```
## router.push<sup>9+</sup>

push(options: RouterOptions, mode: RouterMode): void

Navigates to a specified page in the application.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**
| Name    | Type                             | Mandatory  | Description        |
| ------- | ------------------------------- | ---- | ---------- |
| options | [RouterOptions](#routeroptions) | Yes   | Page routing parameters. |
| mode    | [RouterMode](#routermode9)      | Yes   | Routing mode.|


**Example**
```js
router.push({
  url: 'pages/routerpage2/routerpage2',
  params: {
    data1: 'message',
    data2: {
      data3: [123, 456, 789]
    },
  },
},router.RouterMode.Standard);
```

## router.replace

replace(options: RouterOptions): void

Replaces the current page with another one in the application and destroys the current page.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**

| Name | Type                           | Mandatory| Description              |
| ------- | ------------------------------- | ---- | ------------------ |
| options | [RouterOptions](#routeroptions) | Yes  | Description of the new page.|

**Example**

```js
router.replace({
  url: 'pages/detail',
  params: {
    data1: 'message',
  },
});
```

  ## router.replace<sup>9+</sup>

replace(options: RouterOptions, mode: RouterMode): void

Replaces the current page with another one in the application and destroys the current page.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**
| Name    | Type                             | Mandatory  | Description        |
| ------- | ------------------------------- | ---- | ---------- |
| options | [RouterOptions](#routeroptions) | Yes   | Description of the new page. |
| mode    | [RouterMode](#routermode9)      | Yes   | Routing mode.|

**Example**

```js
router.replace({
  url: 'pages/detail/detail',
  params: {
    data1: 'message',
  },
}, router.RouterMode.Standard);
```

## router.back

back(options?: RouterOptions ): void

Returns to the previous page or a specified page.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**
| Name | Type                           | Mandatory| Description                                                        |
| ------- | ------------------------------- | ---- | ------------------------------------------------------------ |
| options | [RouterOptions](#routeroptions) | No  | Description of the page. The **url** parameter indicates the URL of the page to return to. If the specified page does not exist in the page stack, the application does not respond. If no URL is set, the previous page is returned. |

**Example**

```js
router.back({url:'pages/detail'});    
```

## router.clear

clear(): void

Clears all historical pages in the stack and retains only the current page at the top of the stack.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Example**

```js
router.clear();    
```

## router.getLength

getLength(): string

Obtains the number of pages in the current stack.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**
| Type    | Description                |
| ------ | ------------------ |
| string | Number of pages in the stack. The maximum value is **32**.|

**Example**
```js
var size = router.getLength();        
console.log('pages stack size = ' + size);    
```

## router.getState

getState(): RouterState

Obtains state information about the current page.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type                         | Description     |
| --------------------------- | ------- |
| [RouterState](#routerstate) | Page routing state.|
**Example**

```js
var page = router.getState();
console.log('current index = ' + page.index);
console.log('current name = ' + page.name);
console.log('current path = ' + page.path);
```

## RouterState

Describes the page routing state.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name   | Type    | Description                                |
| ----- | ------ | ---------------------------------- |
| index | number | Index of the current page in the stack. The index starts from 1 from the bottom to the top of the stack.|
| name  | string | Name of the current page, that is, the file name.                 |
| path  | string | Path of the current page.                        |

## router.enableAlertBeforeBackPage

enableAlertBeforeBackPage(options: EnableAlertOptions): void

Enables the display of a confirm dialog box before returning to the previous page.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Parameters**
| Name    | Type                                      | Mandatory  | Description       |
| ------- | ---------------------------------------- | ---- | --------- |
| options | [EnableAlertOptions](#enablealertoptions) | Yes   | Description of the dialog box.|

**Example**

  ```js        
  router.enableAlertBeforeBackPage({            
    message: 'Message Info'        
  });    
  ```
## EnableAlertOptions

Describes the confirm dialog box.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name     | Type    | Mandatory  | Description      |
| ------- | ------ | ---- | -------- |
| message | string | Yes   | Content displayed in the confirm dialog box.|

## router.disableAlertBeforeBackPage

disableAlertBeforeBackPage(): void

Disables the display of a confirm dialog box before returning to the previous page.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Example**
```js
router.disableAlertBeforeBackPage();    
```

##  router.getParams

getParams(): Object

Obtains the parameters passed from the page that initiates redirection to the current page.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

**Return value**

| Type    | Description               |
| ------ | ----------------- |
| Object | Parameters passed from the page that initiates redirection to the current page.|

**Example**

```
router.getParams();
```

## RouterOptions

Describes the page routing options.

**System capability**: SystemCapability.ArkUI.ArkUI.Lite

| Name    | Type    | Mandatory  | Description                                      |
| ------ | ------ | ---- | ---------------------------------------- |
| url    | string | Yes   | URI of the destination page, in either of the following formats:<br>- Absolute path of the page. The value is available in the pages list in the **config.json** file, for example:<br>- pages/index/index<br>- pages/detail/detail<br>- Particular path. If the URI is a slash (/), the home page is displayed.|
| params | Object | No   | Data that needs to be passed to the destination page during redirection. After the destination page is displayed, it can use the passed data, for example, **this.data1** (**data1** is a key in **params**). If there is the same key (for example, **data1**) on the destination page, the passed **data1** value will replace the original value on the destination page.|


  > **NOTE**
  > The page routing stack supports a maximum of 32 pages.

## RouterMode<sup>9+</sup>

Enumerates the routing modes.

**System capability**: SystemCapability.ArkUI.ArkUI.Full

| Name      | Description                                      |
| -------- | ---------------------------------------- |
| Standard | Standard mode.                                   |
| Single   | Singleton mode.<br>If the URL of the target page already exists in the page stack, the page closest to the top of the stack is moved as a new page to the top of the stack.<br>If the URL of the target page does not exist in the page stack, the page is redirected to in standard mode.|

## Examples

### JavaScript-based Web-like Development Paradigm

```js
// Current page
export default {
  pushPage() {
    router.push({
      url: 'pages/detail/detail',
      params: {
        data1: 'message',
      },
    });
  }
}
```
```js
// detail page
export default {
  onInit() {
    console.info('showData1:' + router.getParams()[data1]);
  }
}
```

### TypeScript-based Declarative Development Paradigm

```ts
// Navigate to the target page through router.push with the params parameter carried.
import router from '@ohos.router'

@Entry
@Component
struct Index {
  async  routePage() {
    let options = {
      url: 'pages/second',
      params: {
        text: 'This is the value on the first page.',
        data: {
          array: [12, 45, 78]
        },
      }
    }
    try {
      await router.push(options)
    } catch (err) {
      console.info(` fail callback, code: ${err.code}, msg: ${err.msg}`)
    }
  }

  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
        Text('This is the first page.')
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
      Button() {
        Text('next page')
          .fontSize(25)
          .fontWeight(FontWeight.Bold)
      }.type(ButtonType.Capsule)
          .margin({ top: 20 })
          .backgroundColor('#ccc')
          .onClick(() => {
            this.routePage()
      })
    }
    .width('100%')
    .height('100%')
  }
}
```

```ts
// Receive the transferred parameters on the second page.
import router from '@ohos.router'

@Entry
@Component
struct Second {
  private content: string = "This is the second page."
  @State text: string = router.getParams()['text']
  @State data: any = router.getParams()['data']
  @State secondData : string = ''
  
  build() {
    Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
      Text(`${this.content}`)
        .fontSize(50)
        .fontWeight(FontWeight.Bold)
      Text(this.text)
        .fontSize(30)
        .onClick(()=>{
          this.secondData = (this.data.array[1]).toString()
        })
      .margin({top:20})
      Text('Value from the first page '+'' + this.secondData)
        .fontSize(20)
        .margin({top:20})
        .backgroundColor('red')      
    }
    .width('100%')
    .height('100%')
  }
}
```
