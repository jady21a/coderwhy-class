S# 网络请求
wx. request (Object object)
属性
➢ url: 必传 
➢ data: 请求的参数 
➢ method: 请求的方式 
➢ success: 成功时的回调 
➢ fail: 失败时的回调

## 基本使用
```js
// pages/hh/hh.js
Page({
  data: {
    allCities:{},
    houseList:[],
    currentPage:1
  },
  onLoad(options) {
    // 基本使用
    wx.request({
      url: 'http://codercba.com:1888/api/city/all',
      success:(res)=>{
        const data=res.data.data
        this.setData({allCities:data})
      }
    })
    wx.request({
      url: 'http://codercba.com:1888/api/home/houselist',
      data:{ page:1 },
      success:(res)=>{
        const data=res.data.data
        this.setData({houseList:data})
      }
    })
  },
})
```

```html
<!--pages/hh/hh.wxml-->
<text>pages/hh/hh.wxml</text>
<block wx:for="{{houseList}}" wx:key="id">
  <view>
    <!-- <image src="{{}}"></image> -->
    <view>{{item.data.houseName}}</view>
  </view>
</block>
```

## 封装
### 封装成函数 
```js 
// service-->index.js
// 1.封装成函数
export function jRequest(options) {
  return new Promise((resolve, reject) => {
    wx.request({
      ...options,
      success: (res) => {
        resolve(res.data)
      },
      fail:reject
    })
  })
}
```
#### 使用
##### i.直接使用封装函数
```js
// pages/hh/hh.js
Page({
  data: {
    allCities:{},
    houseList:[],
    currentPage:1
  },
	onLoad(){
    jRequest({
      url: 'http://codercba.com:1888/api/city/all'}).then(res=>{
        this.setData({allCities:res.data})
      })
    jRequest({
      url: 'http://codercba.com:1888/api/home/houselist',
      data:{ page:1 }
    }).then(res=>{
      this.setData({houseList:res.data})
    })
  },
})
```
##### ii. async/await (推荐)
```js
// pages/hh/hh.js
Page({
  data: {
    allCities:{},
    houseList:[],
    currentPage:1
  },
  async onLoad(){
    // 3.async/await(异步await会等前一个请求有结果后再请求下一个)
    // const cityRes=await jRequest({
    //   url:'http://codercba.com:1888/api/city/all'
    // })
    // this.setData({allCities:cityRes.data})

    // const houseRes=await jRequest({
    //   url: 'http://codercba.com:1888/api/home/houselist',
    //   data:{ page:1 }
    // })
    //   this.setData({houseList:houseRes.data})

    // 4.将await/async封装到单独的函数然后在onload调用(推荐)
    this.getCity()
    this.getHouse()
  },
    async getCity(){
    const cityRes=await jRequest({
      url:'http://codercba.com:1888/api/city/all'
    })
    this.setData({allCities:cityRes.data})
  },
  async getHouse(){
    const houseRes=await jRequest({
      url: 'http://codercba.com:1888/api/home/houselist',
      data:{ page:1 }
    })
      this.setData({houseList:houseRes.data})
  }
})
```

### 封装成类 (扩展性更强, 可以传 baseUrl)
```js
// service-->index.js
// 封装成类(扩展性更强,可以传baseUrl)
class JRequest{
  constructor(baseURL) {
    this.baseURL=baseURL
  }
  request(options) {
    const { url } = options
    return new Promise((resolve, reject) => {
      wx.request({
        ...options,
        url: this.baseURL + url,
        success: (res) => {
          resolve(res.data)
        },
        fail: (err) => {
          console.log("err",err)
        }
      })
    })
  }
  get(options) {
    return this.request({ ...options,method:"get"})
  }
  post(options) {
    return this.request({ ...options,method:"post"})
  }
}

export const request1 = new JRequest (' http://codercba.com:1888/api ')
```
#### 使用
```js
// pages/hh/hh.js
Page({
  data: {
    allCities:{},
    houseList:[],
    currentPage:1
  },
	onLoad(){
    request1.get({ 
      url: '/city/all'
    }).then(res => {
      console.log("res",res)
    })
  },
})
```

