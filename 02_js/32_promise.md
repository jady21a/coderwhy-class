# 认识 Promise
es5
![[Pasted image 20220724134936.png]]
Promise 是一个类，可以翻译成承诺、许诺、期约；
在通过 new 创建 Promise 对象时，我们需要传入一个回调函数，我们称之为 executor
-  这个回调函数会被立即执行，并且给传入另外两个回调函数 resolve、reject；
- 当我们调用 resolve 回调函数时，会执行 Promise 对象的 then 方法传入的回调函数； 
- 当我们调用 reject 回调函数时，会执行 Promise 对象的 catch 方法传入的回调函数；
![[Pasted image 20220724135008.png]]
# Promise 状态
以下状态都位于 executor 回调函数中
-  待定（pending）: 初始状态，既没有被兑现，也没有被拒绝； 
	✓ 当执行 executor 中的代码, 且没有确定 resolve 和 reject 时，处于该状态； 
-  已兑现（fulfilled）: 意味着操作成功完成； 
	✓ 执行了 resolve (决议 (why 用语), 解决) 时，处于该状态，Promise 已经被兑现； 
-  已拒绝（rejected）: 意味着操作失败； 
	✓ 执行了 reject 时，处于该状态，Promise 已经被拒绝；

N: promise 只有一个状态, 一旦状态被确定下来，Promise 的状态会被锁死
![[Pasted image 20220724135033.png]]
# Executor
Executor 是在创建 Promise 时需要传入的一个回调函数，这个回调函数会被立即执行，并且传入两个参数：
![[Pasted image 20220724135430.png]]
通常我们会在 Executor 中确定我们的 Promise 状态：

## resolve 传入的值
- resolve 传入值为普通值或对象, 那么这个值会作为 then 回调的参数
- resolve 传入值为另一个 Promise, 那么这个传入的 Promise 会决定原 Promise 的状态：
- thenable: resolve 传入值为对象, 且该对象中有实现 then 方法, 那么会执行该 then 方法，并且根据 then 方法的结果来决定 Promise 的状态：
![[Pasted image 20220724134748.png]]

# promise 的方法
## 实例方法
存放在 Promise 的 prototype 上
### then 方法
它其实是放在 Promise 的原型上的 Promise. prototype. then
![[Pasted image 20220725110154.png]]
如果是 fulfilled 状态 , 可以多次调用, 每次调用都会被执行
![[Pasted image 20220725120115.png]]
##### 返回值
then 方法的返回值是一个 Promise, 因此可以进行链式调用
then 方法返回的 Promise 的状态
-  当 then 方法中的回调函数本身在执行的时候，那么它处于 pending 状态； 
-  当 then 方法中的回调函数返回一个结果时，那么它处于 fulfilled 状态，并且会将结果作为 resolve 的参数； 
	- ✓ 情况一：返回一个普通的值； 
	- ✓ 情况二：返回一个 Promise； 
	- ✓ 情况三：返回一个 thenable 值； 
-  当 then 方法抛出一个异常时，那么它处于 reject 状态；
 ![[Pasted image 20220725122010.png]]


### catch 方法
放在 Promise 的原型上的 Promise. prototype. catch
是可以被多次调用, 当 Promise 的状态变成 reject 的时候，这些回调函数都会被执行；
#### 返回值
catch 方法也是会返回一个 Promise 对象的，所以 catch 方法后面我们可以继续调用 then 方法或者 catch 方法
![[Pasted image 20220726012527.png]]
中断函数执行
![[Pasted image 20220726012445.png]]
### finally  (es9)
Promise 对象无论变成 fulfilled 还是 rejected 状态，最终都会被执行的代码。
◼ finally 方法是不接收参数的，因为无论前面是 fulfilled 状态，还是 rejected 状态，它都会执行。
![[Pasted image 20220726013000.png]]
## 类方法
### resolve
 Promise. resolve 的用法相当于 new Promise，并且执行 resolve 操作：
实例方法需要 new promise, 而类方法不需要 new, 可以直接使用 promise. resolve
resolve 参数
- 普通值或对象
- promise
- thenable
![[Pasted image 20220726014139.png]]
### reject
将 Promise 对象的状态设置为 reject 状态。
Promise. reject 的用法相当于 new Promise，并且执行 reject：
Promise. reject 传入的参数无论是什么形态，都会直接作为 reject 状态的参数传递到 catch 。
![[Pasted image 20220726015114.png]]
### all
将多个 Promise 包裹在一起形成一个新的 Promise；
新的 Promise 状态由包裹的所有 Promise 共同决定:
- 若全为 fulfilled, 则新的 promise 为 fulfilled, 并将所有 Promise 的返回值组成一个数组
- 若其中有一个 reject, 新的 Promise 状态为 reject，并且会将第一个 reject 的返回值作为参数
![[Pasted image 20220726021415.png]]
### allSettled (es11)
all 方法有一个缺陷：当有其中一个 Promise 变成 reject 状态时，新 Promise 就会立即变成对应的 reject 状态
那么对于 resolved 的，以及依然处于 pending 状态的 Promise，我们是获取不到对应的结果的；

allSettled 在所有的 Promise 都有结果（settled），无论是 fulfilled，还是 rejected 时，才会有最终的状态；
![[Pasted image 20220726021449.png]]
打印对象中包含 status 状态，以及对应的 value 值；
注意: all 和 allsettled 最终的排序与执行时间无关, 而与数组中的顺序有关
![[Pasted image 20220726022042.png]]
### race
谁先有结果，那么就使用谁的结果
![[Pasted image 20220726022409.png]]
### any (es12)
等到一个 fulfilled 状态，才会决定新 Promise 的状态；
如果所有的 Promise 都是 reject 的，那么也会等到所有的 Promise 都变成 rejected 状态后报一个 AggregateError 的错误
![[Pasted image 20220726022751.png]]