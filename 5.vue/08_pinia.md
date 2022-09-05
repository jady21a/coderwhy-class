# pinia
菠萝 (接近西班牙语的菠萝)
也是类似 vuex 的状态管理库

## pinia 和 vuex 的区别
pinia 其实算是 vuex 5 的版本
没有 vuex 的 mutations, modules
但是保留了 
state-->data
getters-->computed
actions-->methods

## 安装
npm i pinia
yarn add pinia

## 使用
stores-->index.js
![[Pasted image 20220905172314.png]]
main. js
![[Pasted image 20220905172419.png]]


# store
pinia 中可以有很多个 store, 并且可以直接独立使用
index.js 是入口文件, 其余都是 pinia 的 store
定义 store

约定返回的函数用 useX 命名
1counter. js
![[Pasted image 20220905183530.png]]
Store 在它被使用之前是不会创建的，我们可以通过调用 use 函数来使用 Store：
1.vue
![[Pasted image 20220905183314.png]]
# state
state-->data

# getters
getters-->computed


# actions
actions-->methods
和 getters 一样，在 action 中可以通过 this 访问整个 store 实例的所有操作

## 异步 (请求网络)