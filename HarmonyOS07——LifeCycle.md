# 自定义组件的生命周期

> 允许在生命周期函数中使用 Promise 和异步回调函数，比如网络资源获取，定时器设置等；

## 页面生命周期

即被@Entry 装饰的组件生命周期，提供以下生命周期接口：

### onPageShow

页面加载时触发，页面每次显示时触发一次，包括路由过程、应用进入前台等场景。

### onPageHide

从第一个页面跳转第二个页面后，第一个页面会最为后台，触发`onPageHide`生命周期

页面每次隐藏时触发一次，包括路由过程、应用进入后台等场景。
下面是代码尝试

**`LifeCycle`页面**

```ts
import router from '@ohos.router'
@Entry
@Component
struct LifeCycle {
  @State message: string = '第一页'

  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(25)
        Divider()
        Button('Next').onClick(() => {
          router.pushUrl({url:'pages/LifeCycle2'})
        })
          .fontSize(25)
      }
      .width('100%')
    }
    .height('100%')
  }
  onPageShow() {
    console.log('第一页：——onPageShow')
  }

  onPageHide() {
    console.log('第一页：——onPageHide')
  }

  onBackPress() {
    console.log('第一页：——onBackPress')
  }
}
```

**`LifeCycle2`页面**

```ts
import router from '@ohos.router'

@Entry
@Component
struct LifeCycle2 {
  @State message: string = '第二页'

  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(25)
        Divider()
        Button('Back').onClick((event: ClickEvent) => {
          router.back()
        })
          .fontSize(25)

      }
      .width('100%')
    }
    .height('100%')
  }

  onPageShow() {
    console.log('第二页：——onPageShow')
  }

  onPageHide() {
    console.log('第二页：——onPageHide')
  }

  onBackPress() {
    console.log('第二页：——onBackPress')
  }
}
```

效果的话大家可以从 DevEco Studio 左下角第四个日志中查看具体效果。

### onBackPress

监听物理返回键，也就是手机上的回退，并不是路由连接`router.back()`的返回.
![Alt text](assets/HarmonyOS07%E2%80%94%E2%80%94LifeCycle/image.png)

## 组件生命周期

一般用@Component 装饰的自定义组件的生命周期，提供以下生命周期接口：

### aboutToAppear

在 build 构建之前渲染此生命周期。
详解：aboutToAppear 函数在创建自定义组件的新实例后，在执行其 build()函数之前执行。允许在 aboutToAppear 函数中改变状态变量，更改将在后续执行 build()函数中生效。

### aboutToDisappear

组件销毁时触发，例如删除，移出等操作。
详解：aboutToDisappear 函数在自定义组件析构销毁之前执行。不允许在 aboutToDisappear 函数中改变状态变量，特别是@Link 变量的修改可能会导致应用程序行为不稳定。

例：

```ts
import router from '@ohos.router'

@Entry
@Component
struct LifeCycle {
  @State message: string = '第一页'
  @State status: boolean = true

  build() {
    Row() {
      Column({ space: 20 }) {
        Text(this.message)
          .fontSize(25)
        Divider()
        Button('Next').onClick(() => {
          router.pushUrl({ url: 'pages/LifeCycle2' })
        })
          .fontSize(25)
        Divider()
        if (this.status) {
          LifeCycle_son()
        }
        Button('上段文字显示/隐藏').onClick(() => {
          this.status = !this.status
        }).fontSize(25)
      }
      .width('100%')
    }
    .height('100%')
  }

  onPageShow() {
    console.log('第一页：——onPageShow')
  }

  onPageHide() {
    console.log('第一页：——onPageHide')
  }

  onBackPress() {
    console.log('第一页：——onBackPress')
  }
}

@Component
struct LifeCycle_son {
  build() {
    Column() {
      Text('我是第一页的一个子组件')
        .fontSize(30)
    }
  }
  // aboutToAppear函数在创建自定义组件的新实例后，在执行其build()函数之前执行。
  aboutToAppear() {
    console.log('我是第一页的一个子组件:aboutToAppear')
  }

  // aboutToDisappear函数在自定义组件析构销毁之前执行。
  aboutToDisappear() {
    console.log('我是第一页的一个子组件:aboutToDisappear')
  }
}
```

![Alt text](assets/HarmonyOS07%E2%80%94%E2%80%94LifeCycle/image-2.png)

点击两次`上段文字显示/隐藏`按钮
依次出现上述的生命周期为：
![Alt text](assets/HarmonyOS07%E2%80%94%E2%80%94LifeCycle/image-1.png)

可以看到，如果将组件删除的话就可以触发`aboutTodisappear`生命周期
再次点击显示时触发`aboutToAppear`生命周期。当然默认的话会先触发`aboutToAppear`,因为他默认组件`LifeCycle_son`是先存在的。

## 页面路由

### 路由跳转

```ts
router.pushUrl({ url: "路径" });
```

### 路由传参

```ts
router.pushUrl({
  url: "/pages/LifeCycle2",
  params: {
    id: 1,
    username: "Southern Wind",
    age: 18,
  },
});
```

接受参数`username`，在**LifeCycle2**页面`router.getParams()`

```ts
let username = router.getParams()['username'] as string
```
效果：
![Alt text](assets/HarmonyOS07%E2%80%94%E2%80%94LifeCycle/image-3.png)


### 应用之间传参
公共数据共享创建参数
```ts
// 应用程序数据共享
AppStorage.Set('message','我要玩原神')
AppStorage.SetOrCreate('message2','Southern Wind')
```
其他页面获取此数据


```
```
