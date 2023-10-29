---
title: Redux学习
categories:
  - 前端
  - React
  - Redux
abbrlink: 2905051783
date: 2023-10-29 14:12:40
tags:
---

## 📌 Redux

### 🌟 1.1. Redux理解

---

#### 📚 1.1.1. 学习文档

1. **英文文档:** [Redux Official](https://redux.js.org/)
2. **中文文档:** [Redux 中文版](http://www.redux.org.cn/)
3. **GitHub:** [Redux GitHub](https://github.com/reactjs/redux)

---

#### 🧠 1.1.2. Redux是什么?

1. Redux是一个专门用于做状态管理的JavaScript库，不是React的插件。
2. 它可以与React、Angular、Vue等框架一同使用，但主要与React一起使用。
3. 主要作用: 集中式管理React应用中多个组件共享的状态。

---

#### 🤔 1.1.3. 何时需要使用Redux

1. 当某个组件的状态需要被其他组件访问或共享时。
2. 当一个组件需要更改另一个组件的状态时。
3. 原则: 能不使用就尽量不使用。当不使用会带来困难时，再考虑使用。

---

#### 🔄 1.1.4. Redux工作流程

![](../../../img/react/learn/4.png)

---

### 🌟 1.2. Redux的三大核心概念

---

#### 📜 1.2.1. Action

1. 表示操作的对象。
2. 通常包含以下属性:
   - `type`: 唯一标识，是一个字符串。
   - `data`: 任意类型的数据属性。
   
**例:** `{ type: 'ADD_STUDENT', data: {name: 'tom', age: 18} }`

---

#### 🔧 1.2.2. Reducer

1. 用于初始化和处理状态的函数。
2. 是一个纯函数，根据当前的state和传入的action返回新的state。

---

#### 🏪 1.2.3. Store

1. 把state、action、和reducer联系起来的对象。
2. 可以通过以下方式得到它:
    ```javascript
    import { createStore } from 'redux';
    import reducer from './reducers';
    const store = createStore(reducer);
    ```
3. 它的功能:
   - `getState()`: 获取状态。
   - `dispatch(action)`: 分发action，触发reducer，产生新的state。
   - `subscribe(listener)`: 注册监听，当产生新的state时自动调用。

---

### 🌟 1.3. Redux的核心API

---

#### 🏗️ 1.3.1. `createStore()`

用于创建包含指定reducer的store对象。

---

#### 📦 1.3.2. Store对象

1. Redux库的核心对象。
2. 维护着state和reducer。
3. 主要方法:
   - `getState()`
   - `dispatch(action)`
   - `subscribe(listener)`


---

#### 🛠️ 1.3.3. `applyMiddleware()`

用于应用基于Redux的中间件。

---

#### 🤝 1.3.4. `combineReducers()`

用于合并多个reducer函数。

---

## 📌 1. 求和案例_redux精简版 

### 🚀 1.1. 初步设定 
- 🧹 移除`Count`组件的内部状态。

Count组件
```js
import React, { Component } from 'react';
import store from '../../redux/store';

export default class Count extends Component {

    // 在组件挂载时，监听store的状态变化(也可以写在index文件中如下)
    componentDidMount(){
        store.subscribe(()=>{
            this.setState({}); // 当store状态改变时, 使用setState触发组件重新渲染
        });
    }

    // 处理加法操作
    increment=()=>{
        const {value} = this.selectNumber;  // 获取选择的数值
        store.dispatch({type:'increment',data:value*1});  // 发起一个increment的action
    }

    // 处理减法操作
    decrement=()=>{
        const {value} = this.selectNumber;
        store.dispatch({type:'decrement',data:value*1});
    }

    // 如果当前计数为奇数，则处理加法操作
    increamjishu=()=>{
        const {value} = this.selectNumber;
        const count = store.getState();
        if (count % 2 !== 0) {
            store.dispatch({type:'decrement',data:value*1});
        }
    }

    // 延迟2秒后处理加法操作
    increamodd=()=>{
        setTimeout(()=>{
            const {value} = this.selectNumber;
            store.dispatch({type:'increment',data:value*1});
        }, 2000);
    }

    render() {
        return (
            <div>
                <h2>当前求和为：{store.getState()}</h2>
                <br />
                <select ref={c=>this.selectNumber=c}>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                </select>
                <button onClick={this.increment}>+</button>
                <button onClick={this.decrement}>-</button> 
                <button onClick={this.increamjishu}>和为奇数再加</button> 
                <button onClick={this.increamodd}>等一等再加</button>
            </div>
        );
    }
}
```

*`index.js`监听store的状态变化*

```js
//引入react核心库
import React from 'react'
//引入ReactDOM
import ReactDOM from 'react-dom/client';
import { BrowserRouter} from 'react-router-dom/cjs/react-router-dom'
//引入App
import App from './App'
import store from './redux/store';
const root = ReactDOM.createRoot(document.getElementById('root'));

  root.render(
    <React.StrictMode>
      <BrowserRouter>
        <App />
      </BrowserRouter>
    </React.StrictMode>
  );

store.subscribe(()=>{
  root.render(
    <React.StrictMode>
      <BrowserRouter>
        <App />
      </BrowserRouter>
    </React.StrictMode>
  );
})
```

### 🏗 1.2. 结构搭建 
在`src`目录下创建:
```
- redux
    - store.js
    - count_reducer.js
```

### 📘 1.3. `store.js`配置: 
1. 📦 引入redux中的`createStore`函数，创建一个store。
2. 📡 `createStore`在调用时需要传入一个为其服务的reducer。
3. 🌍 记得暴露store对象。

*案例：* `createStore`已弃用采用这种方法引用

```js
/* 
	该文件专门用于暴露一个store对象，整个应用只有一个store对象
*/
//引入createStore，专门用于创建redux中最为核心的store对象
import { legacy_createStore as createStore} from 'redux'
//引入为Count组件服务的reducer
import countReducer from './count_reducer'
//暴露store
export default createStore(countReducer)
```

### 📖 1.4. `count_reducer.js`配置: 
1. 🌐 reducer本质上是一个函数，接收：`preState`, `action`，返回处理后的状态。
2. 🔧 reducer有两大任务：初始化状态、加工状态。
3. 🚀 当reducer被首次调用时，是由store自动触发的。传递的`preState`是`undefined`, 传递的`action`是: `{type:'@@REDUX/INIT_a.2.b.4}`。

*案例：*

```js
/* 
 1.该文件是用于创建一个为Count组件服务的reducer，reducer的本质就是一个函数
 2.reducer函数会接到两个参数，分别为：之前的状态(preState)，动作对象(action)
*/
const initState = 0 //初始化状态
export default function countReducer(preState=initState,action){
    console.log(preState);
    //从action对象中获取：type、data
    const {type,data} = action
    //根据type决定如何加工数据
    switch (type) {
    case 'increment': //如果是加
    return preState + data
    case 'decrement': //若果是减
    return preState - data
    default:
    return preState
 }
}
```

### 📣 1.5. 实时监测 📡
- 在`index.js`中监测store的状态变化，一旦发生改变，重新渲染`<App/>`。

📝 **备注**：redux只负责管理状态。至于状态的改变驱动着页面的展示，这需要我们手动实现。

## 📌 2. 求和案例_redux完整版

*新增文件：*

1.count_action.js 专门用于创建action对象

```js
// 该文件专门为Count组件生成action对象
import { INCREMENT,DECREMENT} from './constant'
export const createIncrementAction = data => ({type:INCREMENT,data})
export const createDecrementAction = data => ({type:DECREMENT,data})
```

*Count组件调用*

```js
import React, { Component } from 'react';
import store from '../../redux/store';
// 从action creators中引入两个函数，这两个函数用于生成对应的action对象
import {createIncrementAction,createDecrementAction} from '../../redux/count_action';

export default class Count extends Component {

    // 当点击+按钮时触发
    increment=()=>{
        const {value} = this.selectNumber; // 从选择器中获取数值
        // 调用store的dispatch方法，分发一个增加类型的action，并传递增加的数值
        store.dispatch(createIncrementAction(value*1)); 
    }

    // 当点击-按钮时触发
    decrement=()=>{
        const {value} = this.selectNumber; // 从选择器中获取数值
        // 调用store的dispatch方法，分发一个减少类型的action，并传递减少的数值
        store.dispatch(createDecrementAction(value*1)); 
    }

    // 当点击'和为奇数再加'按钮时触发
    increamjishu=()=>{
        const {value} = this.selectNumber; 
        const count = store.getState();
        // 判断当前状态数值是否为奇数，如果是奇数则进行加法操作
        if (count % 2 !== 0) {
          store.dispatch(createIncrementAction(value*1));
        }
    }

    // 当点击'等一等再加'按钮时触发的异步操作
    increamodd=()=>{
        setTimeout(()=>{
            const {value} = this.selectNumber;
            // 延迟2秒后，进行加法操作
            store.dispatch(createIncrementAction(value*1));
        },2000) 
    }

    render() {
        return (
            <div>
                <h2>当前求和为：{store.getState()}</h2> {/* 显示当前的状态数值 */}
                {/* 下面是一个选择器，用于选择要增加或减少的数值 */}
                <select ref={c=>this.selectNumber=c}>
                    <option value="1">1</option>
                    <option value="2">2</option>
                    <option value="3">3</option>
                </select>
                {/* 下面是四个按钮，分别对应四种不同的操作 */}
                <button onClick={this.increment}>+</button>
                <button onClick={this.decrement}>-</button> 
                <button onClick={this.increamjishu}>和为奇数再加</button> 
                <button onClick={this.increamodd}>等一等再加</button>
            </div>
        );
    }
}

```

2.constant.js 放置容易写错的type值

```js
// 该模块是用于定义action对象中type类型的常量值，目的只有一个:便于管理的同时防止程序员单词写错
export const INCREMENT = 'increment'
export const DECREMENT = 'decrement'
```

**注意：**

哪里需要哪里引入,注意引入后的格式，如下：

```js
// 该文件专门为Count组件生成action对象
import { INCREMENT,DECREMENT} from './constant'
export const createIncrementAction = data => ({type:INCREMENT,data})
export const createDecrementAction = data => ({type:DECREMENT,data})
```