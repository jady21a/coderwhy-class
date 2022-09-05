# 状态管理
管理各组件中数据的状态 (数据共享)
工具: vuex/pinia
# vuex
![[Pasted image 20220904185836.png]]
## 安装
npm install vuex

## 使用

## store
每一个 Vuex 应用的核心就是 store（仓库)
Vuex 和单纯的全局对象有什么区别:
1. Vuex 的状态存储是响应式的
2. 不能直接改变 store 中的状态 (需要提交 (commit) mutation) ![[Pasted image 20220904193841.png]]

使用 store 的地方
- template
- options api (如 computed)
- setup
![[Pasted image 20220904195249.png]]


### 单一数据源
Single Source of Truth
只有一个 store, store 里可以有 module

## state
数据的状态
![[Pasted image 20220905001657.png]]
![[Pasted image 20220904230724.png]]
### mapstate
#### option api 中
obj
![[Pasted image 20220905001056.png]]
arr

#### setup 中
![[Pasted image 20220905001247.png]]

## getters
需要经过变化后使用的数据
![[Pasted image 20220905010134.png]]

### mapGetters (辅助函数)
在 option api 好用, setup 中不好用
辅助函数一般: 
vue2--option api-- vuex--辅助函数
vue3-- setup-- pinia

option api
![[Pasted image 20220905010021.png]]

setup
![[Pasted image 20220905005949.png]]

## mutation
突变-->state 改变需要提交 mutation (突变)
相当于提交日志
![[Pasted image 20220905012419.png]]
![[Pasted image 20220905012522.png]]
![[Pasted image 20220905012610.png]]
![[Pasted image 20220905012722.png]]

异步函数不要放于组件中, 应该放于 vuex store 的action中
![[Pasted image 20220905010614.png]]

### mapMutation
option api
![[Pasted image 20220905104211.png]]

setup
![[Pasted image 20220905103723.png]]

## actions
actions 不可以直接改变数据状态, 需要提交 mutations 来改变
异步操作可以放在 actions

contex : contex 是拥有 store 中方法和属性的对象
contex. state
contex. commit ("aa")
contex. getters
![[Pasted image 20220905135707.png]]
### actions 使用
action 提交--mutation 修改--app 派发--template 显示
![[Pasted image 20220905141348.png]]
### mapActions 辅助函数
![[Pasted image 20220905142512.png]]
### 异步操作
  actions
![[Pasted image 20220905144357.png]]
mutations
![[Pasted image 20220905151702.png]]
![[Pasted image 20220905151717.png]]
## module
单一数据源的 store 如果只有一个文件会显得繁杂难以维护, 可以将其分割为小的模块
每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块 (module)；
![[Pasted image 20220905160452.png]]

### module 命名空间
默认 action , mutation 和 getter 内的数据是在全局注册的 (多个模块能够对同一个 action 或 mutation 作出响应), 
让模块内数据有自己的作用域 :
namespaced: true


### module 修改或派发根组件
![[Pasted image 20220905135315.png]]