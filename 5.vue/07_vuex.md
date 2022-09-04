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
2. 不能直接改变 store 中的状态 (需要提交 (commit) mutation)