# Options API 的缺点
Options API 的一大特点就是在对应的属性中编写对应的功能模块
如 data 定义数据、methods 中定义方法、computed 中定义计算属性、watch 中监听属性改变
当我们实现某一个功能时，这个功能对应的代码逻辑会被拆分到各个属性中, 不利于维护

# Composition API
 Composition API 可以将一个功能的相关代码都放在一起
## setup
在 Vue 组件中，Composition API 就是用 setup 函数实现的
setup 可以代替大部分 option api , 如 methods、computed、watch、data、生命周期等

### 参数
- props (参数)
父组件传递过来的属性会被放到 props 对象中，我们在 setup 中如果需要使用，就可以直接通过 props 参数获取：
- context (上下文)
	- atrrs: 所有非 props 的 attribute
	- slots: 父组件传递过来的插槽
	- emit: 子组件发出事件用（因为不能访问 this，所以不可以再通过 this.$emit 发出事件）

### 返回值
setup 的返回值可以在模板 template 中被使用
也就是说通过 setup 的返回值来替代 data 选项
甚至可以返回一个执行函数来代替在 methods 中定义的方法

### reactive api
vue 不会跟踪定义的变量的变化, 所以这时没有双向绑定
要为在 setup 中定义的变量提供响应式特性 (双向绑定), 需要使用 reactive 函数
