## @Styles
通用样式
类似于css中的`class`
语法一：**内部样式** 放在struct内
```js
  @Styles commonStyle(){
    .backgroundColor(Color.Pink)
    .padding('20px')
  }
```

语法二：**外部样式**
```js
@Styles function commonStyle() {
  .backgroundColor(Color.Pink)
  .padding('40px')
}
```
调用`.commonStyle()` 

总结：@Styles 内部样式和外部样式，内部样式优先级高于外部样式，内部不要需要用函数function定义，外部需要function;
缺点：只能用于通用样式，@Styles不能进行传参

那么如何进行传参呢？
## @Extend()
在@Styles的基础上，可以使用@Extend，用于扩展原生组件样式。
```js
@Extend(Text) function textStyle(fs:number){
  .fontSize(fs).fontColor(Color.Pink)
}
```

使用规范：和`@Styles`不同，`@Extend`仅支持定义在全局，不支持在组件内部定义。


```js
@Extend(Text) function fancy () {
  .fontColor(Color.Red)
}

// superFancyText可以调用预定义的fancy
@Extend(Text) function superFancyText(size:number) {
    .fontSize(size)
    .fancy()
}
```

例：
```js
@Entry
@Component
struct ExtendFun {
  @State message: string = '@Extend'

  build() {
    Row() {
      Column() {
        // Text(this.message).fontSize(40)
        Text('Southern Wind').superFancyText(40)
      }
      .width('100%')
    }
    .height('100%')
  }

}


// @Extend(Text) function textStyle(fs:number){
//   .fontSize(fs).fontColor(Color.Pink)
// }

@Extend(Text) function fancy () {
  .fontColor(Color.Red)
}

// superFancyText可以调用预定义的fancy
@Extend(Text) function superFancyText(size:number) {
  .fontSize(size)
  .fancy()
}

```
效果：

![Alt text](assets/HarmonyOS4.0%E7%B3%BB%E5%88%97%E2%80%94%E2%80%9404/image-1.png)

