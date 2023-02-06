 https://zh-hans.reactjs.org/

# react 特点
## 声明式编程
当状态改变时，React 可以根据最新的状态去渲染我们的 UI 界面；
![[Pasted image 20221010172948.png|600]]

## 组件化
将复杂的界面拆分成一个个小的组件

## 多平台适配
react --> web 
ReactNative -->移动端跨平台 (目前 flutter 更好用)
ReactVR --> 虚拟现实 Web

# react 开发依赖
 react：包含 react 所必须的核心代码 
 react-dom：react 渲染在不同平台所需要的核心代码 
 babel：将 jsx 转换成 React 代码的工具

## 引入
1. cdn
```html
<script src="https://unpkg.com/react@18/umd/react.development.js" crossorigin></script>
<script src="https://unpkg.com/react-dom@18/umd/react-dom.development.js" crossorigin></script>
<script src=" https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```
2. 下载后本地引入
3. npm


# demo 代码片段
[snippet generator (snippet-generator.app)](https://snippet-generator.app/)
```jsx
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <div id="root"></div>

  <script crossorigin src="https://unpkg.com/react@18/umd/react.development.js"></script>
  <script crossorigin src="https://unpkg.com/react-dom@18/umd/react-dom.development.js"></script>
  <script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>

  <script type="text/babel">
    class App extends React.Component{
      constructor(){
        super()
        this.state={
          aa:"hello world"
        }
        this.btnClick=this.btnClick.bind(this)
      }
      btnClick(){
          this.setState({
            aa:"hi react"
          })
        }
      render(){
        const { aa } = this.state
        return(
          <div>
            <h3>{aa}</h3>
          </div>
        )
      }
    }
    const root = ReactDOM.createRoot(document.querySelector("#root"))
    root.render(<App/>)
  </script>

</body>
</html>
```


## 插件快捷键 (es7 + React/Redux/React-Native)
[vscode-react-javascript-snippets/Snippets.md at 185bb91a0b692c54136663464e8225872c434637 · chillios-ts/vscode-react-javascript-snippets (github.com)](https://github.com/chillios-ts/vscode-react-javascript-snippets/blob/HEAD/docs/Snippets.md)

### rce
react class export components
![[Pasted image 20221101125424.png]]

### 解构对象简写 dob
destructionObject
![[Pasted image 20230206002720.png]]