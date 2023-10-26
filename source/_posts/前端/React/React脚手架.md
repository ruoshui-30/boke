---
title: React脚手架
abbrlink: 3126488542
date: 2023-10-26 14:44:18
tags:
---

## 第1章：React应用(基于React脚手架)

### 1.1 使用create-react-app创建react应用

#### 1.1.1 React脚手架

* **脚手架定义**: 用于帮助程序员快速创建基于某一库的模板项目。
  - ✅ 包含所有必要配置 (如语法检查、jsx编译、devServer等)
  - ✅ 预装了所有相关依赖
  - ✅ 可直接展示简单效果
  
* **React脚手架库**: 提供了专门的脚手架工具——`create-react-app`。
* **技术架构**: 主要包括react + webpack + es6 + eslint。
* **项目特点**: 脚手架项目通常为模块化、组件化、工程化。

#### 1.1.2 创建项目并启动

1. **全局安装**: 
```bash
npm i -g create-react-app
```
2. **创建项目**:
```bash
create-react-app hello-react
```
1. **进入项目目录**:
```bash
cd hello-react
```
4. **启动项目**:
```bash
npm start
```

#### 1.1.1 React脚手架项目结构

* **`public`**: 静态资源文件夹
  - `favicon.icon`: 网站图标
  - `index.html`: 主页面
  - `logo*.png`: logo图片
  - `manifest.json`: 应用配置文件
  - `robots.txt`: 爬虫协议文件

* **`src`**: 源代码文件夹
  - `App.*`: App组件及其样式
  - `index.*`: 入口文件及其样式
  - `logo.svg`: logo SVG图像
  - …其他文件

#### 1.1.4 功能界面的组件化编码流程

1. **拆分组件**: 根据UI界面进行拆分
2. **实现静态组件**: 使用组件来实现静态效果
1. **实现动态组件**:
   * 动态显示初始化数据
     - 数据类型
     - 数据名称
     - 数据的存储位置
   * 交互: 通常从绑定事件监听开始

### 1.2 组件的组合使用-TodoList(经验总结)

*   **拆分组件与实现静态组件**:
    
    *   拆分成独立的组件，保持代码模块化。
    *   使用`className`代替传统的`class`。
    *   `style`属性的JSX写法。
*   **动态初始化列表**:
    
    *   数据应放在哪个组件的`state`？
        *   单独使用 → 自身的`state`。
        *   多个组件共用 → 共有的父组件的`state`（称为“状态提升”）。
*   **父子组件间的通信**:
    
    *   父 → 子：使用`props`传递数据。
    *   子 → 父：通过`props`，要求父组件传递一个回调函数给子组件。
*   **`defaultChecked` vs. `checked`**:
    
    *   `defaultChecked`: 非受控组件的初始设置。
    *   `checked`: 受控组件的值。
*   **`defaultValue` vs. `value`**:
    
    *   `defaultValue`: 非受控组件的初始值。
    *   `value`: 受控组件的当前值。
*   **状态管理位置**:
    
    *   状态应由拥有它的组件来管理，操作该状态的方法也应定义在此组件内。

## 🚀 第2章：React Ajax

### 🌟 2.1 理解

📌 **前置说明**:
- 📍 React 主要关注界面。
- 📍 需要ajax与后端交互获取JSON。
- 📍 在React中需引入第三方的ajax库。

📌 **常用ajax库**:
- 🔸 **jQuery**: 较重，非必需时避免使用。
- 🔸 **axios**: 轻量、推荐使用。

### 🌟 2.2 axios 使用

