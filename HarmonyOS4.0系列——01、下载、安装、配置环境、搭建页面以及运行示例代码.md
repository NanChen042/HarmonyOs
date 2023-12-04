## HarmonyOS4.0应用开发
### 安装编辑器
![在这里插入图片描述](https://img-blog.csdnimg.cn/d12ee791d3d04727bfcd2dba0643d7a1.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/4945d2bb164c443b879d345cf808c593.png)
这里安装windows版本为例
### 安装依赖
打开`DevEco Studio`
![在这里插入图片描述](https://img-blog.csdnimg.cn/7b98a5e5dd5e4cd3ae3d7da3f51dcdb0.png)
这八项全部打钩即可开始编写代码，如果存在x，需要安装正确的库即可
### 开发
点击`Create Project`
![在这里插入图片描述](https://img-blog.csdnimg.cn/81b56927d15144b9a8e1fc4059ff62a0.png)
选择默认模板——next
![在这里插入图片描述](https://img-blog.csdnimg.cn/a28c50884617439f9d42b62dcc0b0838.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/e0111d159b72457196fd569f7b311677.png)
Model部分分为`Stage`和`FA`两个应用模型，`FA`是支持7版本以内的模型支持JS和TS，而`Stage`支持最新版切只支持TS
![在这里插入图片描述](https://img-blog.csdnimg.cn/e9ee7ddcc6774d4ba70ab9976e9472f4.png)

![在这里插入图片描述](https://img-blog.csdnimg.cn/415d87c2e69b41fb8925e5bf30d05231.png)
建议大家使用`Stage`模型
![在这里插入图片描述](https://img-blog.csdnimg.cn/d95ac887f1f24ae08ced99067dfe6c98.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/19cdfbff78e74031add9807b27932eab.png)
编辑好之后点击`Finish`
进去后等加载完毕在右上角点击预览查看效果
![在这里插入图片描述](https://img-blog.csdnimg.cn/de43917cb3304868b84a4d6e508ef8e5.png)
```ts
@Entry
// 程序入口
@Component
// 组件

// 结构体，语法格式 struct {}
struct Index {
  @State message: string = 'Hello World'

  build() {
    // 界面内容放在build中
    Row() {
      // 行有多高
      Column() {
        // 列有多长
        Text(this.message) 
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

此段代码就是让界面撑满整个屏幕并对`Hello World`设置字体大小以及粗体


DevEco Studio提供自动更新代码和实时渲染的效果


![在这里插入图片描述](https://img-blog.csdnimg.cn/c5cbec3347464bd4afbf3e0a8ccfafd2.png)
电源键：打开状态下会进行实时更新，如果是关闭状态就不会进行更新，建议打开

![在这里插入图片描述](https://img-blog.csdnimg.cn/66617d3114aa4163867146b79218d229.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/d656d82daca648d0b26d92fb0e666878.png)
鸿蒙系统可以在一端代码兼容多端应用，那么如何看到pad端、桌面端等其他的调试效果呢？
![在这里插入图片描述](https://img-blog.csdnimg.cn/6d402de040fa4d37bb6f129e685825cd.png)
![请添加图片描述](https://img-blog.csdnimg.cn/184203004ab14596b5a015414ea05850.gif)
如果开启了多端查询那么热更新是无法进行实时更新的，需要关闭一下
![在这里插入图片描述](https://img-blog.csdnimg.cn/4e1c4db4386b4fd8b2e0c566e172c8c3.png)
### 真机调试
![在这里插入图片描述](https://img-blog.csdnimg.cn/2c46e061deeb4d13a0195914f2ca8864.png)
![在这里插入图片描述](https://img-blog.csdnimg.cn/6b913210daf848e5b1385e9ddada01b9.png)
这里要有绑定的华为设备就可以了，这里就不演示了