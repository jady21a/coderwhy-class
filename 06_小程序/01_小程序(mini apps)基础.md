# 小程序开发的框架
## uni-app
由 DCloud 团队开发和维护用,  vue 开发

一套代码，可发布到 iOS、Android、Web（响应式）、以及各种小程序

## taro  
泰罗
由京东团队开发和维护,  支持使用 React/Vue/Nerv 等框架来开发


uni-app 和 taro 开发的网页, 无论是适配原生小程序还是原生 App，都有较多的适配问题

开发原生 app: reactNative, flutter


# 开发 id
https://mp.weixin.qq.com/cgi-bin/wx
开发--> 开发管理--> 开发设置


![[Pasted image 20220917122452.png]]
## 开发工具
- vscode ![[Pasted image 20220917120909.png]]
- easy wxless
- 微信开发者工具
[稳定版 Stable Build | 微信开放文档 (qq.com)](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html)


# 小程序项目结构
![[Pasted image 20220917122700.png]]


# MVVM
vue
![[Pasted image 20220917125543.png]]

mini apps
![[Pasted image 20220917125653.png]]

都是为 html 和 js 之间建立了联系
- DOM Listeners : 监听事件绑定到 js
- Data Bindings: 将改变的数据由 js 绑定到 html

# 体验
新建文件夹 -->右键-->新建 page   (自动生成四个个文件 . js . json . wxml,wxss, 且在 app. json 里面添加路径)

也可在 app. json 里面添加路径自动生成文件夹和文件

![[Pasted image 20220917132142.png]]
![[Pasted image 20220917132500.png]]

排序第一的为首页
![[Pasted image 20220917132228.png]]
体验案例
![[Pasted image 20220917140140.png]]
![[Pasted image 20220917140229.png]]
![[Pasted image 20220917140127.png]]
