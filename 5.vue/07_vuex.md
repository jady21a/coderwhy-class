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


## 单一数据源
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

### mapGetters
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

异步函数不要放于组件中, 应该放于 vux 的 store 中
![[Pasted image 20220905010614.png]]

### mapMutation
option api
![[Pasted image 20220905104211.png]]

setup
![[Pasted image 20220905103723.png]]

actions

