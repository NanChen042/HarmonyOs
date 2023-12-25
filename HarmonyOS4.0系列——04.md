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
```js
@Extend(Text) function textStyle(fs:number){
  .fontSize(fs).fontColor(Color.Pink)
}
```





