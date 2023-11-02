---
title: React拓展
categories:
  - 前端
  - React
  - React拓展
tags: React拓展
abbrlink: 176947605
date: 2023-11-02 14:28:47
---

## setState

**1. `setState` 更新状态的两种写法**

**(1). `setState(stateChange, [callback])` - 对象式的 `setState` 📦**
   - `stateChange` 为状态改变对象（该对象可以体现出状态的更改）.
   - `callback` 是可选的回调函数, 它在状态更新完毕并且界面也更新后（✅ `render` 调用后）才被调用.

**(2). `setState(updater, [callback])` - 函数式的 `setState` 🔄**
   - `updater` 为返回 `stateChange` 对象的函数.
   - `updater` 可以接收到当前的 `state` 和 `props`.
   - `callback` 是可选的回调函数, 它在状态更新以及界面也更新后（✅ `render` 调用后）才被调用.

**总结**:
1. 对象式的 `setState` 是函数式的 `setState` 的简写方式，它是一种语法糖.
2. 使用原则:
   - 如果新状态不依赖于原状态，可以使用对象方式.
   - 如果新状态依赖于原状态，应使用函数方式.
   - 如果需要在 `setState()` 执行后获取最新的状态数据, 可以在第二个回调函数中读取 📊。

**示例：**

```js
import React, { Component } from 'react'

export default class Demo extends Component {

 state = {count:0}

 add = ()=>{
  //一、对象式的setState
   //1.获取原来的count值
  const {count} = this.state
  //2.更新状态
  this.setState({count:count+1},()=>{
   console.log(this.state.count);
  })
  //console.log('输出count',this.state.count); //0

  //二、函数式的setState
  // this.setState( state => ({count:state.count+1}))
 }

 render() {
  return (
   <div>
    <h1>当前求和为：{this.state.count}</h1>
    <button onClick={this.add}>点我+1</button>
   </div>
  )
 }
}
```

## lazyLoad(懒加载)

### 路由组件的lazyLoad

```js
	//1.通过React的lazy函数配合import()函数动态加载路由组件 ===> 路由组件代码会被分开打包
	const Login = lazy(()=>import('@/pages/Login'))
	
	//2.通过<Suspense>指定在加载得到路由打包文件前显示一个自定义loading界面
	<Suspense fallback={<h1>loading.....</h1>}>
        <Switch>
            <Route path="/xxx" component={Xxxx}/>
            <Redirect to="/login"/>
        </Switch>
    </Suspense>
```

**示例：**

```js
// lazy 是 React 的一个函数，允许你将组件进行动态导入，从而实现代码分割
// Suspense 是 React 的一个组件，用于处理异步操作的等待和错误处理。
// 它最初是为懒加载组件而引入的，但也可用于其他异步操作，例如数据获取。
import React, { Component,lazy,Suspense} from 'react'
import {NavLink,Route} from 'react-router-dom'

// import Home from './Home'
// import About from './About'
// 引入组件的方式需要改变
import Loading from './Loading'
const Home = lazy(()=> import('./Home') )
const About = lazy(()=> import('./About'))

export default class Demo extends Component {
 render() {
  return (
   <div>
    <div className="row">
     <div className="col-xs-offset-2 col-xs-8">
      <div className="page-header"><h2>React Router Demo</h2></div>
     </div>
    </div>
    <div className="row">
     <div className="col-xs-2 col-xs-offset-2">
      <div className="list-group">
       {/* 在React中靠路由链接实现切换组件--编写路由链接 */}
       <NavLink className="list-group-item" to="/about">About</NavLink>
       <NavLink className="list-group-item" to="/home">Home</NavLink>
      </div>
     </div>
     <div className="col-xs-6">
      <div className="panel">
       <div className="panel-body">
        {/* 可以简单写个Loding组件用于展示加载动画 */}
        <Suspense fallback={<Loading/>}>
         {/* 注册路由 */}
         <Route path="/about" component={About}/>
         <Route path="/home" component={Home}/>
        </Suspense>
       </div>
      </div>
     </div>
    </div>
   </div>
  )
 }
}
```

## Hooks

### React Hook/Hooks是什么? 🎣

- Hook是React 16.8.0版本增加的新特性/新语法。
- 可以让你在函数组件中使用state以及其他的React特性。

### 三个常用的Hook 🛠️

- State Hook: `React.useState()`
- Effect Hook: `React.useEffect()`
- Ref Hook: `React.useRef()`

### State Hook 📊

- State Hook让函数组件也可以有state状态，并进行状态数据的读写操作。
- 语法: `const [xxx, setXxx] = React.useState(initValue)`
- `useState()` 说明:
   - 参数: 第一次初始化指定的值在内部作缓存。
   - 返回值: 包含2个元素的数组，第1个为内部当前状态值，第2个为更新状态值的函数。
