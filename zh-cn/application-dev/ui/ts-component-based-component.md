# @Component

@Component装饰的struct表示该结构体具有组件化能力，能够成为一个独立的组件，这种类型的组件也称为自定义组件，在build方法里描述UI结构。自定义组件具有以下特点：


- 可组合：允许开发人员组合使用内置组件、其他组件、公共属性和方法；
- 链式调用<sup>9+</sup>：通过链式调用通用属性改变组件样式；
- 可重用：自定义组件可以被其他组件重用，并作为不同的实例在不同的父组件或容器中使用；
- 生命周期：生命周期的回调方法可以在组件中配置，用于业务逻辑处理；
- 数据驱动更新：由状态变量的数据驱动，实现UI自动更新。


对组件化的深入描述，请参考[深入理解组件化](ts-custom-component-initialization.md)。


>  **说明：**
>
>  - 自定义组件必须定义build方法。
>- 自定义组件禁止自定义构造函数。 


如下代码定义了MyComponent组件：


```ts
@Component
struct MyComponent {
    build() {
        Column() {
            Text('my component')
                .fontColor(Color.Red)
        }.alignItems(HorizontalAlign.Center) // center align Text inside Column
    }
}
```


MyComponent的build方法会在初始渲染时执行，此外，当组件中的状态发生变化时，build方法将再次执行。


以下代码使用了MyComponent组件：


```ts
@Component
struct ParentComponent {
    build() {
        Column() {
            MyComponent()
            Text('we use component')
                .fontSize(20)
        }
    }
}
```


可以多次使用MyComponent，并在不同的组件中进行重用：


```ts
@Component
struct ParentComponent {
    build() {
        Row() {
            Column() {
                MyComponent()
                Text('first column')
                    .fontSize(20)
            }
            Column() {
                MyComponent()
                Text('second column')
                    .fontSize(20)
            }
        }
    }

    aboutToAppear() {
        console.log('ParentComponent: Just created, about to become rendered first time.')
    }

    aboutToDisappear() {
        console.log('ParentComponent: About to be removed from the UI.')
    }
}
```

可链式通用属性，使组件样式多样化：

> **说明：** 从API version 9开始支持。
>
> 自定义组件链式调用暂不支持尾随闭包写法(在初始化自定义组件时，组件名称紧跟一个大括号“{}”形成尾随闭包场景(Inedx(){})。开发者可把尾随闭包看做一个容器，向其填充内容，如在闭包内增加组件{Column(){Text("content")} )。

```ts
@Entry
@Component
struct Index {
  @State bannerValue: string = 'Hello,world';
  build() {
    Column() {
      Chind({ ChindBannerValue:$bannerValue })
      .height(60)
      .width(250)
      .border({ width:5, color:Color.Red, radius:10, style: BorderStyle.Dotted })
    }
  }
}

@Component
struct Chind {
  @Link ChindBannerValue: string;
  build() {
    Column() {
      Text(this.ChindBannerValue)
      .fontSize(30)
    }
  }
}
```

