# Child Component Configuration


For a component that supports child components, for example, a container component, add the UI descriptions of the child components inside "{ ... }". The **\<Column>**,  **\<Row>**,  **\<Stack>**,  **\<Button>**,  **\<Grid>**, and **\<List>** components are container components.


- The following is a simple example of the **\<Column>** component:
  
  ```ts
  Column() {
      Text('Hello')
          .fontSize(100)
      Divider()
      Text(this.myText)
          .fontSize(100)
          .fontColor(Color.Red)
  }
  ```


- Multiple child components can be nested in the **\<Column>** component, as shown below:
  
  ```ts
  Column() {
      Column() {
          Button() {
              Text('+ 1')
          }.type(ButtonType.Capsule)
          .onClick(() => console.log ('+1 clicked!'))
          Image('1.jpg')
      }
      Divider()
      Column() {
          Button() {
              Text('+ 2')
          }.type(ButtonType.Capsule)
          .onClick(() => console.log ('+2 clicked!'))
          Image('2.jpg')
      }
      Divider()
      Column() {
          Button() {
              Text('+ 3')
          }.type(ButtonType.Capsule)
          .onClick(() => console.log('+3 clicked!'))
          Image('3.jpg')
      }
  }.alignItems(HorizontalAlign.Center) // center align components inside Column
  ```
