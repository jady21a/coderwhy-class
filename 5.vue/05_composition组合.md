# Options API 的缺点
Options API 的一大特点就是在对应的属性中编写对应的功能模块
如 data 定义数据、methods 中定义方法、computed 中定义计算属性、watch 中监听属性改变
当我们实现某一个功能时，这个功能对应的代码逻辑会被拆分到各个属性中, 不利于维护

# Composition AP
 Composition API 可以将一个功能的相关代码都放在一起