- `setXxx()` 2种写法:
   - `setXxx(newValue)`: 参数为非函数值，直接指定新的状态值，内部用其覆盖原来的状态值。
   - `setXxx(value => newValue)`: 参数为函数，接收原本的状态值，返回新的状态值，内部用其覆盖原来的状态值。

**示例：**

```js
// 引入React
import React from 'react'
// 类式组件
// export default class Count extends React.Component {
//   state={
//     count:0
//   }
//   add=()=>{
//     const {count} = this.state
//     this.setState({count:count+1})
//   }
//     render() {
//     return (
//       <div>
//         <h2>Count组件</h2>
//         <h2>当前求和为：{this.state.count}</h2><br></br>
//         <button onClick={this.add}>点我+1</button>
//       </div>
//     )
//   }
// }
// 函数式组件
function Demo(){
  const [count,setcount]=React.useState(0)
  function add(){
    setcount(count+1)
  }
  return (
          <div>
            <h2>Count组件</h2>
            <h2>当前求和为：{count}</h2><br></br>
            <button onClick={add}>点我+1</button>
          </div>
      )
}

export default Demo
```

### Effect Hook ⚙️

- Effect Hook可以让你在函数组件中执行副作用操作（用于模拟类组件中的生命周期钩子）。
- React中的副作用操作包括发ajax请求数据获取、设置订阅/启动定时器、手动更改真实DOM等。
- 语法和说明:
  ```javascript
  useEffect(() => {
    // 在此可以执行任何带副作用操作
    return () => {
      // 在组件卸载前执行
      // 在此做一些收尾工作，比如清除定时器/取消订阅等
    }
  }, [stateValue]) // 如果指定的是[]，回调函数只会在第一次render()后执行
  ```
- 可以把 `useEffect` Hook 看做如下三个函数的组合:
  - `componentDidMount()`
  - `componentDidUpdate()`
  - `componentWillUnmount()`

**示例：**

```js
// 引入React
import React from 'react'
import  ReactDOM  from 'react-dom'
// 类式组件
// export default class Count extends React.Component {
//   state={
//     count:0
//   }
//   add=()=>{
//     const {count} = this.state
//     this.setState({count:count+1})
//   }
  // 点击卸载组件
//   unmount=()=>{
//     ReactDOM.unmountComponentAtNode(document.getElementById('root'));
//   }
  // 实现count自增长
//   componentDidMount(){
//     this.timer=setInterval(()=>{
//       this.setState({count:this.state.count+1})
//     },1000)
//   }
//   componentWillUnmount(){
//     clearInterval(this.timer)
//   }
//     render() {
//     return (
//       <div>
//         <h2>Count组件</h2>
//         <h2>当前求和为：{this.state.count}</h2><br></br>
//         <button onClick={this.add}>点我+1</button>
//         <button onClick={this.unmount}>点我卸载组件</button>
//       </div>
//     )
//   }
// }
// 函数式组件
function Demo(){
  const [count,setcount]=React.useState(0)
// 实现挂载组件,count自增长
  React.useEffect(()=>{
    let timer = setInterval(()=>{
      setcount(count=>count+1)
    },1000)
    return ()=>{
      clearInterval(timer)
    }
  },[])
  function add(){
    // 第一种写法
    // setcount(count+1)
    // 第二种写法
    setcount(count=>count+1)
  }
  function unmount(){
        ReactDOM.unmountComponentAtNode(document.getElementById('root'));
  }
  return (
          <div>
            <h2>Count组件</h2>
            <h2>当前求和为：{count}</h2><br></br>
            <button onClick={add}>点我+1</button>
            <button onClick={unmount}>点我卸载组件</button>
          </div>
      )
}

export default Demo
```

**另一种做法：**
```js
import React from 'react';

export default class Count extends React.Component {
  state = {
    count: 0,
    showComponent: true,
  };

  add = () => {
    const { count } = this.state;
    this.setState({ count: count + 1 });
  }

  toggleComponent = () => {
    this.setState((prevState) => ({
      showComponent: !prevState.showComponent,
    }));
  }

  render() {
    const { count, showComponent } = this.state;

    return (
      <div>
        <h2>Count组件</h2>
        {showComponent && (
          <div>
            <h2>当前求和为：{count}</h2>
            <br></br>
            <button onClick={this.add}>点我+1</button>
          </div>
        )}
        <button onClick={this.toggleComponent}>
          {showComponent ? '隐藏组件' : '显示组件'}
        </button>
      </div>
    );
  }
}
```

### Ref Hook 🔄

- Ref Hook可以在函数组件中存储/查找组件内的标签或任意其它数据。
- 语法: `const refContainer = React.useRef()`.
- 作用: 保存标签对象，功能与`React.createRef()`一样。

**示例：**

