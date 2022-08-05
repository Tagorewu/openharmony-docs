# 管理应用窗口（FA模型）

## 基本概念

窗口沉浸式能力：指对状态栏、导航栏等系统窗口进行控制，减少状态栏导航栏等系统界面的突兀感，从而使用户获得最佳体验的能力。
沉浸式能力只在应用主窗口作为全屏窗口时生效。通常情况下，应用子窗口（弹窗、悬浮窗口等辅助窗口）和处于自由窗口下的应用主窗口无法使用沉浸式能力。

## 场景介绍

在FA模型下，管理应用窗口的典型场景有：

- 设置应用子窗口属性及目标页面

- 体验窗口沉浸式能力

以下分别介绍具体开发方式。


## 接口说明

上述场景涉及的常用接口如下表所示。更多API说明请参见[API参考](../reference/apis/js-apis-window.md)。

| 实例名 | 接口名 | 描述 |
| -------- | -------- | -------- |
| window静态方法 | create(id:string,type:WindowType,callback:AsyncCallback]&lt;Window&gt;):void | 创建子窗口。<br>此接口仅可在`FA`模型下使用。 |
| window静态方法 | getTopWindow(callback:AsyncCallback&lt;Window&gt;):void | 获取当前应用内最后显示的窗口。<br/>此接口仅可在`FA`模型下使用。 |
| window静态方法 | find(id:string,callback:AsyncCallback&lt;Window&gt;):void | 查找`id`所对应的窗口。 |
| Window | loadContent(path:string,callback:AsyncCallback&lt;void&gt;):void | 为当前窗口加载具体页面内容。 |
| Window | moveTo(x:number,y:number,callback:AsyncCallback&lt;void&gt;):void | 移动当前窗口。 |
| Window | setBackgroundColor(color:string,callback:AsyncCallback&lt;void&gt;):void | 设置窗口的背景色 |
| Window | setBrightness(brightness:number,callback:AsyncCallback&lt;void&gt;):void | 设置屏幕亮度值。 |
| Window | resetSize(width:number,height:number,callback:AsyncCallback&lt;void&gt;):void | 改变当前窗口大小。 |
| Window | setFullScreen(isFullScreen:boolean,callback:AsyncCallback&lt;void&gt;):void | 设置窗口是否全屏显示。 |
| Window | setLayoutFullScreen(isLayoutFullScreen:boolean,callback:AsyncCallback&lt;void&gt;):void | 设置窗口布局是否为全屏布局。 |
| Window | setSystemBarEnable(names:Array&lt;'status'\|'navigation'&gt;):Promise&lt;void&gt; | 设置导航栏、状态栏是否显示。 |
| Window | setSystemBarProperties(systemBarProperties:SystemBarProperties,callback:AsyncCallback&lt;void&gt;):void | 设置窗口内导航栏、状态栏属性。<br/>`systemBarProperties`：导航栏、状态栏的属性集合。 |
| Window | show(callback: AsyncCallback\<void>): void | 显示当前窗口。 |
| Window | on(type:'touchOutside',callback:Callback&lt;void&gt;):void | 开启本窗口区域外的点击事件的监听。 |
| Window | destroy(callback: AsyncCallback&lt;void&gt;):void | 销毁当前窗口。 |


## 设置应用子窗口

开发者可以按需创建应用子窗口，如弹窗等，并对其进行属性设置等操作。


### 开发步骤

1. 创建/获取子窗口对象。

   - 可以通过`window.create`接口创建子窗口。
   - 可以通过`window.getTopWindow`来获取最后显示的窗口得到子窗口。
   - 也可以通过`window.find`接口来查找已经创建的窗口从而得到子窗口。

   ```js
   import window from '@ohos.window';
   
   var windowClass = null;
   // 1.方式一：创建子窗口。
   window.create("subWindow", window.WindowType.TYPE_APP, (err, data) => {
       if (err.code) {
           console.error('Failed to create the subWindow. Cause: ' + JSON.stringify(err));
           return;
       }
       console.info('Succeeded in creating subWindow. Data: ' + JSON.stringify(data));
       windowClass = data;
   });
   // 1.方式二：获取子窗口。
   window.getTopWindow((err, data) => {
       if (err.code) {
           console.error('Failed to get the subWindow. Cause: ' + JSON.stringify(err));
           return;
       }
       console.info('Succeeded in getting subWindow. Data: ' + JSON.stringify(data));
       windowClass = data;
   });
   // 1.方式三：查找得到子窗口。
   window.find("subWindow", (err, data) => {
       if (err.code) {
           console.error('Failed to find the subWindow. Cause: ' + JSON.stringify(err));
           return;
       }
       console.info('Succeeded in finding subWindow. Data: ' + JSON.stringify(data));
       windowClass = data;
   });
   ```
   
2. 设置子窗口属性。

   子窗口创建成功后，可以改变其大小、位置等，还可以根据应用需要设置窗口背景色、亮度等属性。

   
   ```js
   // 2.移动子窗口位置。
   windowClass.moveTo(300, 300, (err, data) => {
     if (err.code) {
       console.error('Failed to move the window. Cause:' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in moving the window. Data: ' + JSON.stringify(data));
   });
   // 2.改变子窗口大小。
   windowClass.resetSize(500, 1000, (err, data) => {
     if (err.code) {
       console.error('Failed to change the window size. Cause:' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in changing the window size. Data: ' + JSON.stringify(data));
   });
   ```

