# 概览
![[Pasted image 20220924131232.png]]
![[Pasted image 20220924131258.png]]
![[Pasted image 20220924131209.png]]
# tabbar
app.json
```json
  "tabBar": {
    "list": [{
      "pagePath": "pages/a-music/a-music",
      "text": "音乐",
      "iconPath": "/assets/img/tabbar/music_normal.png",
      "selectedIconPath": "/assets/img/tabbar/music_active.png"
    },
    {
      "pagePath": "pages/b-video/b-video",
      "text": "视频",
      "iconPath": "/assets/img/tabbar/video_normal.png",
      "selectedIconPath": "/assets/img/tabbar/video_active.png"
    }
  ]
  },
```

# music
## vant
### 安装
npm i @vant/weapp -S --production
构建
工具-->构建 ![[Pasted image 20220923223411.png]]
 把 node_modules 的文件复制到 miniprogram_npm
### 注册
在使用 vant 的文件. json 中注册使用到的 vant 组件名
这里以 button 和 rate 为例
```json 
{
  "usingComponents": {
    "van-button": "@vant/weapp/button/index",
    "van-rate": "@vant/weapp/rate/index"
  }
}
```

如果小程序编译有问题可以尝试清空缓存后重新编译



## id 传递
![[Pasted image 20220925001118.png]]
![[Pasted image 20220925001251.png]]

## 毛玻璃效果
```html 
<!--pages/a-music5-player/a-music5-player.wxml-->
<!-- background -->
<image class="bg-image" src="{{currentSong.al.picUrl}}" mode="aspectFill"></image>
<view class="bg-cover"></view>
```

```css 
/* pages/a-music5-player/a-music5-player.wxss */
.bg-image, .bg-cover {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  z-index: -1;
}

.bg-cover {
  background-color: rgba(0,0,0,.2);
  backdrop-filter: blur(20px);
}
```





# video
# 要点
## 数据共享
### app. globalData (app.js)
```js
// app.js
App({
  globalData: {
    screenWidth: 375,
    screenHeight: 667,
  },
  onLaunch() {
    // 1.获取设备的信息
    wx.getSystemInfo({
      success: (res) => {
        this.globalData.screenWidth = res.screenWidth
        this.globalData.screenHeight = res.screenHeight

      },
    })
  }
})
```

使用
```js
// pages/main-music/main-music.js
const app = getApp()
Page({
  data: {
    screenWidth: 375,
  },
  onLoad() {
    this.setData({ screenWidth: app.globalData.screenWidth })
  }
```

### HYEventStore
#### 安装
 npm i hy-event-store
构建 npm

#### 使用
store-->songStore
```js
import { HYEventStore } from "hy-event-store"
import { getPlaylistDetail } from "../services/music"

const songStore=new HYEventStore({
  state:{
    recommendSongs:[],
  },
  actions:{
    fetchRecommendSongAction(ctx){
      getPlaylistDetail(3778678).then(res=>{
        console.log(res)
				ctx.recommendSongs=res.playlist.tracks
      })
    }
  }
})
export default songStore
```

a-music. js
```js
import songStore  from '../../store/songStore'

Page({
  data: {
    recommendSongs:[]
  },
  onLoad(options) {
      // 把请求到的数据赋值给recommendSongs
      songStore.onState("recommendSongs",(value)=>{
      this.setData({recommendSongs:value})
    })
      songStore.dispatch("fetchRecommendSongAction")
   }
 )}

```

其他页面使用 store 中共享的数据
```js
// pages/a-music2-songDetail/a-music2-songDetail.js
import songStore from "../../store/songStore"

Page({
  data: {
    songs:[]
  },
  onLoad(){
    // 将请求到的数据放到songs
    // songStore.onState("recommendSongs",(value)=>{
    //   this.setData({songs:value})
    // })
    // 优化
    songStore.onState("recommendSongs",this.handleRecommendSongs)
  },
  handleRecommendSongs(value){
      this.setData({songs:value})
  },
  onUnload(){
    songStore.offState("recommendSongs",this.handleRecommendSongs)
  }
})
```

```html
<!--pages/a-music2-songDetail/a-music2-songDetail.wxml-->
<view>
  <block wx:for="{{songs}}" wx:key="id">
    <view>{{item.name}}</view>
  </block>
</view>

```