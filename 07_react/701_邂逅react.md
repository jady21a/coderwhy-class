https://zh-hans.reactjs.org/

# react 特点
## 声明式编程
当状态改变时，React 可以根据最新的状态去渲染我们的 UI 界面；
![[Pasted image 20221010172948.png]]

## 组件化
将复杂的界面拆分成一个个小的组件

## 多平台适配
react --> web 
ReactNative -->移动端跨平台 (目前 flutter 更好用)
ReactVR --> 虚拟现实 Web

# react 开发依赖
 react：包含 react 所必须的核心代码 
 react-dom：react 渲染在不同平台所需要的核心代码 
 babel：将 jsx 转换成 React 代码的工具

## 引入
1. cdn
```html
<script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
<script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin></script>
<script src=" https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```
2. 下载后本地引入
3. npm

