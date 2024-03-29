# jsx 是什么
 JSX 是一种 JavaScript 的语法扩展extension
 使 js 中可以使用 html (html in js)
 ![[Pasted image 20221010205354.png]]
## 书写注意
- JSX 的顶层只能有一个根元素
- 我们通常在 jsx 的外层包裹一个小括号 (), 这为了方便阅读，而且可以换行书写
- jsx 中可以是单标签或双标签

## 本质
实际上，jsx 仅仅只是 React. createElement (type, config, children) 函数的语法糖。
参数
- type  eg: div /span/h3
- config eg: className
- children 标签中的内容
### 虚拟 DOM
由 React. createElement 创建出的 js 代码 (一个对象) 就是虚拟 DOM,
react 的虚拟 DOM 可以 (打印) console. log ( ) 出来
### 虚拟 DOM 的作用
1. diff 算法 , 决定要更新哪些东西
2. 虚拟 dom 方便跨平台渲染
3. 声明式编程

# 使用
## 注释
{ /*这是注释*/ }
![[Pasted image 20221010205820.png]]
## 标签内嵌入变量 (插入内容)
1. 若变量是 Number、String、Array 类型时，可以直接显示
2. 若变量是 null、undefined、Boolean 类型时，内容为空
	将 null/undefined/Boolean 转为字符串显示的方法:  toString/ +" " (字符串拼接) /String ![[Pasted image 20221010210653.png]]
3. Object 对象类型不能作为子元素 (但是可以插入对象的具体 key) ![[Pasted image 20221010210714.png]]
4. 插入表达式 
	- 运算表达式
	- 三元运算符
	- 执行函数
	![[Pasted image 20221010210844.png]]

## 标签绑定属性
title/src/href/class/style 
```jsx
render() {
	const { title, imgURL, href, isActive, objStyle } = this.state

	// 需求: isActive: true -> active
	// 1.class绑定的写法一: 字符串的拼接
	const className = `abc cba ${isActive ? 'active': ''}`
	// 2.class绑定的写法二: 将所有的class放到数组中
	const classList = ["abc", "cba"]
	if (isActive) classList.push("active")
	// 3.class绑定的写法三: 第三方库classnames -> npm install classnames

	return (
		<div>
			{ /* 1.基本属性绑定 */ }
			<h2 title={title}>我是h2元素</h2>
			{/*<img src={imgURL} alt=""/>*/}
			<a href={href}>百度一下</a>


			{ /* 2.绑定class属性: 最好使用className */ }
			<h2 className={className}>哈哈哈哈</h2>
			<h2 className={classList.join(" ")}>哈哈哈哈</h2>


			{ /* 3.绑定style属性: 绑定对象类型 */ }
			<h2 style={{color: "red", fontSize: "30px"}}>呵呵呵呵</h2>
			<h2 style={objStyle}>呵呵呵呵</h2>
		</div>
	)
}

```

## this 为 undefined
构造函数内部的 this，会指向创建出来的新对象；
但是继承的类里面的函数中的 this 指向 undefined, 因为严格模式下独立调用的函数 this 指向 undefined,class 默认为严格模式
![[Pasted image 20221011161041.png]]
非严格模式下独立调用的函数 this 指向 window

### 解决 this 为 undefine
1. 显示绑定 bind
2. es6 的 class fields 语法 (外部箭头函数) ![[Pasted image 20221011162025.png]]
3. 箭头函数 (内部箭头函数)
![[Pasted image 20221011161807.png]]

### 参数传递
event 是默认会传递的参数
![[Pasted image 20221011165548.png]]

## 条件渲染
### if
![[Pasted image 20221011174713.png]]
### 三元运算符
![[Pasted image 20221011174727.png]]
### &&
有值才渲染, 如果是 undefined, null 则不渲染
![[Pasted image 20221011174738.png]]
### v-show 的效果
```jsx
<h3 style={{display:isShow? 'block':'none'}}>aaaaaaa</h3>
```





-----
# 案例
## 动态样式
![[Pasted image 20221011180954.png]]
```jsx
  <script type="text/babel">
    class App extends React.Component{
      constructor(){
        super()
        this.state={
          arr:["aa","bb","cc","dd"],
          currentIndex:0
        }
      }
      itemClick(index){
          this.setState({currentIndex:index })
        }
      render(){
        const { arr,currentIndex } = this.state
        return(
          <div>
            <ul>
              {arr.map((item,index)=>{
                return(
                  <li className={currentIndex===index?'active':''} key={item} onClick={()=>this.itemClick(index)}>{item}</li>
                )
              })}
            </ul>
          </div>
        )
      }
    }
    const root = ReactDOM.createRoot(document.querySelector("#root"))
    root.render(<App/>)
  </script>
```
## 购书
![[Pasted image 20221011193630.png]]