🔗 **文档**:
[axios官方文档](https://github.com/axios/axios)

📌 **相关API**:

🔸 **GET请求**:
```javascript
axios.get('/user?ID=12345')
  .then(response => console.log(response.data))
  .catch(error => console.log(error));

axios.get('/user', { params: { ID: 12345 } })
  .then(response => console.log(response))
  .catch(error => console.log(error));
```

🔸 **POST请求**:
```javascript
axios.post('/user', { firstName: 'Fred', lastName: 'Flintstone' })
  .then(response => console.log(response))
  .catch(error => console.log(error));
```

### 🌟 2.3 GitHub 用户搜索经验总结

#### 📌 设计状态

- 在设计状态时，应考虑全局性，尤其是网络请求。考虑如何处理请求失败或错误的情况。

  ```javascript
  state = {
    users: [],
    loading: false,
    error: null
  }
  ```

#### 📌 ES6 解构赋值

- ES6 提供了非常强大的解构赋值功能。

  ```javascript
  let obj = { a: { b: 1 } };
  const { a } = obj;  // 传统解构
  const { a: { b } } = obj;  // 连续解构
  const { a: { b: value } } = obj;  // 连续解构 + 重命名
  ```

#### 📌 消息订阅与发布

- 先订阅，再发布。它允许组件间的“隔空对话”。

  ```javascript
  // 组件A中
  componentDidMount() {
    this.token = PubSub.subscribe('eventName', (msg, data) => {
      this.setState({ data });
    });
  }

  componentWillUnmount() {
    PubSub.unsubscribe(this.token);
  }

  // 组件B中
  someFunction() {
    PubSub.publish('eventName', data);
  }
  ```

#### 📌 使用 fetch 发送请求

- 使用 fetch 可以使请求逻辑与组件分离，使代码更加清晰。
- fetch: 原生函数，不再使用XmlHttpRequest对象提交ajax请求
- 老版本浏览器可能不支持

  ```javascript
  async fetchData(keyWord) {
    try {
      const response = await fetch(`/api1/search/users2?q=${keyWord}`);
      const data = await response.json();
      this.setState({ users: data.items });
    } catch (error) {
      console.error('请求出错', error);
    }
  }
  ```

#### 📌 组件间通信

- **父 → 子**：使用 props 传递。

  ```javascript
  // 父组件
  <ChildComponent data={this.state.data} />

  // 子组件
  const { data } = this.props;
  ```

- **子 → 父**：通过回调函数。

  ```javascript
  // 父组件
  handleDataFromChild = (data) => {
    this.setState({ data });
  }
  <ChildComponent sendDataToParent={this.handleDataFromChild} />

  // 子组件
  this.props.sendDataToParent(data);
  ```

- **任意组件间通信**：使用 PubSubJS。

  ```bash
  npm i pubsub-js
  ```

  ```javascript
  import PubSub from 'pubsub-js'; //导入

  // ComponentA
  PubSub.publish('event', data);//订阅消息

  // ComponentB 
  PubSub.subscribe('event', (_, data) => { //发布消息
    this.setState({ data });
  });
  ```

[查看 PubSubJS 官方文档](https://github.com/mroderick/PubSubJS)

### 🌟 2.4 React 脚手架配置代理总结

#### 方法一：简易配置

1. **配置步骤**：在`package.json`中加入代理配置。
    ```json
    "proxy": "http://localhost:5000"
    ```

2. **说明**：
    - **优点**：
        - 配置简单。
        - 请求时无需添加前缀。
    - **缺点**：
        - 仅支持单一代理。
    - **工作机制**：
        - 使用此代理配置，如果在端口3000上的资源不存在，那么该请求会被转发到端口5000（前端资源匹配优先）。


#### 方法二：详细配置

1. **配置步骤**：
    - **Step 1**：在 `src` 目录下创建代理配置文件。
        ```
        src/setupProxy.js
        ```
    - **Step 2**：在 `setupProxy.js` 中配置具体的代理规则。
        ```js
        const { createProxyMiddleware } = require('http-proxy-middleware');

        module.exports = function(app) {
            app.use(
                createProxyMiddleware('/api1', {
                    target: 'http://localhost:5000',
                    changeOrigin: true,
                    pathRewrite: {'^/api1': ''}
                }),
                createProxyMiddleware('/api2', {
                    target: 'http://localhost:5001',
                    changeOrigin: true,
                    pathRewrite: {'^/api2': ''}
                })
            );
        }
        ```

2. **说明**：
    - **优点**：
        - 支持多个代理配置。
        - 提供灵活的控制，决定哪些请求应走代理。
    - **缺点**：
        - 配置稍微复杂。
        - 请求时必须加上特定的前缀。


