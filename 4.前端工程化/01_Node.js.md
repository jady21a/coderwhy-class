# node 基本
## node 是什么
基于 V8 JavaScript 引擎的 JavaScript 运行时环境
chorme 和 node 都有 v8 引擎来解析 js 代码
不同:
 浏览器中，还需要解析、渲染 HTML、CSS 等相关渲染引擎，另外还需要提供支持浏览器操作的 API、浏览器自己的事件循环等；
在 Node. js 中，比如文件系统读/写、网络 IO、加密、压缩解压文件等操作；

## 应用
目前前端开发的库都是以 node 包的形式进行管理；
npm、yarn、pnpm 工具成为前端开发使用最多的工具；
## 安装
重要工具放 c 盘
![[Pasted image 20220819115957.png]]
c++依赖打钩
![[Pasted image 20220819121805.png]]
检查是否安装成功
![[Pasted image 20220819120346.png]]

## node 版本控制
- n
- nvm
以上两个 only for mac
但是有 nvm for windows
https://github.com/coreybutler/nvm-windows

nvm install latest 安装最新的 node 版本
nvm list 展示目前安装的所有版本
nvm use 切换版本

## 在终端运行
打开终端快捷键 ctrl+ ~
![[Pasted image 20220819132141.png]]

运行方案: git bash>cmd>powershell
选择默认运行方案
![[Pasted image 20220819132553.png]]


## node 传递参数
输出
https://nodejs.org/dist/latest-v16.x/docs/api/console.html
console. log
console. trace 打印函数的调用栈
console. clear (写在 js 文件, node 运行时清空) ![[Pasted image 20220819144318.png]]

清空终端命令 cls
终止正在安装的库  ctrl+c

![[Pasted image 20220819143900.png]]
输入
argc:  argument counter 的缩写，传递参数的个数；
argv:   argument vector  参数向量
![[Pasted image 20220819135638.png]]
![[Pasted image 20220819143752.png]]
## Repl
Read-Eval-Print Loop   “读取-求值-输出”循环；
REPL 是一个简单的、交互式的编程环境；
类似浏览器
![[Pasted image 20220819144723.png]]

node 终端打开 repl
node+回车
![[Pasted image 20220819144848.png]]
退出 repl
![[Pasted image 20220819150214.png]]
ctrl+D  或两次 ctrl+c
## 全局对象
![[Pasted image 20220819184723.png]]

◼ __dirname：获取当前文件所在的路径
◼ __filename：获取当前文件所在的路径和文件名称：
![[Pasted image 20220819184747.png]]