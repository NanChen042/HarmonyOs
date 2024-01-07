# 状态管理

看下面这张图

![Alt text](assets/HarmonyOS4.0%E7%B3%BB%E5%88%97%E2%80%94%E2%80%9405%E3%80%81%E7%8A%B6%E6%80%81%E7%AE%A1%E7%90%86/image.png)
`Components`部分的装饰器为组件级别的状态管理，`Application`部分为应用的状态管理。开发者可以通过@StorageLink/@LocalStorageLink 实现应用和组件状态的双向同步，通过@StorageProp/@LocalStorageProp 实现应用和组件状态的单向同步。

### Prop

```ts
static Prop(propName: string): any
```

与 AppStorage 中对应的 propName 建立单向属性绑定。如果给定的 propName 在 AppStorage 中存在，则返回与 AppStorage 中 propName 对应属性的单向绑定数据。如果 AppStorage 中不存在 propName，则返回 undefined。单向绑定数据的修改不会被同步回 AppStorage 中。
prop 是单向绑定，但父级不会跟子集进行相应

**@Prop 是单向传递。**

```js
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
        .btnStyle(()=>{
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
@Extend(Button) function btnStyle(click:Function) {
  .backgroundColor(Color.Green)
  .fontSize(25)
  .margin(10)
  .onClick(()=>{
    click()
  })
 }
```

效果：
![Alt text](assets/HarmonyOS4.0%E7%B3%BB%E5%88%97%E2%80%94%E2%80%9405%E3%80%81%E7%8A%B6%E6%80%81%E7%AE%A1%E7%90%86/recording-1.gif)

关于多个页面使用相同组件重名报错问题：
可以自己定义一个规范：
我这里用结构体名称加下划线的形式命名函数,如果文件名为 Index,那么我的按钮组件可以用`Index_btnStyle`



### Link

```ts
static Link(propName: string): any
```

与 AppStorage 中对应的 propName 建立双向数据绑定。如果给定的 propName 在 AppStorage 中存在，返回与 AppStorage 中 propName 对应属性的双向绑定数据。

双向绑定数据的修改会同步回 AppStorage 中，AppStorage 会将变化同步到所有绑定该 propName 的数据和自定义组件中。

如果 AppStorage 中不存在 propName，则返回 undefined。


**以上是官方的说明，其实说白了`Prop`就是单项数据绑定,`Link`是双向数据绑定。**


## @Link 和@Prop 的区别
继续往下看个例子就明白了：

```js
@Entry
@Component
struct Index {
  // State必须要进行初始化
  @State message: string = 'Southern Wind'

  build() {
    Row() {
      Column() {
        Text(this.message)
          .textStyle()
        Button('点击')
          .backgroundColor(Color.Black)

          .onClick(() => {
            this.message = this.message === 'Southern Wind' ? '你好' : 'Southern Wind';
          })
        StateProp({ content: this.message })
        // Index_link({content_link:this.message})
        // 如果是Link，则使用$+变量名进行传递
        Index_link({content_link: $message})
      }
      .width('100%')
    }
  }
}


// 子组件
@Component
struct StateProp {
  @Prop content: string
  build() {
    Column() {
      Text('prop:' + this.content)
        .textStyle()
        .fontColor(Color.Green)
      Button('修改Prop数据')
        .btnStyle(() => {
          this.content = '我是Prop数据'
        })
    }
  }
}

@Component
struct Index_link {
  @Link content_link: string
  build() {
    Column() {
      Text('link:' + this.content_link)
        .textStyle()
        .fontColor(Color.Red)
      Button('修改Link数据').btnStyle(()=>{
        this.content_link = '我是Link数据'
      })
        .backgroundColor(Color.Red)
    }
  }
}


// 文本公共样式
@Extend(Text) function textStyle() {
  .fontSize(30)
  .fontWeight(FontWeight.Bold)
}
// 按钮公共样式
@Extend(Button) function btnStyle(click: Function) {
  .backgroundColor(Color.Green)
  .fontSize(25)
  .margin(10)
  .onClick(() => {
    click()
  })
  // .click()
}

```

效果：
![Alt text](assets/HarmonyOS4.0%E7%B3%BB%E5%88%97%E2%80%94%E2%80%9405%E3%80%81%E7%8A%B6%E6%80%81%E7%AE%A1%E7%90%86/recording-2.gif)
