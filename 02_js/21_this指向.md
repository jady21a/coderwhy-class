# this 绑定
函数在调用时，JavaScript 会默认给 this 绑定一个值;
this 的绑定和定义的位置（编写的位置）没有关系；
this 的绑定和调用方式以及调用的位置有关系; 
即 this 是在运行时被绑定的；

## 默认绑定 (default binding)
独立函数调用 (函数没有被绑定到某个对象上进行调用 ) 时为默认绑定。
![[Pasted image 20220606190916.png]]
## 隐式绑定 (Implicit Binding)
通过某个对象进行调用
![[Pasted image 20220606195637.png]]
## 显式绑定 (explicit binding)
隐式绑定时函数是作为对象的一个属性, 如果想要函数不在对象内部, 且需要调用函数, 则可以用显式绑定
### call, apply, bind
![[Pasted image 20220606171438.png]]
![[Pasted image 20220606171445.png]]
![[Pasted image 20220606202041.png]]
## new 绑定
使用 new 关键字来调用函数时
1. 创建一个全新的对象；
2. 这个新对象会被执行 prototype 连接
3. 这个新对象会绑定到函数调用的 this 上（this 的绑定在这个步骤完成）
4. 4. 如果函数没有返回其他对象，表达式会返回这个新对象
![[Pasted image 20220606195750.png]]

# 内置函数的绑定
setTimeout、数组的 forEach、点击监听
![[Pasted image 20220606201328.png]]
# 绑定优先级
从低到高
默认<隐式<显式 ( call=apply<bind)< new
new 不可以和 apply/call 一起使用, 但是 new 高于 bind
![[Pasted image 20220606202754.png]]
# 规则之外 (不按优先级规则)
-  显示绑定中，传入 null 或 undefined, 忽略显式绑定 ![[Pasted image 20220606204112.png]]
- 间接 (indirect)函数引用 ![[Pasted image 20220606204132.png]]
- 箭头 (arrow)函数 [[06.函数1]]
	- 箭头函数不绑定 this，而是根据外层作用域来决定 this。![[Pasted image 20220606184545.png]]
	- ![[Pasted image 20220606184637.png]]


----
# 面试题

1. ![[Pasted image 20220607130505.png]]
2. ![[Pasted image 20220607130545.png]]  ![[Pasted image 20220607130637.png]]       
3. ![[Pasted image 20220607130712.png]]  ![[Pasted image 20220607130737.png]]
4. ![[Pasted image 20220607130805.png]]  ![[Pasted image 20220607130820.png]]