# 网络请求
wx. request (Object object)
属性
➢ url: 必传 
➢ data: 请求的参数 
➢ method: 请求的方式 
➢ success: 成功时的回调 
➢ fail: 失败时的回调

## 基本使用

## 封装




## 网络请求的域名配置
小程序只可以跟指定的域名进行网络通信, 因此需要预先设置通讯域名

小程序登录后台 – 开发管理 – 开发设置 – 服务器域名
- 域名只支持 https (wx. request、wx. uploadFile、wx. downloadFile) 和 wss (wx. connectSocket) 协议
- 域名不能使用 IP 地址（小程序的局域网 IP 除外）或 localhost；
- 可以配置端口, 但只能固定一个端口; 如果不配端口, 那么请求的 url 就带端口
- 不支持配置父域名来使用子域名

# 小程序简单 api
## 小程序弹窗
showToast、showModal、showLoading、showActionSheet


## 分享功能
分享方式
- 右上角菜单
- 点击某一个按钮, 直接转发
收到的转发页面显示设置
onShareAppMessage

## 获取设备信息
wx. getSystemInfo (Object object)


获取位置信息
wx. getLocation (Object object)


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
- navigator 组件 (标签)
	navigator 可以跳转到不同页面，也可以跳转到其他小程序中：
- api
	wx. navigateTo (Object object)
	wx. navigateBack (Object object)


### 跳转时传递数据



# 小程序登录

## 识别用户身份
 认识小程序登录流程 
 openid 和 unionid 
 获取 code 
 换取 authToken


