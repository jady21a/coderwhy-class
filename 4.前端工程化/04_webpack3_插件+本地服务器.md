# 插件
 Loader 是用于特定的模块类型进行转换；
 Plugin 可以用于执行更加广泛的任务，比如打包优化、资源管理、环境变量注入等；

## CleanWebpackPlugin
打包自动删除多余文件
目前 webpack 已经含有此功能
![[Pasted image 20220823221526.png]]
npm install clean-webpack-plugin -D
![[Pasted image 20220823221141.png]]

## HtmlWebpackPlugin
 生成对应 index. html 文件
 npm install html-webpack-plugin -D
 ![[Pasted image 20220823221241.png]]

## DefinePlugin
是一个 webpack 内置的插件（不需要单独安装）
正确编译 template ，读取到 BASE_URL 的值
![[Pasted image 20220823221643.png]]

## mode
可选值有：'none' | 'development' | 'production'；
![[Pasted image 20220823221816.png]]

![[Pasted image 20220823221838.png]]

# 本地服务器
搭建本地服务器可以在文件发生变化时，自动完成编译和展示, 以减少一直 npm run build 和需要自己打开浏览器的麻烦

## webpack-dev-server
可以监听到文件的变化，但是事实上它本身是没有自动刷新浏览器的功能
npm install webpack-dev-server -D
![[Pasted image 20220823222343.png]]
webpack-dev-server 在编译之后不会写入到任何输出文件，而是将 bundle 文件保留在内存中

### 热模块替换（HMR）
Hot Module Replacement  (webpack-dev-server 已内置, 且默认开启)
应用程序运行过程中，替换、添加、删除模块，而无需重新刷新整个页面；
修改了 css、js 源代码，会立即在浏览器更新
![[Pasted image 20220823222721.png]]
![[Pasted image 20220823222917.png]]

vue 和 react 中有自己的 loader 对模块热替已经预设好了, 不需要自己每次自己设置

## host 配置
host 设置主机地址：  默认值是 localhost；
如果希望其他地方也可以访问，可以设置为 0.0.0.0；
 localhost：本质上是一个域名，通常情况下会被解析成 127.0.0.1
port :设置监听的端口，默认情况下是 8080
open: 是否打开浏览器：默认值是 false
compress: 是否为静态文件开启 gzip compression , 默认值是 false

## 开发环境和生产环境
![[Pasted image 20220823223510.png]]

![[Pasted image 20220823223755.png]]