---
title: JavaScript进阶第三天
tags: pink
categories:
  - 前端
  - pink
  - JS进阶
abbrlink: 2655645558
date: 2023-04-11 20:50:14
---
# JavaScript 进阶 - 第3天笔记

> 了解构造函数原型对象的语法特征，掌握 JavaScript 中面向对象编程的实现方式，基于面向对象编程思想实现 DOM 操作的封装。

- 了解面向对象编程的一般特征
- 掌握基于构造函数原型对象的逻辑封装
- 掌握基于原型对象实现的继承
- 理解什么原型链及其作用
- 能够处理程序异常提升程序执行的健壮性

## 编程思想

> 学习 JavaScript 中基于原型的面向对象编程序的语法实现，理解面向对象编程的特征。

### 面向过程

面向过程就是分析出解决问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候再一个一个的依次

调用就可以了。

 举个栗子：蛋炒饭

![67679290689](/img/pink/jinjie/assets3/1676792906898.png)

### 面向对象

面向对象是把事务分解成为一个个对象，然后由对象之间分工与合作。

![67679293032](/img/pink/jinjie/assets3/1676792930329.png)

在面向对象程序开发思想中，每一个对象都是功能中心，具有明确分工。

面向对象编程具有灵活、代码可复用、容易维护和开发的优点，更适合多人合作的大型软件项目。

面向对象的特性：

- 封装性


- 继承性
- 多态性

## 构造函数

对比以下通过面向对象的构造函数实现的封装：

```html
<script>
  function Person() {
    this.name = '佚名'
    // 设置名字
    this.setName = function (name) {
      this.name = name
    }
    // 读取名字
    this.getName = () => {
      console.log(this.name)
    }
  }

  // 实例对像，获得了构造函数中封装的所有逻辑
  let p1 = new Person()
  p1.setName('小明')
  console.log(p1.name)

  // 实例对象
  let p2 = new Person()
  console.log(p2.name)
</script>
```

封装是面向对象思想中比较重要的一部分，js面向对象可以通过构造函数实现的封装。

同样的将变量和函数组合到了一起并能通过 this 实现数据的共享，所不同的是借助构造函数创建出来的实例对象之

间是彼此不影响的

>总结：
>
>1. 构造函数体现了面向对象的封装特性
>2. 构造函数实例创建的对象彼此独立、互不影响

封装是面向对象思想中比较重要的一部分，js面向对象可以通过构造函数实现的封装。

前面我们学过的构造函数方法很好用，但是 存在`浪费内存`的问题

## 原型对象

构造函数通过原型分配的函数是所有对象所 共享的。

- JavaScript 规定，每一个构造函数都有一个 prototype 属性，指向另一个对象，所以我们也称为原型对象
- 这个对象可以挂载函数，对象实例化不会多次创建原型上函数，节约内存
- 我们可以把那些不变的方法，直接定义在 prototype 对象上，这样所有对象的实例就可以共享这些方法。
- 构造函数和原型对象中的this 都指向 实例化的对象

```html
<script>
  function Person() {
    
  }

  // 每个函数都有 prototype 属性
  console.log(Person.prototype)
</script>
```



了解了 JavaScript 中构造函数与原型对象的关系后，再来看原型对象具体的作用，如下代码所示：

```html
<script>
  function Person() {
    // 此处未定义任何方法
  }

  // 为构造函数的原型对象添加方法
  Person.prototype.sayHi = function () {
    console.log('Hi~');
  }
	
  // 实例化
  let p1 = new Person();
  p1.sayHi(); // 输出结果为 Hi~
</script>
```



构造函数 `Person` 中未定义任何方法，这时实例对象调用了原型对象中的方法 `sayHi`，接下来改动一下代码：

```html
<script>
  function Person() {
    // 此处定义同名方法 sayHi
    this.sayHi = function () {
      console.log('嗨!');
    }
  }

  // 为构造函数的原型对象添加方法
  Person.prototype.sayHi = function () {
    console.log('Hi~');
  }

  let p1 = new Person();
  p1.sayHi(); // 输出结果为 嗨!
</script>
```

