## 状态管理
#### `@Prop`父传子
`@Prop`定义变量
```js
 @Prop content:string
```
例：
```js
@Entry
@Component
struct Index {
  // State必须要进行初始化
  @State message: string ='你好'

  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
        Button('点击')
          .fontSize(40)
          .onClick(()=>{
            this.message= this.message  === '你好'? '再见' : '你好';
          })
        StateProp({content:this.message})

      }

    }

  }
}


// 子组件
@Component
struct StateProp{
  @Prop content:string
  build(){
    Column(){
      Text(this.content)
        .fontSize(30)
        .fontColor(Color.Green)
    }
  }
}

```
效果：
![Alt text](assets/HarmonyOS4.0%E7%B3%BB%E5%88%97%E2%80%94%E2%80%9405%E3%80%81%E7%8A%B6%E6%80%81%E7%AE%A1%E7%90%86/recording.gif)

**@Prop是单向传递。父可以到子，子不可以到父**


```
@Entry
@Component
struct Index {
  // State必须要进行初始化
  @State message: string ='Southern Wind'

  build() {
    Row() {
      Column() {
        Text(this.message)
          .textStyle()
        Button('点击')
          .btnStyle()
          .backgroundColor(Color.Black)

          .onClick(()=>{
            this.message= this.message  === 'Southern Wind'? '你好' : 'Southern Wind';
          })
        StateProp({content:this.message})
      }
      .width('100%')
    }
  }
}


// 子组件
@Component
struct StateProp{
  @Prop content:string
  build(){
    Column(){
      Text('prop:'+this.content)
        .textStyle()
        .fontColor(Color.Green)
      Button('修改数据')
        .btnStyle()
        .onClick((event: ClickEvent) => {
        this.content = 'HarmonyOS4.0'

      })

    }
  }
}
// 文本公共样式
@Extend(Text) function textStyle() {
  .fontSize(30)
  .fontWeight(FontWeight.Bold)
}
// 按钮公共样式
@Extend(Button) function btnStyle() {
  .backgroundColor(Color.Green)
  .fontSize(25)
  .margin(10)
  // .click()
}





```