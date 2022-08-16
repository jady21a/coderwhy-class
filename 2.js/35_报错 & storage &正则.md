# 报错方法
return 的报错只能是 undefined, 调用者不知道是因为函数内部没有正常执行因此需要其他报错方法

## throw 异常
throw 语句用于抛出一个用户自定义的异常
遇到 throw 语句时，当前的函数执行会被停止（throw 后面的语句不会执行）
throw expression
throw 的 expression 表达式可以为 number, string, Boolean, 对象

### Error 类
JavaScript 已经给我们提供了一个 Error 类，我们可以直接创建这个类的对象
属性:
- message：创建 Error 对象时传入的 message；
- name: Error 的名称，通常和类的名称一致；
- stack : 整个 Error 的错误信息，包括函数的调用栈，当我们直接打印 Error 对象时，打印的就是 stack；
![[Pasted image 20220806141140.png]]

子类
-  RangeError：下标值越界时使用的错误类型； 
-  SyntaxError：解析语法错误时使用的错误类型；
-  TypeError：出现类型错误时，使用的错误类型；

## 捕获异常
![[Pasted image 20220806141109.png]]

# storage
- localStorage：本地存储，提供的是一种永久性的存储方法，在关闭掉网页重新打开时，存储的内容依然保留；
- sessionStorage：会话存储，提供的是本次会话的存储，在关闭掉会话时，存储的内容会被清除；
![[Pasted image 20220808145948.png]]
二者区别
1. 关闭网页后重新打开，localStorage 会保留，而 sessionStorage 会被删除；
2. 在页面内实现跳转，localStorage 会保留，sessionStorage 也会保留
3. 在页面外实现跳转（打开新的网页），localStorage 会保留，sessionStorage 不会被保留；
![[Pasted image 20220808145921.png]]
属性:  length
方法: 
- key (index)
- getItem ( )
- setItem ( )
- removeItem ( )
- clear ( )
![[Pasted image 20220808151822.png]]
# 正则表达式
https://c.runoob.com/front-end/854/   正则测试

Regular Expression，常简写为 regex、regexp 或 RE
正则表达式使用单个字符串来描述、匹配一系列匹配某个句法规则的字符串。
正则表达式是一种字符串匹配利器，可以帮助我们搜索、获取、替代字符串
![[Pasted image 20220816160944.png]]
## 方法
test ,exec  (    re1. exec (a)  )
match, repalce, split    (  a. match (re1)  )
![[Pasted image 20220815135347.png]]
![[Pasted image 20220816161017.png]]
## flag 修饰符
![[Pasted image 20220815135530.png]]

## 规则
### 字符类  
\\d \\s \\w   .
![[Pasted image 20220815135651.png]]
注意 " . " 不需要转义
\\d = [0-9]
\\w = [a-zA-Z0-9]
![[Pasted image 20220816161047.png]]

![[Pasted image 20220815135719.png]]

### 锚点 ^ $
- 符号 ^ 匹配文本开头
- 符号 $  匹配文本末尾
- 词边界   \\ b
![[Pasted image 20220816161102.png]]
### 转义字符  "\\" 
![[Pasted image 20220815140204.png]]
![[Pasted image 20220816161115.png]]
### Sets 和 Ranges  [ ]
集合（Sets）[ ... ] : 搜索方框中的任意一个字符          eg: [abcdc123]
范围（Ranges）  如:[a-z] , [0-5], [0-9A-F]
![[Pasted image 20220816161125.png]]
### 量词 {n}
 确切的位数：{5} 
 某个范围的位数：{3, 5}
![[Pasted image 20220816161144.png]]
-  +：代表“一个或多个”，相当于 {1,} 
-  ?：代表“零个或一个”，相当于 {0, 1}。换句话说，它使得符号变得可选； 
-  *：代表着“零个或多个”，相当于 {0,}。也就是说，这个字符可以多次出现或不出现；

### greedy 和 lazy 模式
贪婪 (greedy) 模式  
从头直接匹配到尾
![[Pasted image 20220816161209.png]]
懒惰 (lazy) 模式
只要获取到对应的内容后，就不再继续向后匹配
在量词后面再加一个问号‘?’来启用 lazy 模式
所以匹配模式变为 *?  ,+?， ??


### 捕获组 (...)
作用:
 它允许将匹配的一部分作为结果数组中的单独项；
 它将括号视为一个整体；
- 捕获组命名   ----在第一个括号之后加 ?\<name>  
- 非捕获组   -----在开头添加 ?: 来排除组。

或 or ---- |
![[Pasted image 20220816161255.png]]

## 例
歌词解析
[123.207.32.32:9001/lyric?id=167876](http://123.207.32.32:9001/lyric?id=167876)
更改 id 即可获得对应歌词
