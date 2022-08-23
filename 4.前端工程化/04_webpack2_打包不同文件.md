# 打包 css
css-loader
npm install style-loader -D
npm install css-loader -D

## 使用 css css-loader 
1. 内联 ![[Pasted image 20220823191227.png]]
2. 配置
在 webpack. config. js 文件中写明配置信息
module. rules 配置:
- test: 用于对 resource（资源）进行匹配，通常会设置成正则表达式
- use: 数组[UseEntry]
	loader: 必须有一个 loader 属性，对应的值是一个字符串
	options：可选的属性，值是一个字符串或者对象，值会被传入到 loader 中

use 中多个 loader 的使用顺序是从后往前
![[Pasted image 20220823192719.png]]


# PostCSS
自动添加浏览器前缀、css 样式的重置
npm install postcss-loader -D

 postcss 需要有对应的插件才会起效果，所以我们需要配置它的 plugin
![[Pasted image 20220823193015.png]]

## postcss-preset-env
npm install postcss-preset-env -D
![[Pasted image 20220823214041.png]]
![[Pasted image 20220823214021.png]]

# 打包图片

在 webpack5 之前，加载这些资源我们需要使用一些 loader，比如 raw-loader 、url-loader、file-loader；
之后:
- asset 
	在导出一个 data URI 和发送一个单独的文件之间自动选择.   对应 url-loader 并且配置资源体积限制实现
- asset/resource  
	发送一个单独的文件并导出 URL  对应 file-loader
- asset/inline
	导出一个资源的 data URI。对应 url-loader 
- asset/source
	导出源码.  对应 raw-loader
![[Pasted image 20220823214929.png]]
![[Pasted image 20220823214907.png]]


## 图片分大小打包
1. 将 type 修改为 asset
2. 添加 parser 属性
![[Pasted image 20220823215149.png]]

# babel
将 ES6+的语法， TypeScript， React 项目等转为普通浏览器识别代码

npm install @babel/cli @babel/core -D
npm install babel-loader -D
![[Pasted image 20220823215833.png]]
px babel src --out-dir dist
	src: 源文件目录
	--out-dir dist 指定输出文件夹为 dist

## babel 预设
npm install @babel/preset-env -D
npx babel src --out-dir dist --presets=@babel/preset-env

![[Pasted image 20220823112240.png]]
![[Pasted image 20220823215926.png]]


# resolve
用于设置模块如何被解析
resolve 可以帮助 webpack 从每个 require/import 语句中，找到需要引入到合适的模块代码；

如果文件具有扩展名, 直接打包, 否则会根据 resolve. mainFiles 配置选项中指定的文件顺序查找；
	resolve. mainFiles 的默认值是 ['index']；
	扩展名默认查找顺序 [".js", "json","wasm"]

配置别名 alias
当我们项目的目录结构比较深的时候，或者一个文件的路径可能需要 ../../../这种路径片段；
可以给某些常见的路径起一个别名
![[Pasted image 20220823220646.png]]