构造函数 `Person` 中定义与原型对象中相同名称的方法，这时实例对象调用则是构造函中的方法 `sayHi`。

通过以上两个简单示例不难发现 JavaScript 中对象的工作机制：**当访问对象的属性或方法时，先在当前实例对象是查找，然后再去原型对象查找，并且原型对象被所有实例共享。**

```html
<script>
	function Person() {
    // 此处定义同名方法 sayHi
    this.sayHi = function () {
      console.log('嗨!' + this.name)
    }
  }

  // 为构造函数的原型对象添加方法
  Person.prototype.sayHi = function () {
    console.log('Hi~' + this.name)
  }
  // 在构造函数的原型对象上添加属性
  Person.prototype.name = '小明'

  let p1 = new Person()
  p1.sayHi(); // 输出结果为 嗨!
  
  let p2 = new Person()
  p2.sayHi()
</script>
```

总结：**结合构造函数原型的特征，实际开发重往往会将封装的功能函数添加到原型对象中。**

### constructor 属性


在哪里？ 每个原型对象里面都有个constructor 属性（constructor 构造函数）

作用：该属性指向该原型对象的构造函数， 简单理解，就是指向我的爸爸，我是有爸爸的孩子

**使用场景：**

如果有多个对象的方法，我们可以给原型对象采取对象形式赋值.

但是这样就会覆盖构造函数原型对象原来的内容，这样修改后的原型对象 constructor 就不再指向当前构造函数了

此时，我们可以在修改后的原型对象中，添加一个 constructor 指向原来的构造函数。

### 对象原型


对象都会有一个属性 __proto__ 指向构造函数的 prototype 原型对象，之所以我们对象可以使用构造函数 prototype 

原型对象的属性和方法，就是因为对象有 __proto__ 原型的存在。

注意：

- __proto__ 是JS非标准属性
- [[prototype]]和__proto__意义相同
- 用来表明当前实例对象指向哪个原型对象prototype
- __proto__对象原型里面也有一个 constructor属性，指向创建该实例对象的构造函数



### 原型继承

继承是面向对象编程的另一个特征，通过继承进一步提升代码封装的程度，JavaScript 中大多是借助原型对象实现继承

的特性。

龙生龙、凤生凤、老鼠的儿子会打洞描述的正是继承的含义。

```html
<body>
  <script>
    // 继续抽取   公共的部分放到原型上
    // const Person1 = {
    //   eyes: 2,
    //   head: 1
    // }
    // const Person2 = {
    //   eyes: 2,
    //   head: 1
    // }
    // 构造函数  new 出来的对象 结构一样，但是对象不一样
    function Person() {
      this.eyes = 2
      this.head = 1
    }
    // console.log(new Person)
    // 女人  构造函数   继承  想要 继承 Person
    function Woman() {

    }
    // Woman 通过原型来继承 Person
    // 父构造函数（父类）   子构造函数（子类）
    // 子类的原型 =  new 父类  
    Woman.prototype = new Person()   // {eyes: 2, head: 1} 
    // 指回原来的构造函数
    Woman.prototype.constructor = Woman

    // 给女人添加一个方法  生孩子
    Woman.prototype.baby = function () {
      console.log('宝贝')
    }
    const red = new Woman()
    console.log(red)
    // console.log(Woman.prototype)
    // 男人 构造函数  继承  想要 继承 Person
    function Man() {

    }
    // 通过 原型继承 Person
    Man.prototype = new Person()
    Man.prototype.constructor = Man
    const pink = new Man()
    console.log(pink)
  </script>
</body>
```

### 原型链(面试高频)

基于原型对象的继承使得不同构造函数的原型对象关联在一起，并且这种关联的关系是一种链状的结构，我们将原型对

象的链状结构关系称为原型链

![67679338869](/img/pink/jinjie/assets3/1676793388695.png)