3. 加载显示子窗口的具体内容。

   使用`loadContent`和`show`接口加载显示子窗口的具体内容。

   
   ```js
   // 3.为子窗口加载对应的目标页面。
   windowClass.loadContent("pages/page2", (err, data) => {
       if (err.code) {
           console.error('Failed to load the content. Cause: ' + JSON.stringify(err));
           return;
       }
       console.info('Succeeded in loading the content. Data: ' + JSON.stringify(data));
       // 3.显示子窗口。
       windowClass.show((err, data) => {
        if (err.code) {
               console.error('Failed to show the window. Cause: ' + JSON.stringify(err));
               return;
           }
           console.info('Succeeded in showing the window. Data: ' + JSON.stringify(data));
       });
   });
   ```
   
4. 销毁子窗口。

   当不再需要某些子窗口时，可根据场景的具体实现逻辑，使用`destroy`接口销毁子窗口。

   
   ```js
   // 4.销毁子窗口。当不再需要某些子窗口时，可根据场景的具体实现逻辑，使用destroy接口销毁子窗口，此处以监听窗口区域外的点击事件实现子窗口的销毁。
   windowClass.on('touchOutside', () => {
       console.info('touch outside');
       windowClass.destroy((err, data) => {
           if (err.code) {
               console.error('Failed to destroy the subwindow. Cause:' + JSON.stringify(err));
               return;
           }
           console.info('Succeeded in destroying the subwindow. Data: ' + JSON.stringify(data));
       });
   });
   ```


## 体验窗口沉浸式能力

在看视频、玩游戏等场景下，用户往往希望隐藏状态栏、导航栏等不必要的系统窗口，从而获得更佳的沉浸式体验。此时可以借助窗口沉浸式能力（窗口沉浸式能力都是针对应用主窗口而言的），达到预期效果。


### 开发步骤

1. 获取主窗口对象。

   沉浸式能力需要在成功获取应用主窗口对象的前提下进行。使用`window.getTopWindow`接口来获取得到主窗口。

   
   ```js
   import window from '@ohos.window';
   
   var mainWindowClass = null;
   // 1.获取主窗口
   window.getTopWindow((err, data) => {
     if (err.code) {
       console.error('Failed to get the subWindow. Cause: ' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in getting subWindow. Data: ' + JSON.stringify(data));
     mainWindowClass = data;
   });
   ```

2. 实现沉浸式效果。有以下三种方式：

   - 方式一：调用`setFullScreen`接口，设置应用主窗口为全屏显示，此时导航栏、状态栏将隐藏，从而达到沉浸式效果。
   - 方式二：调用`setSystemBarEnable`接口，设置导航栏、状态栏不显示，从而达到沉浸式效果。
   - 方式三：调用`setLayoutFullScreen`接口，设置应用主窗口为全屏布局；然后调用`setSystemPropertites`接口，设置导航栏、状态栏的透明度、背景/文字颜色以及高亮图标等属性，使之保持与主窗口显示协调一致，从而达到沉浸式效果。

   ```js
   // 2.实现沉浸式效果。方式一：设置窗口全屏显示。
   var isFullScreen = true;
   mainWindowClass.setFullScreen(isFullScreen, (err, data) => {
     if (err.code) {
       console.error('Failed to enable the full-screen mode. Cause:' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in enabling the full-screen mode. Data: ' + JSON.stringify(data));
   });
   // 2.实现沉浸式效果。方式二：设置导航栏、状态栏不显示。
   var names = null;
   mainWindowClass.setSystemBarEnable(names, (err, data) => {
     if (err.code) {
       console.error('Failed to set the system bar to be visible. Cause:' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in setting the system bar to be visible. Data: ' + JSON.stringify(data));
   });
   // 2.实现沉浸式效果。
   //方式三：设置窗口为全屏布局，配合设置状态栏、导航栏的透明度、背景/文字颜色及高亮图标等属性，与主窗口显示保持协调一致。
   var isLayoutFullScreen = true;
   mainWindowClass.setLayoutFullScreen(isLayoutFullScreen, (err, data) => {
     if (err.code) {
       console.error('Failed to set the window layout to full-screen mode. Cause:' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in setting the window layout to full-screen mode. Data: ' + JSON.stringify(data));
   });
   var SystemBarProperties = {
     statusBarColor: '#ff00ff',
     navigationBarColor: '#00ff00',
     //以下两个属性从API Version7开始支持
     isStatusBarLightIcon: false,
     isNavigationBarLightIcon: false,
     //以下两个属性从API Version8开始支持
     statusBarContentColor: '#ffffff',
     navigationBarContentColor: '#ffffff'
   };
   mainWindowClass.setSystemBarProperties(SystemBarProperties, (err, data) => {
     if (err.code) {
       console.error('Failed to set the system bar properties. Cause: ' + JSON.stringify(err));
       return;
     }
     console.info('Succeeded in setting the system bar properties. Data: ' + JSON.stringify(data));
   });
   ```
   
3. 加载显示沉浸式窗口的具体内容。

   使用`loadContent`和`show`接口加载显示沉浸式窗口的具体内容。

   
   ```js
   // 3.为沉浸式窗口加载对应的目标页面。
   mainWindowClass.loadContent("pages/page3", (err, data) => {
       if (err.code) {
           console.error('Failed to load the content. Cause: ' + JSON.stringify(err));
           return;
       }
       console.info('Succeeded in loading the content. Data: ' + JSON.stringify(data));
       // 3.显示沉浸式窗口。
       mainWindowClass.show((err, data) => {
           if (err.code) {
               console.error('Failed to show the window. Cause: ' + JSON.stringify(err));
               return;
           }
           console.info('Succeeded in showing the window. Data: ' + JSON.stringify(data));
       });
   });
   ```

