## 编辑器调整
我们在每次退出编辑器后再次打开会直接进入项目文件中，这样在新建项目用起来很是不方便，所以这里跟着设置一下就好
![Alt text](assets/HarmonyOS4.0%E7%B3%BB%E5%88%97%E2%80%94%E2%80%9402%E3%80%81%E6%B1%89%E5%8C%96%E6%8F%92%E4%BB%B6%E3%80%81%E5%A3%B0%E6%98%8E%E5%BC%8F%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8FArkTS%E5%92%8C%E7%B1%BBweb%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8F/image.png)
![Alt text](assets/HarmonyOS4.0%E7%B3%BB%E5%88%97%E2%80%94%E2%80%9402%E3%80%81%E6%B1%89%E5%8C%96%E6%8F%92%E4%BB%B6%E3%80%81%E5%A3%B0%E6%98%8E%E5%BC%8F%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8FArkTS%E5%92%8C%E7%B1%BBweb%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8F/image-4.png)
![Alt text](assets/HarmonyOS4.0%E7%B3%BB%E5%88%97%E2%80%94%E2%80%9402%E3%80%81%E6%B1%89%E5%8C%96%E6%8F%92%E4%BB%B6%E3%80%81%E5%A3%B0%E6%98%8E%E5%BC%8F%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8FArkTS%E5%92%8C%E7%B1%BBweb%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8F/image-1.png)
![Alt text](assets/HarmonyOS4.0%E7%B3%BB%E5%88%97%E2%80%94%E2%80%9402%E3%80%81%E6%B1%89%E5%8C%96%E6%8F%92%E4%BB%B6%E3%80%81%E5%A3%B0%E6%98%8E%E5%BC%8F%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8FArkTS%E5%92%8C%E7%B1%BBweb%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8F/image-2.png)
这样下次进入就不会直接跳转到当时的文件项目中！！

![Alt text](assets/HarmonyOS4.0%E7%B3%BB%E5%88%97%E2%80%94%E2%80%9402%E3%80%81%E6%B1%89%E5%8C%96%E6%8F%92%E4%BB%B6%E3%80%81%E5%A3%B0%E6%98%8E%E5%BC%8F%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8FArkTS%E5%92%8C%E7%B1%BBweb%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8F/image-3.png)
## 关于汉化
`settings` → `plugins `→ `installed `→ 输入 `chinese `→ 点击 `ebable `→ 点击 `apply `→重启DevEco-Studio完成汉化

![Alt text](assets/HarmonyOS4.0%E7%B3%BB%E5%88%97%E2%80%94%E2%80%9402%E3%80%81%E6%B1%89%E5%8C%96%E6%8F%92%E4%BB%B6%E3%80%81%E5%A3%B0%E6%98%8E%E5%BC%8F%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8FArkTS%E5%92%8C%E7%B1%BBweb%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8F/image-5.png)
## ArkTS路由

ArkTS的路由在`main_pages.json`中
![Alt text](assets/HarmonyOS4.0%E7%B3%BB%E5%88%97%E2%80%94%E2%80%9402%E3%80%81%E6%B1%89%E5%8C%96%E6%8F%92%E4%BB%B6%E3%80%81%E5%A3%B0%E6%98%8E%E5%BC%8F%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8FArkTS%E5%92%8C%E7%B1%BBweb%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8F/image-6.png)
### 点击事件
点击事件的写法为
```js
标签('标签名称')
	.onClick(()=>{
		router.pushUrl({
			url:'路径'
		})
	})
```
从First.ets跳转到Second.ets页面代码示例：
#### First.ets
```ts
import router from '@ohos.router'
@Entry
@Component
struct First {

  build() {
      Column() {
        Text('Southern Wind01')
          .fontSize(30)
        Button('click....')
          .width('40%')
          .height('40vp')
          .margin(20)
          .onClick(()=>{
          //    去第二个页面
            router.pushUrl({
              url:'pages/Second'
            })
          })
      }
    .width('100%')
    .height('100%')
  }
}

```

### Second.ets
```js
import router from '@ohos.router'
@Entry
@Component
struct second {

  build() {

      Column() {
        Text('Southern Wind02')
          .fontSize(30)
        Button('back')
          .padding(20)
          .margin(20)
          .backgroundColor('#e0e0e0')
          .fontColor('#000')
          .onClick(()=>{
            router.back()
          })
      }
      .width('100%')

    .height('100%')
  }
}

```
实际效果：
![请添加图片描述](./assets/HarmonyOS4.0系列——02、汉化插件、声明式开发范式ArkTS和类web开发范式/900a9faff9254354a0c2b8962a9b9868.gif)

### 类web开发范式
也就是所谓的前端开发方式。创建时使用`FA`模型，语言选择`JS`

![Alt text](assets/HarmonyOS4.0%E7%B3%BB%E5%88%97%E2%80%94%E2%80%9402%E3%80%81%E6%B1%89%E5%8C%96%E6%8F%92%E4%BB%B6%E3%80%81%E5%A3%B0%E6%98%8E%E5%BC%8F%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8FArkTS%E5%92%8C%E7%B1%BBweb%E5%BC%80%E5%8F%91%E8%8C%83%E5%BC%8F/image-7.png)
#### 类web路由配置
路由页面在`config.json`中
![在这里插入图片描述](./assets/HarmonyOS4.0系列——02、汉化插件、声明式开发范式ArkTS和类web开发范式/5d1779a3e27347b6ab0b8f399208617b.png)
写法和Vue类似
这里看一下
`first.html`
```html
<div class="container">
  <text class="title">
    Southern Wind 01
  </text>

  <button @click="goSecond">点击跳转</button>
</div>

```
`first.js`
```js
import router from '@ohos.router'
export default {
  data: {
    title: ""
  },
  onInit() {
    this.title = "Southern Wind";

  },
  //   跳转事件
  goSecond(){
    // router.pushUrl({
    //   url:'pages/second/second'
    // })
    router.push({
      url:'pages/second/second'
    })
  }
}

```
**注意：这里官方是说9版本以后使用`pushUrl`，但在js写法中起不了作用，应该是还没兼容导致的，这里还是用老版的`router.push`即可**

`second.html`
```html
<div class="container">
  <text class="title">
    Southern Wind 02
  </text>
  <button @click="back">back</button>
</div>

```
`second.js`
```js
import router from '@ohos.router'
export default {
  data: {
    title: ""
  },
  onInit() {
  },
  back(){
    router.back();
  }
}

```
效果：![请添加图片描述](./assets/HarmonyOS4.0系列——02、汉化插件、声明式开发范式ArkTS和类web开发范式/fb6fb67c648c421aafbbaa2bc0340e6b.gif)
