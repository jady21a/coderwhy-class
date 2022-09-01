# Options API 的缺点
Options API 的一大特点就是在对应的属性中编写对应的功能模块
如 data 定义数据、methods 中定义方法、computed 中定义计算属性、watch 中监听属性改变
当我们实现某一个功能时，这个功能对应的代码逻辑会被拆分到各个属性中, 不利于维护

# Composition API
 Composition API 可以将一个功能的相关代码都放在一起
## setup
在 Vue 组件中，Composition API 就是用 setup 函数实现的
setup 可以代替大部分 option api , 如 methods、computed、watch、data、生命周期等

 setup 中不能使用 this, 因为 setup 函数没有绑定this

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

### reactive api (响应 api)
创建响应式代理
vue 不会跟踪定义的变量的变化, 所以这时没有双向绑定
要为在 setup 中定义的变量提供响应式特性 (双向绑定), 需要使用 reactive 函数
这是因为当我们使用 reactive 函数处理我们的数据之后，数据再次被使用时就会进行依赖收集；

事实上， data 选项，也是在内部交给了 reactive 函数实现的双向绑定

### ref api (引用响应对象)
reactive API 对传入的类型是有限制的，它要求我们必须传入的是一个对象或者数组类型： 
 如果我们传入一个基本数据类型（String、Number、Boolean）会报一个警告

ref 会返回一个可变的响应式对象
注意
在模板中引入 ref 的值时，Vue 会自动帮助我们进行解包操作，所以我们并不需要在模板中通过 ref. value 的方式来使用
但是在 setup 函数内部，它依然是一个 ref 引用，所以对其进行操作时，我们依然需要使用 ref. value 的方式

模板中的解包是浅层的解包

unref: 要获取一个 ref 引用中的 value

### toRefs
将 reactive 返回的对象中的属性都转成 ref；
使解构后的数据变成响应式的
如果对 reactive 返回的对象进行解构获取值, 那么之后无论是修改结构后的变量，还是修改 reactive 返回的 state 对象，数据都不再是响应式的：

toRef 
只转换 reactive 中的某一个属性为 ref

### readonly
只读, 能用不能改
如 const info = readonly (obj)
info 不能改, 但 obj 可改
其实本质上就是 readonly 返回的对象的 setter 方法被劫持了而已

readonly 传入的参数可以为
普通对象, reactive 返回的对象, ref 的对象

应用: 
子组件可以修改父组件的内容, 但这其实是不希望的, 此时可以用 readonly 来防止内容被子组件修改



### 判断 api
- isProxy (检查对象是否是由 reactive 或 readonly 创建的 proxy)
- isReactive (检查是否是 reactive 创建的代理)
- isRef (判断值是否是一个 ref 对象)
- isReadonly ( 检查对象是否是由 readonly 创建的只读代理 )
- toRaw ( 返回 reactive 或 readonly 代理的原始对象)
- shallowReactive (不执行嵌套对象的深层响应式转换 
- shallowRef (创建一个浅层的 ref 对象 )
- shallowReadonly (不执行嵌套对象的深度只读转换)
- triggerRef (手动触发和 shallowRef 相关联的副作用：) ![[Pasted image 20220902000833.png]]