## 网络请求的域名配置
小程序只可以跟指定的域名进行网络通信, 因此需要预先设置通讯域名

小程序登录后台 – 开发管理 – 开发设置 – 服务器域名
- 域名只支持 https (wx. request、wx. uploadFile、wx. downloadFile) 和 wss (wx. connectSocket) 协议
- 域名不能使用 IP 地址（小程序的局域网 IP 除外）或 localhost；
- 可以配置端口, 但只能固定一个端口; 如果不配端口, 那么请求的 url 就带端口
- 不支持配置父域名来使用子域名

# 小程序简单 api
```html
<!--pages/jj/jj.wxml-->
<text>pages/jj/jj.wxml</text>
<!-- 1.展示弹窗 -->
<view>
  <button size="mini" bindtap="onShowToast">showToast</button>
  <button size="mini" bindtap="onShowModal">showModal</button>
  <button size="mini" bindtap="onShowAction">showAction</button>
</view>


<!-- 3.设备信息 -->
<button bindtap="onGetSystemInfo">设备信息</button>

<!-- 4.本地存储 -->
<button bindtap="onLocalStorage">本地存储</button>
```
## 弹窗
showToast、showModal、showLoading、showActionSheet
### showToast
```js
// pages/jj/jj.js
Page({
  // 1.弹窗相关的API
  onShowToast() {
    wx.showToast({
      title: '购买失败!',
      icon: "error",
      duration: 5000,
      mask: true,
      success: (res) => {
        console.log("res:", res);
      },
      fail: (err) => {
        console.log("err:", err);
      }
    })

    // wx.showLoading({
    //   title: "加载中ing"
    // })
  },
 }) 
```
![[Pasted image 20220923111100.png]]
![[Pasted image 20220923110943.png]]
### showModal (Modal/ˈmoʊd(ə)l /-->模态的)
```js
// pages/jj/jj.js
Page({
  onShowModal() {
    wx.showModal({
      title: "确定购买吗?",
      content: "确定购买的话, 请确定您的微信有钱!",
      confirmColor: "#f00",
      cancelColor: "#0f0",
      success: (res) => {
        if (res.cancel) {
          console.log("用户点击取消");
        } else if (res.confirm) {
          console.log("用户点击了确定");
        }
      }
    })
  },
 })
```
![[Pasted image 20220923111400.png]]

### showActionSheet
```js
  // pages/jj/jj.js
Page({
  onShowAction() {
    wx.showActionSheet({
      itemList: ["衣服", "裤子", "鞋子"],
      success: (res) => {
        console.log(res.tapIndex);
      },
      fail: (err) => {
        console.log("err:", err);
      }
    })
  },
 })
```
![[Pasted image 20220923111724.png]]



## 分享功能
分享方式
- 右上角菜单
- 点击某一个按钮, 直接转发
收到的转发页面显示设置
onShareAppMessage
```js
// pages/jj/jj.js
Page({
// 2.分享的显式内容
  onShareAppMessage() {
    return {
      title: "旅途的内容",
      path: "/pages/jj/jj",
      imageUrl: "/assets/img/21.png"
    }
  },
})
```
## 获取设备信息
wx. getSystemInfo (Object object)
```js
// pages/jj/jj.js
Page({
	onGetSystemInfo() {
    // 1.获取手机的基本信息
     wx.getSystemInfo({
       success: (res) => {
         console.log(res);
       }
     })

    // 2.获取当前的位置信息
    wx.getLocation({
      success: (res) => {
        console.log("res:", res);
      }
    })
  },
})
```
![[Pasted image 20220923113516.png]]
获取位置信息
wx. getLocation (Object object)
需要在 app. json 中加上 permission
```json
{
  "pages": ["pages/index/index"],
  "permission": {
    "scope.userLocation": {
      "desc": "你的位置信息将用于小程序位置接口的效果展示" 
    }
  }
}
```

![[Pasted image 20220923113110.png]]


