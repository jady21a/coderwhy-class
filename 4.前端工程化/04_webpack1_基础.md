# 打包工具
gulp, rollup, webpack, vite


# node 内置模块 path
Mac OS、Linux 和 window 上的路径是不一样的
解决办法: path 模块
## path 基本
-  extname：获取文件扩展名；
-  basename：获取文件名； 
-  dirname：当前文件之前的路径；
![[Pasted image 20220822215157.png]]
- join

## path. resolve ( )
path. resolve () 方法会把一个路径或路径片段的序列解析为一个绝对路径
给定的路径的序列是从右往左被处理的，后面每个 path 被依次解析，直到构造完成一个绝对路径；
如果在处理完所有给定 path 的段之后，还没有生成绝对路径，则使用当前工作目录
生成的路径被规范化并删除尾部斜杠，零长度 path 段被忽略
![[Pasted image 20220822232630.png]]

# webpack
https://webpack.js.org/
现在的 js 需求
- 模块化
- 高级特性增加效率: 如 es6, ts, sass, less
- 实时监听文件变化
- 代码压缩, 合并
webpack 是为现代的 JavaScript 应用程序而出现一个静态模块打包工具
静态: webpack 最终可以将代码打包成最终的静态资源（部署到静态服务器）；
模块化: webpack 默认支持各种模块化开发，ES Module、CommonJS、AMD 等；

## 打包的作用:
js: 
	es6-->es5, 
	ts-->js
css: 
	css 模块加载提取, 
	lesssass
img, font
	img 加载
	font 加载
html
	打包 html 文件
vue
	处理. vue 文件

## 安装
npm i webpack webpack-cli -D

## webpack-cli 作用
使可以在 node 命令行使用 webpack 的命令
![[Pasted image 20220822211251.png]]


## 默认打包
npm init -y
npm webpack webpack-cli -D
使用当前目录下的 webpack: npx webpack

使用全局 webpack: 在目录下直接执行 `webpack`
默认文件夹 ![[Pasted image 20220823003222.png]]

## webpack 配置
1. npx webpack --entry ./src/main. js --output-path ./build
2. 配置文件 npm run build
配置出入口文件名
![[Pasted image 20220823003829.png]]
配置 npx 运行 webpack 的脚本
![[Pasted image 20220823003912.png]]

![[Pasted image 20220823003713.png]]


## webpack 依赖图
从入口开始，会生成一个依赖关系图，这个依赖关系图会包含应用程序中所需的所有模块（比如. js 文件、css 文件、图片、字体等）； 然后遍历图结构，打包一个个模块（根据文件的不同使用不同的 loader 来解析）；
![[Pasted image 20220823190810.png]]



