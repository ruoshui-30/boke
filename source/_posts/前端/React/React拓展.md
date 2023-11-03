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

## 组件优化

### Component的2个问题 

> 1. 只要执行`setState()`,即使不改变状态数据, 组件也会重新`render()` ==> 效率低
>
> 2. 只要当前组件重新`render()`, 就会自动重新render子组件，纵使子组件没有用到父组件的任何数据,也会重新调用`render()` ==> 效率低

### 效率高的做法

>  只有当组件的`state`或`props`数据发生改变时才重新`render()`

### 原因

>  `Component中`的`shouldComponentUpdate()`总是返回`true`

### 解决

** 办法1: **

>+ 重写`shouldComponentUpdate()`方法
>+ 比较新旧`state`或`props`数据, 如果有变化才返回`true`, 如果没有返回`false`

** 办法2:  **

>+ 使用`PureComponent`
>+ `PureComponent`重写了`shouldComponentUpdate()`, 只有`state`或`props`数据有变化才返回`true`

**  注意: **

+ 只是进行`state`和`props`数据的浅比较, 如果只是数据对象内部数据变了, 返回`false`  
+ 不要直接修改`state`数据, 而是要产生新数据
+ 项目中一般使用`PureComponent`来优化

**示例：**

```js
import React, { PureComponent } from 'react'
export default class Parent extends PureComponent {

	state = {
		carName:"奔驰c36",
		stus:['小张','小李','小王']}

	addStu = ()=>{
		// 方法不可取
		// 不能直接修改state数据, 而是要产生新数据
		/* const {stus} = this.state
		stus.unshift('小刘')
		this.setState({stus}) */

		const {stus} = this.state
		this.setState({stus:['小刘',...stus]})
	}

	changeCar = ()=>{
		this.setState({carName:'迈巴赫'})
		// 方法不可取
		// 不能直接修改state数据, 而是要产生新数据
		// const obj = this.state
		// obj.carName = '迈巴赫'
		// console.log(obj === this.state);
		// this.setState(obj)
	}
	// 重写shouldComponentUpdate
	/* shouldComponentUpdate(nextProps,nextState){
		console.log(this.props,this.state); //目前的props和state
		console.log(nextProps,nextState); //接下要变化的目标props，目标state
		return !this.state.carName === nextState.carName
	} */

	render() {
		console.log('Parent---render');
		const {carName} = this.state
		return (
			<div className="parent">
				<h3>我是Parent组件</h3>
				{this.state.stus}&nbsp;
				<span>我的车名字是：{carName}</span><br/>
				<button onClick={this.changeCar}>点我换车</button>
				<button onClick={this.addStu}>添加一个小刘</button>
				<Child carName="奥拓"/>
			</div>
		)
	}
}

class Child extends PureComponent {
	// 重写shouldComponentUpdate
	/* shouldComponentUpdate(nextProps,nextState){
		console.log(this.props,this.state); //目前的props和state
		console.log(nextProps,nextState); //接下要变化的目标props，目标state
		return !this.props.carName === nextProps.carName
	} */

	render() {
		console.log('Child---render');
		return (
			<div className="child">
				<h3>我是Child组件</h3>
				<span>我接到的车是：{this.props.carName}</span>
			</div>
		)
	}
}
```

## Render Props

在React中，如何向组件内部动态传入带内容的结构（标签）？Vue中可以使用slot技术，也就是通过组件标签体传入结构`<A><B/></A>`，那么在React中可以采用以下两种常见方法：

### Children Props

在React中，可以使用 `children props` 来通过组件标签体传入结构。这种方法允许您将内容作为子元素传递给组件，然后在组件内部访问和显示这些子元素。但如果子组件需要访问父组件的数据，可能需要使用状态提升或其他技术来实现。

```jsx
<A>
  <B>xxxx</B>
</A>
// 在A组件中使用 {this.props.children} 来渲染子元素
```

### Render Props

另一种常见的方法是使用 `render props`。通过这种方式，您可以通过组件标签属性传入结构，并且可以携带数据。通常，这是通过传递一个渲染函数属性来实现的。这种方法更加灵活，可以轻松地传递数据给子组件。

```jsx
<A render={(data) => <C data={data}></C>}></A>
// 在A组件中使用 {this.props.render(内部state数据)} 来渲染子组件C，并传递数据
```

这两种方法在React中用于实现组件复用和组合，根据需要选择适合您场景的方法。这是React中的常见模式，用于动态传递结构和数据到组件内部。

