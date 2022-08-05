# ForEach

The development framework provides **ForEach** to iterate arrays and create components for each array item. If a large number of elements are involved in **ForEach**, the page loading may become slow. For best possible results, you are advised to use **[LazyForEach](ts-rending-control-syntax-lazyforeach.md)** instead. **ForEach** is defined as follows:


```ts
ForEach(
    arr: any[], // Array to be iterated
    itemGenerator: (item: any, index?: number) => void, // child component generator
    keyGenerator?: (item: any, index?: number) => string // (optional) Unique key generator, which is recommended.
)
```


## ForEach


ForEach(arr: any[],itemGenerator: (item: any, index?: number) =&gt; void, keyGenerator?: (item: any, index?: number) =&gt; string):void


Table 1 Parameters

| Name          | Type                                    | Mandatory  | Default Value | Description                                    |
| ------------- | ---------------------------------------- | ---- | ---- | ---------------------------------------- |
| arr           | any[]                                    | Yes   | -    | Must be an array. An empty array is allowed. If the array is empty, no child component is created. The functions that return array-type values are also allowed, for example, **arr.slice (1, 3)**. The set functions cannot change any state variables including the array itself, such as **Array.splice**, **Array.sort**, and **Array.reverse**.|
| itemGenerator | (item: any, index?: number) =&gt; void | Yes   | -    | Lambda function used to generate one or more child components for a given array item. A component and its child component list must be enclosed in braces ({...}).|
| keyGenerator  | (item: any, index?: number) =&gt; string | No   | -    | Anonymous parameter used to generate a unique and stable key value for a given array item. When the position of a subitem in the array is changed, the key value of the subitem cannot be changed. When a subitem in the array is replaced with a new item, the key value of the current item must be different from that of the new item. This key-value generator is optional. However, for performance reasons, it is strongly recommended that the key-value generator be provided, so that the development framework can better identify array changes. If the array is reversed while no key-value generator is provided, all nodes in **ForEach** will be rebuilt.|


> **NOTE**
> - **ForEach** must be used in container components.
>
> - The generated child components are allowed in the parent container component of **ForEach**. The child component generator function can contain the **if/else** conditional statement, and the **if/else** conditional statement can contain **ForEach**.
>
> - The call sequence of subitem generator functions may be different from that of the data items in the array. During the development, do not assume whether the subitem generator and key value generator functions are executed and the execution sequence. Below is an example of incorrect usage:
>   ```ts
>   ForEach(anArray, item => {Text(`${++counter}. item.label`)})
>   ```
>
>   Below is an example of correct usage:
>
>   ```ts
>   ForEach(anArray.map((item1, index1) => { return { i: index1 + 1, data: item1 }; }), 
>           item => Text(`${item.i}. item.data.label`),
>           item => item.data.id.toString())
>   ```


## Example

The following is an example of a simple-type array:

```ts
// xxx.ets
@Entry
@Component
struct MyComponent {
    @State arr: number[] = [10, 20, 30]
    build() {
        Column() {
            Button() {
                Text('Reverse Array')
            }.onClick(() => {
                this.arr.reverse()
            })

            ForEach(this.arr,                         // Parameter 1: array to be iterated
                    (item: number) => {               // Parameter 2: item generator
                        Text(`item value: ${item}`)
                        Divider()
                    },
                    (item: number) => item.toString() // Parameter 3: unique key generator, which is optional but recommended.
            )
        }
    }
}
```

The following is an example of a complex-type array:
```ts
// xxx.ets
class Month {
  year: number
  month: number
  days: Array<number>

  constructor(year, month, days) {
    this.year = year;
    this.month = month;
    this.days = days;
  }
}

@Entry
@Component
struct Calendar1 {
// simulate with 6 months
  @State calendar: Month[] = [
    new Month(2020, 1, [...Array(31).keys()]),
    new Month(2020, 2, [...Array(28).keys()]),
    new Month(2020, 3, [...Array(31).keys()]),
    new Month(2020, 4, [...Array(30).keys()]),
    new Month(2020, 5, [...Array(31).keys()]),
    new Month(2020, 6, [...Array(30).keys()]),
  ]

  build() {
    Column() {
      Button('next month')
        .onClick(() => {
          this.calendar.shift()
          this.calendar.push({
            year: 2020,
            month: 7,
            days: [...Array(31)
              .keys()]
          })
        })
      ForEach(this.calendar,
        (item: Month) => {
          Text('month:' + item.month)
            .fontSize(30)
            .padding(20)
          Grid() {
            ForEach(item.days,
              (day: number) => {
                GridItem() {
                  Text((day + 1).toString())
                    .fontSize(30)
                }
              },
              (day: number) => day.toString())
          }
          .columnsTemplate('1fr 1fr 1fr 1fr 1fr 1fr 1fr')
          .rowsGap(20)
        },
        // field is used together with year and month as the unique ID of the month.
        (item: Month) => (item.year * 12 + item.month).toString())
    }
  }
}
```
