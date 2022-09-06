# 项目搭建
## 创建
1. vue create j-trip  (webpack)
2. npm init vue@latest   (vite)

## 配置
### 图标+标题+jsconfig.json
1. icon 图标
2. 标题  (src根目录下 index. html)
3. jsconfig. json
	(vite 创建的项目没有, 可以去其他项目里拖进来, 可以有更好的代码提示)

### 目录结构划分
- assets: img/css/font/video/audio
- components:
	common  多个项目共用的组件
	content    当前项目共用的组件
- mock: 接口没写好的时候用于模拟数据
- router: 路由
- service: 网络请求
- store (vuex)/stores (pinia): 状态管理
- utils: 工具函数
- views/pages: 路由跳转的大页面

![[Pasted image 20220906131154.png]]
### css
npm i normalize. css
reset. css
common. css
![[Pasted image 20220906114938.png]]
### router
router-->index.js
![[Pasted image 20220906122248.png]]
main. js
![[Pasted image 20220906122055.png]]
### 状态管理 pinia/vuex
pinia
store-->index. js
```js
import { createPinia } from "pinia";

const pinia = createPinia()
  
export default pinia
```
store-->modules-->aa. js
```js
import { defineStore } from "pinia";

const useAa = defineStore("aa", {
  state: () => ({

  }),
  actions: {

  }
})
export default useAa
```

main. js
```js
import { createPinia } from 'pinia'

app.use(createPinia())
```