**示例：**

```js
import React, { Component } from 'react';

export default class Parent extends Component {
  render() {
    return (
      <div className="parent">
        <h3>我是Parent组件</h3>
        {/* 通过render属性将name数据传递给B组件 */}
        <A render={(name) => <B name={name} />} />
      </div>
    );
  }
}

class A extends Component {
  state = { name: 'tom' }; // A组件的初始状态数据

  render() {
    console.log(this.props);
    const { name } = this.state;
    return (
      <div className="a">
        <h3>我是A组件</h3>
        {/* 通过render属性调用传入的函数并传递name数据 */}
        {this.props.render(name)} 
      </div>
    );
  }
}

class B extends Component {
  render() {
    console.log('B--render');
    return (
      <div className="b">
        <h3>我是B组件, {this.props.name}</h3> {/* 显示传入的name数据 */}
      </div>
    );
  }
}
```

## 错误边界

### 理解：

错误边界`(Error boundary)`：用来捕获后代组件错误，渲染出备用页面

### 特点：

只能捕获后代组件生命周期产生的错误，不能捕获自己组件产生的错误和其他组件在合成事件、定时器中产生的错误

### 使用方式：

>`getDerivedStateFromError`配合`componentDidCatch`

```js
// 生命周期函数，一旦后台组件报错，就会触发
static getDerivedStateFromError(error) {
    console.log(error);
    // 在render之前触发
    // 返回新的state
    return {
        hasError: true,
    };
}

componentDidCatch(error, info) {
    // 统计页面的错误。发送请求发送到后台去
    console.log(error, info);
}
```

**示例：**

如果子组件出问题,给其父组件添加错误边界

子组件`Child`
```js
import React, { Component } from 'react'

export default class Child extends Component {
 state = {
  users:[
   {id:'001',name:'tom',age:18},
   {id:'002',name:'jack',age:19},
   {id:'003',name:'peiqi',age:20},
  ]
  // users:'abc'
 }

 render() {
  return (
   <div>
    <h2>我是Child组件</h2>
    {
     this.state.users.map((userObj)=>{
      return <h4 key={userObj.id}>{userObj.name}----{userObj.age}</h4>
     })
    }
   </div>
  )
 }
}
```

父组件`Parent`
```js
import React, { Component } from 'react'
import Child from './Child'

export default class Parent extends Component {

 state = {
  hasError:'' //用于标识子组件是否产生错误
 }

 //当Parent的子组件出现报错时候，会触发getDerivedStateFromError调用，并携带错误信息
 static getDerivedStateFromError(error){
  console.log('@@@',error);
  return {hasError:error}
 }

 componentDidCatch(){
  console.log('此处统计错误，反馈给服务器，用于通知编码人员进行bug的解决');
 }

 render() {
  return (
   <div>
    <h2>我是Parent组件</h2>
    {this.state.hasError ? <h2>当前网络不稳定，稍后再试</h2> : <Child/>}
   </div>
  )
 }
}
```

## 组件通信方式总结

### 组件间的关系：

- 父子组件
- 兄弟组件（非嵌套组件）
- 祖孙组件（跨级组件）

### 几种通信方式：

你提到了一些在React中用于组件通信的常见方式，这些方式包括：

1.  **Props**：
    
    *   **Children Props**：通过将子元素作为`props`传递给组件，子组件可以在其中渲染内容。
    *   **Render Props**：通过将一个渲染函数作为`props`传递给组件，使组件能够动态渲染内容。
2.  **消息订阅-发布**：
    
    * 	`pubs-sub`、`event`等等
    *   通过使用第三方库或原生事件系统来实现消息的发布和订阅，以实现组件之间的通信。
3.  **集中式管理**：
    
    *   使用状态管理工具，如**Redux**或**Dva**，以集中管理应用程序的状态，从而实现不同组件之间的通信。
4.  **Context**：
    
    *   使用**Context** API，可以在React中创建一个全局数据存储和访问的机制。通常结合**Provider**和**Consumer**来实现数据的传递，实现了生产者-消费者模式。

这些通信方式在不同场景下都有各自的优势和用途。选择适当的通信方式取决于项目的需求和架构。

### 比较好的搭配方式：

+ 父子组件：`props`
+ 兄弟组件：消息订阅-发布、集中式管理
+ 祖孙组件(跨级组件)：消息订阅-发布、集中式管理、`conText`(开发用的少，封装插件用的多)