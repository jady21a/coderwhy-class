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




# video

