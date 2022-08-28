# vue
用于构建用户界面的渐进式 JavaScript 框架。
渐进式, 声明式的、组件化, 的编程模型
渐进式: 可以在项目中一点点来引入和使用 Vue，而不一定需要全部使用 Vue 来开发整个项目

# 引入
 方式一：在页面中通过 CDN 的方式来引入；
<script src="https://unpkg.com/vue@next"></script>
 方式二：下载 Vue 的 JavaScript 文件，并且自己手动引入；
![[Pasted image 20220826220250.png]]
 方式三：通过 npm 包管理工具安装使用它； 
 方式四：直接通过 Vue CLI 创建项目，并且使用它； ![[Pasted image 20220826220353.png]]

# 声明式和命令式
命令式编程关注的是 “how to do”
声明式编程关注的是 “what to do”, 由框架 (机器) 完成 “how”的过程；

原生 js 每完成一个操作，都需要通过 JavaScript 编写一条代码来给浏览器一个指令

vue在 createApp 传入的对象中声明需要的内容，模板 template、数据 data、方法 methods

# MVVM
MVC 是 Model – View –Controller 的简称
![[Pasted image 20220826222929.png]]
MVVM 是 Model-View-ViewModel 的简称
![[Pasted image 20220826222515.png]]
# 生成代码片段
1. 复制自己需要生成代码片段的代码
2. https://snippet-generator.app/
3. 在 VSCode 中配置代码片段
![[Pasted image 20220826142420.png]]
![[Pasted image 20220826142649.png]]

# 虚拟 DOM
VNode (Virtual Node) 的本质是一个 JavaScript 的对象；
![[Pasted image 20220827221235.png]]
vnode 会形成跟真实 dom 一样的 dom tree

# 快捷建议 snip
![[Pasted image 20220827145322.png]]


# 属性
## data
传入一个函数，并且该函数需要返回一个对象
data 中返回的对象会被 Vue 的响应式系统劫持，之后对该对象的修改或者访问都会在劫持中被处理：所以修改 counter 的值时，app 中的 {{counter}} 也会发生改变；
![[Pasted image 20220826234919.png]]
## methods
methods属性是一个对象，通常我们会在这个对象中定义很多的方法：
这些方法可以被绑定到模板中；
在该方法中，可以使用 this 关键字来直接访问到 data 中返回的对象的属性

methods 中的函数不能使用匿名函数, 因为匿名函数 this 指向 window

## computed
在模板中可以直接通过插值语法显示一些 data 中的数据。
有些情况需要对数据进行一些转化后再显示，或者需要将多个数据结合起来进行显示, 这个时候应使用 computed
![[Pasted image 20220828103335.png]]
computed 和 methods
computed 有缓存, 如果数据没有变化, computed 不需要重新计算, 而 methods 每次都需要重新计算

computed 的get 和 set
![[Pasted image 20220828104343.png]]
## watch 
侦听器: 在代码逻辑中监听某个数据的变化
![[Pasted image 20220828112100.png]]

deep 和 immediate
![[Pasted image 20220828112145.png]]

$watch
在 created 的生命周期中，使用 this.$watchs 来侦听；
 第一个参数是要侦听的源； 
 第二个参数是侦听的回调函数 callback； 
 第三个参数是额外的其他选项，比如 deep、immediate；
![[Pasted image 20220828112847.png]]
## 其他属性
如 props、computed、watch、emits、setup , components等


# 组件
我们将一个完整的页面分成很多个组件；
 每个组件都用于实现页面的一个功能块； 
 而每一个组件又可以进行细分； 
 而组件本身又可以在多个地方进行复用；

app 对象其实本质上就是一个组件，也是我们应用程序的根组件；
![[Pasted image 20220828222922.png]]
## 注册组件

 全局组件：在任何其他的组件中都可以使用的组件； 
 局部组件：只有在注册的组件中才能使用的组件；

### 组件名
1. 使用 kebab-case（短横线分割符）如: my-component-name  (推荐)
2. 使用 PascalCase（大驼峰标识符）如: MyComponentName

### 注册全局组件
![[Pasted image 20220829000823.png]]

![[Pasted image 20220828223633.png]]


### 注册局部组件
![[Pasted image 20220829001808.png]]
![[Pasted image 20220828223557.png]]


## 单文件组件
后缀名为 . vue 的 single-file components (单文件组件)
单文件的特点:
 代码的高亮； 
 ES6、CommonJS 的模块化能力； 
 组件作用域的 CSS； 
 可以使用预处理器来构建更加丰富的组件，比如 TypeScript、Babel、Less、Sass 等；


使用单文件组件的方法:
1. Vue CLI 创建项目, 项目会默认帮助我们配置好所有的配置选项，可以在其中直接使用. vue 文件；
2. 自己使用 webpack 或 rollup 或 vite 这类打包工具，对其进行打包处理

VSCode 使用单文件组件的插件
 插件一：Vetur，从 Vue2 开发就一直在使用的 VSCode 支持 Vue 的插件； 
 插件二：Volar，官方推荐的插件；

## vue-cli
全局安装:
npm install @vue/cli -g
升级 vue cli:
npm update @vue/cli -g
创建项目:
Vue create 项目的名称

![[Pasted image 20220828233131.png]]
![[Pasted image 20220828233505.png]]

![[Pasted image 20220828233820.png]]