```js
// 引入React
import React, { useRef } from 'react'
import  ReactDOM  from 'react-dom'
// 类式组件
// export default class Count extends React.Component {
//   state={
//     count:0
//   }
//   add=()=>{
//     const {count} = this.state
//     this.setState({count:count+1})
//   }
//   myRef=React.createRef()
//   // 点击卸载组件
//   unmount=()=>{
//     ReactDOM.unmountComponentAtNode(document.getElementById('root'));
//   }
//   // 提示输入内容
//   showdata=()=>{
//     alert(this.myRef.current.value)
//   }
//   // 实现count自增长
//   componentDidMount(){
//     this.timer=setInterval(()=>{
//       this.setState({count:this.state.count+1})
//     },1000)
//   }
//   componentWillUnmount(){
//     clearInterval(this.timer)
//   }
//     render() {
//     return (
//       <div>
//         <h2>Count组件</h2>
//         <input type='text' ref={this.myRef}></input>
//         <h2>当前求和为：{this.state.count}</h2><br></br>
//         <button onClick={this.add}>点我+1</button>
//         <button onClick={this.unmount}>点我卸载组件</button>
//         <button onClick={this.showdata}>点我提示输入的数据</button>
        
//       </div>
//     )
//   }
// }
// 函数式组件
function Demo(){
  const [count,setcount]=React.useState(0)
  const myRef=useRef()
// 实现挂载组件,count自增长
  React.useEffect(()=>{
    let timer = setInterval(()=>{
      setcount(count=>count+1)
    },1000)
    return ()=>{
      clearInterval(timer)
    }
  },[])
  function add(){
    // 第一种写法
    // setcount(count+1)
    // 第二种写法
    setcount(count=>count+1)
  }
  // 卸载组件
  function unmount(){
        ReactDOM.unmountComponentAtNode(document.getElementById('root'));
  }
  // 提示输入的数据
  function showdata(){
    alert(myRef.current.value)
  }
  return (
          <div>
            <h2>Count组件</h2>
            <input ref={myRef}></input>
            <h2>当前求和为：{count}</h2><br></br>
            <button onClick={add}>点我+1</button>
            <button onClick={unmount}>点我卸载组件</button>
            <button onClick={showdata}>点我提示输入的数据</button>
          </div>
      )
}
export default Demo
```

## Fragment

### 两种写法

+ `<Fragment><Fragment>`
+ `<></>`

### 作用

> 可以不用必须有一个真实的DOM根标签了
> 组件需要遍历时可以使用`<Fragment key={1}><Fragment>`,它只能用于传递`key`

**示例：**

```js
import React, { Component ,Fragment} from 'react'
import Count from './containers/Count'
export default class App extends Component {
  render() {
    return (
      <Fragment>
        {/* 给容器组件传递store */}
        <Count></Count>
      </Fragment>
    )
  }
}
```

## Context

### 理解

> 一种组件间通信方式, 常用于【祖组件】与【后代组件】间通信

### 使用

```js
1) 创建Context容器对象：
	const XxxContext = React.createContext()  
	
2) 渲染子组时，外面包裹xxxContext.Provider, 通过value属性给后代组件传递数据：
	<xxxContext.Provider value={数据}>
		子组件
    </xxxContext.Provider>
    
3) 后代组件读取数据：

	//第一种方式:仅适用于类组件 
	  static contextType = xxxContext  // 声明接收context
	  this.context // 读取context中的value数据
	  
	//第二种方式: 函数组件与类组件都可以
	  <xxxContext.Consumer>
	    {
	      value => ( // value就是context中的value数据
	        要显示的内容
	      )
	    }
	  </xxxContext.Consumer>
```

### 注意

	在应用开发中一般不用`context`, 一般都用它的封装`react`插件

**示例：**

```js
import React, { Component } from 'react'
//创建Context对象
const MyContext = React.createContext()
const {Provider,Consumer} = MyContext
export default class A extends Component {

 state = {username:'tom',age:18}

 render() {
  const {username,age} = this.state
  return (
   <div className="parent">
    <h3>我是A组件</h3>
    <h4>我的用户名是:{username}</h4>
    <Provider value={{username,age}}>
     <B/>
    </Provider>
   </div>
  )
 }
}

class B extends Component {
 render() {
  return (
   <div className="child">
    <h3>我是B组件</h3>
    <C/>
   </div>
  )
 }
}
// 类式组件接收
/* class C extends Component {
 声明接收context
 static contextType = MyContext
 render() {
  const {username,age} = this.context
  return (
   <div className="grand">
    <h3>我是C组件</h3>
    <h4>我从A组件接收到的用户名:{username},年龄是{age}</h4>
   </div>
  )
 }
} */
// 函数式组件接收
function C(){
 return (
  <div className="grand">
   <h3>我是C组件</h3>
   <h4>我从A组件接收到的用户名:
   <Consumer>
    {
        // value => `${value.username},年龄是${value.age}`
        // 另一种写法
        value => <span>我从A组件接收到的用户名:{value.username},年龄是{value.age}</span>
        }
   </Consumer>
   </h4>
  </div>
 )
}
```