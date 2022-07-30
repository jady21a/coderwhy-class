# proxy
## 响应式
监听内容的改变, 当内容改变时页面显示也随之改变

监听对象
es5: Object. defineProperty
![[Pasted image 20220719195813.png]]
缺点:
Object. defineProperty 设计的初衷，不是为了去监听
不能监听新增属性、删除属性

## es6: proxy
如果我们希望监听一个对象的相关操作，那么我们可以先创建一个代理对象（Proxy 对象）；
`const p = new Proxy (target, handler)` `
之后对该对象的所有操作，都通过代理对象来完成，代理对象可以监听我们想要对原对象进行哪些操作
![[Pasted image 20220719201956.png]]
proxy 的 set 和 get
set 的参数: 
- target (监听对象), 
- property (将被设置的属性 key), 
- value (新属性值)
- receiver (调用的代理对象)

get 的参数:
- target (监听对象), 
- property (将被设置的属性 key), 
- receiver (调用的代理对象)

## proxy 捕获器
![[Pasted image 20220719192841.png]]
![[Pasted image 20220720113325.png]]
## Proxy 的 construct 和 apply
应用于函数对象
![[Pasted image 20220720113239.png]]


# reflect 反射
它主要提供了很多操作 JavaScript 对象的方法，有点像 Object 中操作对象的方法；
如 Reflect. getPrototypeOf (target) 类似于 Object. getPrototypeOf ()；
如 Reflect. defineProperty (target, propertyKey, attributes) 类似于 Object. defineProperty () ；
![[Pasted image 20220720113221.png]]
有 Object 可以做这些操作，那么为什么还需要有 Reflect 这样的新增对象呢？
Object 作为一个构造函数，那些操作实际上放到它身上并不合适
些类似于 in、delete 操作符，让 JS 看起来是会有一些奇怪
所以在 ES6 中新增了 Reflect，让我们这些操作都集中到了 Reflect 对象上；
另外在使用 Proxy 时，可以做到不操作原对象
[比较 Reflect 和 Object 方法 - JavaScript | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect/Comparing_Reflect_and_Object_methods)
![[Pasted image 20220720114104.png]]
## 常见方法
![[Pasted image 20220719193907.png]]


## receiver 的作用
如果我们的源对象（obj）有 setter、getter 的访问器属性，那么可以通过 receiver 来改变里面的 this；(原 this 指向 obj, 改变后指向 proxyObj )
![[Pasted image 20220721232349.png]]
## Reflect 的 construct
![[Pasted image 20220721184310.png]]