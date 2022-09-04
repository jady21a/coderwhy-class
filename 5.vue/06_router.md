# 路由历史
网络工程在架构一个网络时，非常重要的两个设备就是路由器和交换机。

路由器主要就是维护一个映射表；(给设备分配一个唯一的 ip 地址以供传输数据 )
![[Pasted image 20220904000739.png]]

路由经历了不同阶段
## 后端路由
一个页面有自己对应的网址, 也就是 URL；
服务器会通过正则对该 URL 进行匹配, 并且最后交给一个 Controller 进行处理, 最后生成 HTML 或者数据并返回给浏览器

优点: 服务器渲染好的页面, 不需要单独加载任何的 js 和 css, 可以直接交给浏览器展示, 有利于 SEO 的优化
缺点: 通常情况下 HTML 代码和数据以及对应的逻辑会混在一起, 难以编写和维护

## 前后端分离阶段
前端通过 aja 获取数据, 后端提供 api 返回数据, 前端通过 js 将数据渲染到页面 (目前用的较少)

## 单页面富应用 SPA
在前后端分离的基础上加上了前端路由 (由前端来维护一套路由规则)

# 路由核心
前端路由核心: 改变 url 页面不整体刷新, 只是局部切换组件

## url 的 hash
URL 的 hash 也就是锚点 (#), 本质上是改变 window. location 的 href 属性；
优点:  兼容性好, 老板 ie 都能运行
缺点: 有一个#，显得不像一个真实的路径。

## HTML5 的 history
有六种模式改变 URL 而不刷新页面
forward, back, go, replaceState, pushState, popState


# vue-router
用于设定访问路径, 将路径和组件映射起来
在 vue-router 的单页面应用中, 页面的路径的改变就是组件的切换

## 安装
npm install vue-router


## 使用
### 1. 创建路由对象 (router-->index.js)
```js
const router = createRouter({
  history: createWebHashHistory(),//hash
  // history: createWebHistory(),//history
  routes: [
    { path: "/", redirect: "/aa" },
    { path: "/aa", component: aa },
    {
      path: '/bb',
      component: () => import('../view/bb.vue'),//分包
    },
    {
      name: "cc",
      path: '/cc',
      component: () => import('../view/cc.vue'),
      meta: { name: "jay", age: 25 },
      children: [
       {
          path: '/cc',
          redirect: '/cc/cc1'
        },
        {
          path: 'cc1',///cc/cc1
          component: () => import('../view/cc1.vue')
        },
        {
          path: 'cc2',
          component: () => import('../view/cc2.vue')
        }
      ]
    }
  ]
})
export default router
```

### 2. app.use 让路由生效 (main. js)
![[Pasted image 20220904134130.png]]
### 3. router-view 占位 (App.vue)
![[Pasted image 20220904134349.png]]
### 4. router-link 切换 (App. vue)
![[Pasted image 20220904134434.png]]
### hash 和 history
![[Pasted image 20220904133246.png]]

## 默认路径 (首页)
 根路径 " :/ " + redirect 重定向
![[Pasted image 20220904134504.png]]

## router-link
属性: 
to: 可以是字符串或对象
replace: 替换原页面, (不能返回)
active-class: 激活后的 class, 默认为 router-link-active
exact-active-class: 精准激活时的 class, 默认是 router-link-exact-active
![[Pasted image 20220904151131.png]]
![[Pasted image 20220904151023.png]]
默认类名不需要在元素上再加类名

## 路由懒加载 (分包)
将不需要首屏渲染的组件进行分包处理 (分开打包), 提高首屏渲染速度
分包
![[Pasted image 20220904151359.png]]
分包的命名
![[Pasted image 20220904152216.png]]

## routes 的其他属性
name: 路由记录唯一的名称
meta: 自定义的数据
![[Pasted image 20220904152253.png]]
# 动态路由 (路径)
不同的路径对应相同的组件
![[Pasted image 20220904153843.png]]
## 获取动态路由 (路径)的值
![[Pasted image 20220904155004.png]]
# notFound
不能匹配到的路由 (路径)
path: '/: pathMatch (.* ) * '
如果加最后一个* 会将路径解析为字符串
![[Pasted image 20220904004852.png]]

们可以通过 $route. params. pathMatch 获取到传入的参数
![[Pasted image 20220904155554.png]]
# 路由嵌套 children
![[Pasted image 20220904155834.png]]

# 代码实现页面跳转
click
![[Pasted image 20220904160944.png]]
1. 路径
![[Pasted image 20220904005303.png]]
2. 对象
![[Pasted image 20220904005319.png]]

3. setup 中
 ![[Pasted image 20220904005401.png]]

# query
![[Pasted image 20220904005448.png]]

