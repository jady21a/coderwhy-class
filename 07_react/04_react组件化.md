# 分类
- 按定义: 函数组件/类组件
- 按是否有状态维护: 无状态组件/有状态组件
- 按职责: 展示型组件/容器型组件

函数组件, 无状态组件, 展示型组件主要关注 ui 展示
类组件, 有状态组件, 容器型组件主要关注数据逻辑

## 类组件
- 组件名首字母大写 (包括函数组件)
- 类组件需要继承自 React. Component
- 类组件必须实现 render 函数
![[Pasted image 20221026175706.png]]
在 ES6 之前，可以通过 create-react-class 模块来定义类组件，但是目前官网建议我们使用 ES6 的 class 类定义。

### render 函数的返回值
render 被调用时，它会检查 this.props 和 this.state 的变化并返回以下类型之一：
- React 元素,    如<div/>会被渲染为 DOM 节点 <div/>是 react 元素
- 数组或 fragments:   使得 render 方法可以返回多个元素。
- portals:   可以渲染子节点到不同的 DOM 子树中。
- 字符串或数值类型：它们在 DOM 中会被渲染为文本节点
- 布尔类型或 null：什么都不渲染。

## 函数组件
函数组件是使用 function 来进行定义的函数，只是这个函数会返回和类组件中 render 函数返回一样的内容。
![[Pasted image 20221026175634.png]]
没有 hooks 的函数:
-  没有生命周期，也会被更新并挂载，但是没有生命周期函数； 
-  this 关键字不能指向组件实例（因为没有组件实例）； 
-  没有内部状态（state）；


# 生命周期
- Mount
- Update
- Unmount
没有 hooks 的函数组件没有生命周期
![[Pasted image 20221026180602.png]]
## constructor
-  通过给 this. state 赋值对象来初始化内部的 state； 
-  为事件绑定实例（this）；
![[Pasted image 20221026180719.png]]
如果不初始化 state 或不进行方法绑定，则不需要为 React 组件实现构造函数。
## componentDidMount
组件挂载后（插入 DOM 树中）立即调用。

里面通常进行的操作
-  依赖于 DOM 的操作可以在这里进行； 
-  在此处发送网络请求就最好的地方；（官方建议） 
-  可以在此处添加一些订阅（会在 componentWillUnmount 取消订阅）；

## componentDidUpdate
更新后会被立即调用，首次渲染不会执行此方法。

里面通常进行的操作
-  当组件更新后，可以在此处对 DOM 进行操作； 
-  如果对更新前后的 props 进行了比较，也可以选择在此处进行网络请求；（例如，当 props 未发生变化时，则不会执行网络请求）。

## componentWillUnmount
组件卸载及销毁之前直接调用

里面通常进行的操作
-  在此方法中执行必要的清理操作；例如，清除 timer，取消网络请求或清除在 componentDidMount () 中创建的订阅等；

## 不常用生命周期
-  getDerivedStateFromProps：state 的值在任何时候都依赖于 props 时使用；该方法返回一个对象来更新 state； 
-  getSnapshotBeforeUpdate：在 React 更新 DOM 之前回调的一个函数，可以获取 DOM 更新前的一些信息（比如说滚动位置）； 
-  shouldComponentUpdate：该生命周期函数很常用，见性能优化；

# 组件间通讯
父传子: 通过属性=值的形式来传递数据给子组件
子传父: 通过 props 参数获取父组件传递过来的数据