```html
<body>
  <script>
    // function Objetc() {}
    console.log(Object.prototype)
    console.log(Object.prototype.__proto__)

    function Person() {

    }
    const ldh = new Person()
    // console.log(ldh.__proto__ === Person.prototype) // true
    // console.log(Person.prototype.__proto__ === Object.prototype) // true
    console.log(ldh instanceof Person) // true
    console.log(ldh instanceof Object)  // true
    console.log(ldh instanceof Array) // false
    console.log([1, 2, 3] instanceof Array) // true
    console.log(Array instanceof Object)  // true
  </script>
</body>
```
#### 原型链的查找机制

① 当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。

② 如果没有就查找它的原型（也就是 __proto__指向的 prototype 原型对象）

③ 如果还没有就查找原型对象的原型（Object的原型对象）

④ 依此类推一直找到 Object 为止（null）

⑤ __proto__对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线

⑥ 可以使用 instanceof 运算符用于检测构造函数的 prototype 属性是否出现在某个实例对象的原型链上



#### 案例(模态框效果用构造函数实现)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>面向对象封装消息提示</title>
  <style>
    .modal {
      width: 300px;
      min-height: 100px;
      box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
      border-radius: 4px;
      position: fixed;
      z-index: 999;
      left: 50%;
      top: 50%;
      transform: translate3d(-50%, -50%, 0);
      background-color: #fff;
    }

    .modal .header {
      line-height: 40px;
      padding: 0 10px;
      position: relative;
      font-size: 20px;
    }

    .modal .header i {
      font-style: normal;
      color: #999;
      position: absolute;
      right: 15px;
      top: -2px;
      cursor: pointer;
    }

    .modal .body {
      text-align: center;
      padding: 10px;
    }

    .modal .footer {
      display: flex;
      justify-content: flex-end;
      padding: 10px;
    }

    .modal .footer a {
      padding: 3px 8px;
      background: #ccc;
      text-decoration: none;
      color: #fff;
      border-radius: 2px;
      margin-right: 10px;
      font-size: 14px;
    }

    .modal .footer a.submit {
      background-color: #369;
    }
  </style>
</head>

<body>
  <button id="delete">删除</button>
  <button id="login">登录</button>

  <!-- <div class="modal">
    <div class="header">温馨提示 <i>x</i></div>
    <div class="body">您没有删除权限操作</div>
  </div> -->


  <script>
    // 1.  模态框的构造函数
    function Modal(title = '', message = '') {
      // 公共的属性部分
      this.title = title
      this.message = message
      // 因为盒子是公共的
      // 1. 创建 一定不要忘了加 this 
      this.modalBox = document.createElement('div')
      // 2. 添加类名
      this.modalBox.className = 'modal'
      // 3. 填充内容 更换数据
      this.modalBox.innerHTML = `
        <div class="header">${this.title} <i>x</i></div>
        <div class="body">${this.message}</div>
      `
      // console.log(this.modalBox)
    }
    // 2. 打开方法 挂载 到 模态框的构造函数原型身上
    Modal.prototype.open = function () {
      if (!document.querySelector('.modal')) {
        // 把刚才创建的盒子 modalBox  渲染到 页面中  父元素.appendChild(子元素)
        document.body.appendChild(this.modalBox)
        // 获取 x  调用关闭方法
        this.modalBox.querySelector('i').addEventListener('click', () => {
          // 箭头函数没有this 上一级作用域的this
          // 这个this 指向 m 
          this.close()
        })
      }
    }
    // 3. 关闭方法 挂载 到 模态框的构造函数原型身上
    Modal.prototype.close = function () {
      document.body.removeChild(this.modalBox)
    }

    // 4. 按钮点击
    document.querySelector('#delete').addEventListener('click', () => {
      const m = new Modal('温馨提示', '您没有权限删除')
      // 调用 打开方法
      m.open()
    })

    // 5. 按钮点击
    document.querySelector('#login').addEventListener('click', () => {
      const m = new Modal('友情提示', '您还么有注册账号')
      // 调用 打开方法
      m.open()
    })

  </script>
</body>

</html>
```