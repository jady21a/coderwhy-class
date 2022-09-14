# vue 自定义指令
## 如 v-focus 的实现
1. 默认方式
```js
//hooks-->useInput.js
import { ref, onMounted } from "vue"

export default function useInput() {
  const inputRef = ref()
  onMounted(() => {
    inputRef.value?.focus()
  })
  return { inputRef }
}
```

 ![[Pasted image 20220914151754.png]]
2. v-focus 局部指令 
![[Pasted image 20220914152914.png]]
![[Pasted image 20220914152839.png]]
3. v-focus 全局指令
	1. 直接在 main. 写
	![[Pasted image 20220914160118.png]]
	. vue 使用
	![[Pasted image 20220914160503.png]]
	2. 新建一个 directives (指令) 文件夹
	directive ![[Pasted image 20220914160316.png]]
	![[Pasted image 20220914160334.png]]
	
	main.js
	![[Pasted image 20220914160430.png]]
	也可以像插件一样使用
![[Pasted image 20220914173315.png]]
	. vue
	![[Pasted image 20220914160509.png]]
## 指令的生命周期
created, beforeMount, mounted, beforeUpdate, updated, beforeUmount, unmounted
没有 beforeCreate
## 指令的参数及修饰符
![[Pasted image 20220914132701.png]]
![[Pasted image 20220914171027.png]]
![[Pasted image 20220914171155.png]]

## 自定义时间格式化的指令
```js
// directive-->b_time.js
import dayjs from 'dayjs'

export default function directiveTime(app) {
  app.directive("time", {
    mounted(el, bindings) {
    let timestamp=el.textContent
      if (timestamp.length === 10) {
        timestamp=timestamp*1000
      }
      timestamp = Number(timestamp)
      let value = bindings.value
      if (!value) {
        value="YYYY-MM-DD hh:mm:ss"
      }
      const time = dayjs (timestamp).format (value)
      el.textContent=time
    }
  })
}
```
 directive-->index.js
 ```js
 // directive-->index
import directiveFocus from "./a_focus";
import directiveTime from "./b_time";

export default function directive(app) {
  directiveFocus(app)
  directiveTime(app)
}
```
main.js
```js
import directive  from './01_自定义指令/directive/index.js'

createApp (App).use (directive).mount ("#app")
```


# 内置组件
## teleport 远距离传送
类似 react 的 Portals
是 vue 的内置组件
### 属性
- to: 移动到目标元素
- disabled: 是否禁用 teleport
![[Pasted image 20220914183500.png]]
![[Pasted image 20220914183421.png]]
在. vue 的文件中写的 teleport 不会被渲染到真实 dom, 但是teleport 内要显示的内容会渲染到 to 的真实 dom 位置

### 多个 teleport
如果将多个 teleport 应用到同一个目标上（to 的值相同），那么这些目标会进行合并


## suspense (悬念) 异步组件用
结果如何是未知的悬念
还属于试验特性
是 vue 的内置全局组件
- default  默认显示
- fallback (退路, 备用) 默认无法显示时显示



# vue 插件
如 axios , router, pinia 都是 vue 插件
我们也可以编写自己的插件来全局给 vue 添加功能
插件功能
 添加全局方法或者 property，通过把它们添加到 config. globalProperties 上实现； 
 添加全局资源：指令/过滤器/过渡等； 
 通过全局 mixin 来添加一些组件选项； 
 一个库，提供自己的 API，同时提供上面提到的一个或多个功能；

vue 插件可以编写为
- 对象
- 函数


# 渲染函数 h ( )
