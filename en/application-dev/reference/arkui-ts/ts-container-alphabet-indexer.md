# AlphabetIndexer

The **\<Indexer>** component can create a logically indexed array of items in a container for instant location.

>  **NOTE**
>
>  This component is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.

## Required Permissions

None


## Child Components

Not supported


## APIs

AlphabetIndexer(value: {arrayValue : Array&lt;string&gt;, selected : number})

- Parameters
  | Name| Type| Mandatory| Default Value| Description|
  | -------- | -------- | -------- | -------- | -------- |
  | arrayValue | Array&lt;string&gt; | Yes| - | Array of strings to be displayed in the alphabetic index bar.|
  | selected | number | Yes| - | ID of a selected item.|


## Attributes

| Name| Type| Description|
| -------- | -------- | -------- |
| selectedColor | [ResourceColor](../../ui/ts-types.md) | Font color of the selected text.|
| popupColor | [ResourceColor](../../ui/ts-types.md) | Font color of the pop-up text.|
| selectedBackgroundColor | [ResourceColor](../../ui/ts-types.md) | Background color of the selected text.|
| popupBackground | [ResourceColor](../../ui/ts-types.md) | Background color of the pop-up text.|
| usingPopup | boolean | Whether to use pop-up text.|
| selectedFont | {<br>size?: number,<br>weight?: FontWeight,<br>family?: string,<br>style?: FontStyle<br>} | Font style of the selected text.|
| popupFont | {<br>size?: number,<br>weight?: FontWeight,<br>family?: string,<br>style?: FontStyle<br>} | Font style of the pop-up text.|
| font | {<br>size?: number,<br>weight?: FontWeight,<br>family?: string,<br>style?: FontStyle<br>} | Default font style of the alphabetic index bar.|
| itemSize | Length | Size of an item in the alphabetic index bar. The item is a square, and the side length needs to be set.|
| alignStyle | IndexerAlign | Alignment style of the alphabetic index bar. Left alignment and right alignment are supported. The alignment style affects the position of the pop-up window.|

- IndexerAlign enums
  | Name| Description|
  | -------- | -------- |
  | Left | The pop-up window is displayed on the right of the alphabetic indexer bar.|
  | Right | The pop-up window is displayed on the left of the alphabetic indexer bar.|


## Events

| Name| Description|
| -------- | -------- |
| onSelected(index: number) =&gt; void<sup>(deprecated) </sup>| Invoked when an item in the alphabetic indexer bar is selected.|
| onSelect(index: number) =&gt; void<sup>8+</sup> | Invoked when an item in the alphabetic indexer bar is selected.|
| onRequestPopupData(callback: (index: number) =&gt; Array&lt;string&gt;)<sup>8+</sup> | Invoked when a request for displaying content in the index prompt window is sent when an item in the alphabetic indexer bar is selected.<br>The return value is a string array corresponding to the indexes. The string array is displayed vertically in the pop-up window. It can display up to five strings at a time and allows scrolling.|
| onPopupSelect(callback: (index: number) =&gt; void)<sup>8+</sup> | Invoked when an item in the index pop-up window is selected.|


## Example

```ts
// xxx.ets
@Entry
@Component
struct AlphabetIndexerSample {
  private value: string[] = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I', 'J', 'K', 'L', 'M', 'N', 'O', 'P', 'Q', 'R', 'S', 'T', 'U', 'V', 'W', 'X', 'Y', 'Z']

  build() {
    AlphabetIndexer({ arrayValue: this.value, selected: 0 })
      .selectedColor(0xffffff) // Font color of the selected text
      .popupColor(0xFFFAF0) // Font color of the pop-up text
      .selectedBackgroundColor(0xCCCCCC) // Background color of the selected text
      .popupBackground(0xD2B48C) // Background color of the pop-up text
      .usingPopup(true) // Whether to use pop-up text
      .selectedFont({ size: 16, weight: FontWeight.Bolder }) // Font style of the selected text
      .popupFont({ size: 30, weight: FontWeight.Bolder }) // Font style of the pop-up text
      .itemSize(28) // Size of each item (square)
      .alignStyle(IndexerAlign.Left) // Left aligned
      .onSelect((index: number) => {
        console.info(this.value[index] + 'Selected') // Event indicating that an item is selected
      })
      .margin({ left: 50 })
  }
}
```

![en-us_image_0000001212378392](figures/en-us_image_0000001212378392.gif)