## storage
### 同步存储数据
 wx. setStorageSync (string key, any data) 
 any wx. getStorageSync (string key) 
 wx. removeStorageSync (string key) 
 wx. clearStorageSync ()

### 异步存储数据
 wx. setStorage (Object object) 
 wx. getStorage (Object object) 
 wx. removeStorage (Object object) 
 wx. clearStorage (Object object)

# 小程序页面跳转
```html
<!--pages/kk/kk.wxml-->
<text>pages/kk/kk.wxml</text>
<button bindtap="onNavTap">navigatorTo跳转</button>
<navigator class="nav" url="/pages/kk2/kk2?name=why&age=18">标签跳转</navigator>

<view> {{message}} </view>
```
- navigator 组件 (标签)
	navigator 可以跳转到不同页面，也可以跳转到其他小程序中：
	![[Pasted image 20220923115951.png]]
- api
	wx. navigateTo (Object object)
	wx. navigateBack (Object object)
```js
// pages/kk/kk.js
Page({
  data: {
    name: "kobe",
    age: 30,
    message: "哈哈哈"
  },
  onNavTap() {
    const name = this.data.name
    const age = this.data.age
    // 页面导航跳转
    wx.navigateTo({
      // 跳转的过程, 传递一些参数过去
      url: `/pages/kk2/kk2?name=${name}&age=${age}`,
      events: {
        backEvent(data) {
          console.log("back:", data);
        },
        coderwhy(data) {
          console.log("why:", data);
        }
      }
    })
  }
})
```
### 跳转时传递数据
![[Pasted image 20220923120238.png]]
### 跳转后返回数据
```html
<!--pages/kk2/kk2.wxml-->
<text>pages/kk2/kk2.wxml</text>
<text>pages2/detail/detail.wxml</text>
<view>name: {{name}}, age: {{age}}</view>
<button size="mini" type="primary" bindtap="onBackTap">返回</button>
<navigator open-type="navigateBack">返回</navigator>
```

```js
// pages/kk2/kk2.js
Page({
  data: {
    name: "",
    age: 0
  },

  onLoad(options) {
    console.log(options);
    const name = options.name
    const age = options.age
    this.setData({ name, age })

    // const eventChannel = this.getOpenerEventChannel()
  },

  onBackTap() {
    // 1.返回导航
    wx.navigateBack()

    // 2.方式一: 给上一级的页面传递数据
    // 2.1. 获取到上一个页面的实例
    // const pages = getCurrentPages()
    // const prePage = pages[pages.length-2]

    // // 2.2.通过setData给上一个页面设置数据
    // prePage.setData({ message: "呵呵呵" })

    // 3.方式二: 回调events的函数
    // 3.1. 拿到eventChannel
    const eventChannel = this.getOpenerEventChannel()

    // 3.2. 通过eventChannel回调函数
    eventChannel.emit("backEvent", { name: "back", age: 111 })
    eventChannel.emit("coderwhy", { name: "why", age: 10 })
  },
  onUnload() {
    // // 2.1. 获取到上一个页面的实例
    const pages = getCurrentPages()
    const prePage = pages[pages.length-2]

    // // 2.2.通过setData给上一个页面设置数据
    prePage.setData({ message: "呵呵呵" })
  }
})
```

# 小程序登录

## 识别用户身份
 认识小程序登录流程 
 openid 和 unionid 
 获取 code 
 换取 authToken




----

# 案例
## 上拉加载更多  [[00_注意]]

```js
// pages/ii/ii.js
import { jRequest , request1} from "../../service/index"

Page({
  data:{
    houseList:[],
    currentPage:1
  },
  async onLoad(){
    this.getHouse()
  },
  
  async getHouse(){
    const houseRes=await jRequest({
      url: 'http://codercba.com:1888/api/home/houselist',
      data:{ page:this.data.currentPage }
    })
    const finalList =[...this.data.houseList, ...houseRes.data]
    this.setData({ houseList: finalList })
    // 此处++不需要使用setData,因为setData是在改变数据的时候需要刷新页面才使用
    this.data.currentPage++
  },
  onReachBottom() {
    console.log("reachBottom!")
    this.getHouse()
  }
})
```