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

## 其他属性
如 props、computed、watch、emits、setup 等

