---
title: JavaScript进阶第四天
tags: pink
categories:
  - 前端
  - pink
  - JS进阶
abbrlink: 694482451
date: 2023-04-11 20:50:44
---
# JavaScript 进阶 - 第4天

## 深浅拷贝

### 浅拷贝

首先浅拷贝和深拷贝只针对引用类型

浅拷贝：拷贝的是地址

常见方法：

1. 拷贝对象：Object.assgin() / 展开运算符 {...obj} 拷贝对象
2. 拷贝数组：Array.prototype.concat() 或者 [...arr]

>如果是简单数据类型拷贝值，引用数据类型拷贝的是地址 (简单理解： 如果是单层对象，没问题，如果有多层就有问题)

#### 思考？

1. 直接赋值和浅拷贝有什么区别？

a.直接赋值的方法,只要是对象，都会相互影响，因为是直接拷贝对象栈里面的地址。

b.浅拷贝如果是一层对象，不互相影响，如果是多层对象，会相互影响。

2. 浅拷贝怎么理解？

a.拷贝对象之后，如果对象中的属性是基本数据类型，修改拷贝之后的对象，不会影响原对象。
b.如果对象中的属性是引用数据类型，修改拷贝之后的对象，会影响原对象。

```js
  <script>
    const obj = {
      uname: 'pink',
      age: 18,
      family: {
        baby: '小pink'
      }
    }
    // 浅拷贝
    // const o = { ...obj }
    // console.log(o)
    // o.age = 20
    // console.log(o)
    // console.log(obj)
    const o = {}
    Object.assign(o, obj)
    o.age = 20
    o.family.baby = '老pink'
    console.log(o)
    console.log(obj)
  </script>
```


### 深拷贝

首先浅拷贝和深拷贝只针对引用类型

深拷贝：拷贝的是对象，不是地址

常见方法：

1. 通过递归实现深拷贝
2. lodash/cloneDeep
3. 通过JSON.stringify()实现


#### 用递归的方式实现一秒钟打印一次当前时间

```js
  <script>
    function getTime() {
      document.querySelector('div').innerHTML = new Date().toLocaleString()
      setTimeout(getTime, 1000)
    }
    getTime()
  </script>
```


#### 递归实现深拷贝

函数递归：

如果一个函数在内部可以调用其本身，那么这个函数就是递归函数

- 简单理解:函数内部自己调用自己, 这个函数就是递归函数
- 递归函数的作用和循环效果类似
- 由于递归很容易发生“栈溢出”错误（stack overflow），所以必须要加退出条件 return

~~~html
<body>
  <script>
    const obj = {
      uname: 'pink',
      age: 18,
      hobby: ['乒乓球', '足球'],
      family: {
        baby: '小pink'
      }
    }
    const o = {}
    // 拷贝函数
    function deepCopy(newObj, oldObj) {
      debugger
      for (let k in oldObj) {
        // 处理数组的问题  一定先写数组 在写 对象 不能颠倒
        if (oldObj[k] instanceof Array) {
          newObj[k] = []
          //  newObj[k] 接收 []  hobby
          //  oldObj[k]   ['乒乓球', '足球']
          deepCopy(newObj[k], oldObj[k])
        } else if (oldObj[k] instanceof Object) {
          newObj[k] = {}
          deepCopy(newObj[k], oldObj[k])
        }
        else {
          //  k  属性名 uname age    oldObj[k]  属性值  18
          // newObj[k]  === o.uname  给新对象添加属性
          newObj[k] = oldObj[k]
        }
      }
    }
    deepCopy(o, obj) // 函数调用  两个参数 o 新对象  obj 旧对象
    console.log(o)
    o.age = 20
    o.hobby[0] = '篮球'
    o.family.baby = '老pink'
    console.log(obj)
    console.log([1, 23] instanceof Object)
    // 复习
    // const obj = {
    //   uname: 'pink',
    //   age: 18,
    //   hobby: ['乒乓球', '足球']
    // }
    // function deepCopy({ }, oldObj) {
    //   // k 属性名  oldObj[k] 属性值
    //   for (let k in oldObj) {
    //     // 处理数组的问题   k 变量
    //     newObj[k] = oldObj[k]
    //     // o.uname = 'pink'
    //     // newObj.k  = 'pink'
    //   }
    // }
  </script>
</body>
~~~

#### 面试题怎么实现深拷贝

1. 深拷贝拷贝出来的对象不会影响新对象,通过递归实现深拷贝
2. 在普通拷贝时可以直接赋值,但是在拷贝时遇到数组,需要递归拷贝,再次调用这个递归函数就可以了
3. 如果遇到对象,也需要递归拷贝,再次调用这个递归函数就可以了

**注意：**先拷贝数组，再拷贝对象，不能颠倒

#### js库lodash里面cloneDeep内部实现了深拷贝

lodash是一个js库，提供了很多js常用的方法，cloneDeep就是其中一个方法，用来实现深拷贝

lodash官网：https://www.lodashjs.com/

~~~html
<body>
  <!-- 先引用 -->
  <script src="./lodash.min.js"></script>
  <script>
    const obj = {
      uname: 'pink',
      age: 18,
      hobby: ['乒乓球', '足球'],
      family: {
        baby: '小pink'
      }
    }
    const o = _.cloneDeep(obj)
    console.log(o)
    o.family.baby = '老pink'
    console.log(obj)
  </script>
</body>
~~~

#### JSON序列化

~~~html
<body>
  <script>
    const obj = {
      uname: 'pink',
      age: 18,
      hobby: ['乒乓球', '足球'],
      family: {
        baby: '小pink'
      }
    }
    // 把对象转换为 JSON 字符串
    // console.log(JSON.stringify(obj))
    const o = JSON.parse(JSON.stringify(obj))
    console.log(o)
    o.family.baby = '123'
    console.log(obj)
  </script>
</body>
~~~

## 异常处理

> 了解 JavaScript 中程序异常处理的方法，提升代码运行的健壮性。

### throw

异常处理是指预估代码执行过程中可能发生的错误，然后最大程度的避免错误的发生导致整个程序无法继续运行

总结：

1. throw 抛出异常信息，程序也会终止执行
2. throw 后面跟的是错误提示信息
3. Error 对象配合 throw 使用，能够设置更详细的错误信息

```html
<script>
  function counter(x, y) {

    if(!x || !y) {
      // throw '参数不能为空!';
      throw new Error('参数不能为空!')  // Error 对象配合 throw 使用，能够设置更详细的错误信息
    }

    return x + y
  }

  counter()
</script>
```

总结：

1. `throw` 抛出异常信息，程序也会终止执行
2. `throw` 后面跟的是错误提示信息
3. `Error` 对象配合 `throw` 使用，能够设置更详细的错误信息

### try ... catch

```html
<body>
  <p>123</p>
    <script>
    function fn() {
      try {
        // 可能发送错误的代码 要写到 try
        const p = document.querySelector('.p')
        p.style.color = 'red'
      } catch (err) {
        // 拦截错误，提示浏览器提供的错误信息，但是不中断程序的执行
        console.log(err.message)
        throw new Error('你看看，选择器错误了吧')
        // 需要加return 中断程序
        // return
      }
      finally {
        // 不管你程序对不对，一定会执行的代码
        alert('弹出对话框')
      }
      console.log(11)
    }
    fn()
  </script>
</body>
```

总结：

1. `try...catch` 用于捕获错误信息
2. 将预估可能发生错误的代码写在 `try` 代码段中
3. 如果 `try` 代码段中出现错误后，会执行 `catch` 代码段，并截获到错误信息
4. `finally` 代码段中的代码不管 `try` 代码段中的代码是否出错，都会执行

### debugger

相当于断点调试

## 处理this

> 了解函数中 this 在不同场景下的默认值，知道动态指定函数 this 值的方法。

`this` 是 JavaScript 最具“魅惑”的知识点，不同的应用场合 `this` 的取值可能会有意想不到的结果，在此我们对以往学习过的关于【 `this` 默认的取值】情况进行归纳和总结。

### 普通函数

**普通函数**的调用方式决定了 `this` 的值，即【谁调用 `this` 的值指向谁】，如下代码所示：

```html
<script>
  // 普通函数
  function sayHi() {
    console.log(this)  // window 
  }
  // 函数表达式
  const sayHello = function () {
    console.log(this)   // window
  }
  // 函数的调用方式决定了 this 的值
  sayHi() // window
  window.sayHi()
	

// 普通对象
  const user = {
    name: '小明',
    walk: function () {
      console.log(this) // user
    }
  }
  // 动态为 user 添加方法
  user.sayHi = sayHi
  uesr.sayHello = sayHello
  // 函数调用方式，决定了 this 的值
  user.sayHi()
  user.sayHello()
</script>
```

#### 普通函数的this指向问题

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <button>点击</button>
  <script>
    // 普通函数：  谁调用我，this就指向谁
    console.log(this)  // window
    function fn() {
      console.log(this)  // window    
    }
    window.fn()
    window.setTimeout(function () {
      console.log(this) // window 
    }, 1000)
    document.querySelector('button').addEventListener('click', function () {
      console.log(this)  // 指向 button
    })
    const obj = {
      sayHi: function () {
        console.log(this)  // 指向 obj
      }
    }
    obj.sayHi()
  </script>
</body>

</html>
```


注： 普通函数没有明确调用者时 `this` 值为 `window`，严格模式下没有调用者时 `this` 的值为 `undefined`。

### 箭头函数

**箭头函数**中的 `this` 与普通函数完全不同，也不受调用方式的影响，事实上箭头函数中并不存在 `this` ！箭头函数中访问的 `this` 不过是箭头函数所在作用域的 `this` 变量。

```html
<script>
    
  console.log(this) // 此处为 window
  // 箭头函数 
  const sayHi = function() {
    console.log(this) // 该箭头函数中的 this 为函数声明环境中 this 一致
  }
  // 普通对象
  const user = {
    name: '小明',
    // 该箭头函数中的 this 为函数声明环境中 this 一致
    walk: () => {
      console.log(this)
    },
    
    sleep: function () {
      let str = 'hello'
      console.log(this)
      let fn = () => {
        console.log(str)
        console.log(this) // 该箭头函数中的 this 与 sleep 中的 this 一致
      }
      // 调用箭头函数
      fn();
    }
  }

  // 动态添加方法
  user.sayHi = sayHi
  
  // 函数调用
  user.sayHi()
  user.sleep()
  user.walk()
</script>
```

在开发中【使用箭头函数前需要考虑函数中 `this` 的值】，**事件回调函数**使用箭头函数时，`this` 为全局的 `window`，因此DOM事件回调函数不推荐使用箭头函数，如下代码所示：

```html
<script>
  // DOM 节点
  const btn = document.querySelector('.btn')
  // 箭头函数 此时 this 指向了 window
  btn.addEventListener('click', () => {
    console.log(this)
  })
  // 普通函数 此时 this 指向了 DOM 对象
  btn.addEventListener('click', function () {
    console.log(this)
  })
</script>
```

同样由于箭头函数 `this` 的原因，**基于原型的面向对象也不推荐采用箭头函数**，如下代码所示：

```html
<script>
  function Person() {
  }
  // 原型对像上添加了箭头函数
  Person.prototype.walk = () => {
    console.log('人都要走路...')
    console.log(this); // window
  }
  const p1 = new Person()
  p1.walk()
</script>
```

### 箭头函数总结

1. 箭头函数内不存在this时，沿用上一级的
2. 不适用
> 构造函数,原型函数,dom事件函数等等

3. 适用
> 普通函数,对象方法函数,闭包函数,需要使用上一层this的地方等等


### 改变this指向

以上归纳了普通函数和箭头函数中关于 `this` 默认值的情形，不仅如此 JavaScript 中还允许指定函数中 `this` 的指向，有 3 个方法可以动态指定普通函数中 `this` 的指向：

#### call

使用 `call` 方法调用函数，同时指定函数中 `this` 的值，使用方法如下代码所示：

```html
<script>
  // 普通函数
  function sayHi() {
    console.log(this);
  }

  let user = {
    name: '小明',
    age: 18
  }

  let student = {
    name: '小红',
    age: 16
  }

  // 调用函数并指定 this 的值
  sayHi.call(user); // this 值为 user
  sayHi.call(student); // this 值为 student

  // 求和函数
  function counter(x, y) {
    return x + y;
  }

  // 调用 counter 函数，并传入参数
  let result = counter.call(null, 5, 10);
  console.log(result);
</script>
```

总结：

1. `call` 方法能够在调用函数的同时指定 `this` 的值
2. 使用 `call` 方法调用函数时，第1个参数为 `this` 指定的值
3. `call` 方法的其余参数会依次自动传入函数做为函数的参数

#### apply

使用 `call` 方法**调用函数**，同时指定函数中 `this` 的值，使用方法如下代码所示：

```html
<script>
  // 普通函数
  function sayHi() {
    console.log(this)
  }

  let user = {
    name: '小明',
    age: 18
  }

  let student = {
    name: '小红',
    age: 16
  }

  // 调用函数并指定 this 的值
  sayHi.apply(user) // this 值为 user
  sayHi.apply(student) // this 值为 student

  // 求和函数
  function counter(x, y) {
    return x + y
  }
  // 调用 counter 函数，并传入参数
  let result = counter.apply(null, [5, 10])
  console.log(result)
</script>
```

总结：

1. `apply` 方法能够在调用函数的同时指定 `this` 的值
2. 使用 `apply` 方法调用函数时，第1个参数为 `this` 指定的值
3. `apply` 方法第2个参数为数组，数组的单元值依次自动传入函数做为函数的参数

#### bind

`bind` 方法并**不会调用函数**，而是创建一个指定了 `this` 值的新函数，使用方法如下代码所示：

```html
<script>
  // 普通函数
  function sayHi() {
    console.log(this)
  }
  let user = {
    name: '小明',
    age: 18
  }
  // 调用 bind 指定 this 的值
  let sayHello = sayHi.bind(user);
  // 调用使用 bind 创建的新函数
  sayHello()
</script>
```

注：`bind` 方法创建新的函数，与原函数的唯一的变化是改变了 `this` 的值。

#### call

`call` 方法可以动态的指定函数中 `this` 的值，`call` 方法的第一个参数就是 `this` 的值，后面的参数是函数执行时的参数。

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <script>
    const obj = {
      uname: 'pink'
    }
    function fn(x, y) {
      console.log(this) // window
      console.log(x + y)
    }
    // 1. 调用函数  
    // 2. 改变 this 指向
    fn.call(obj, 1, 2)
  </script>
</body>

</html>
```

#### apply

`apply` 方法与 `call` 方法的作用一致，只是传参方式不同，`apply` 方法的第一个参数也是 `this` 的值，第二个参数是一个数组，数组中的元素是函数执行时的参数。

语法：

```js
fn.apply(thisArg, [argsArray])
```

>thisArg：必选项，函数执行时的 `this` 的值
>argsArray：可选项，数组，函数执行时的参数,传递的参数必须包含在数组里
>返回值：函数的返回值,因为是调用函数，所以返回值就是函数的返回值
>因此apply主要跟数组有关系,比如使用Math.max求最大值

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <script>
    const obj = {
      age: 18
    }
    function fn(x, y) {
      console.log(this) // {age: 18}
      console.log(x + y)
    }
    // 1. 调用函数
    // 2. 改变this指向 
    //  fn.apply(this指向谁, 数组参数)
    fn.apply(obj, [1, 2])
    // 3. 返回值   本身就是在调用函数，所以返回值就是函数的返回值

    // 使用场景： 求数组最大值
    // const max = Math.max(1, 2, 3)
    // console.log(max)
    const arr = [100, 44, 77]
    const max = Math.max.apply(Math, arr)
    const min = Math.min.apply(null, arr)
    console.log(max, min)
    // 使用场景： 求数组最大值
    console.log(Math.max(...arr))
  </script>
</body>

</html>
```

#### bind(重点)

`bind` 方法与 `call` 方法的作用一致，只是 `bind` 方法不会立即调用函数，而是返回一个新的函数，新函数中的 `this` 值已经被绑定，后面的参数是函数执行时的参数。

语法：

```js
fn.bind(thisArg, agr1,agr2)
```

>bind()方法不会调用函数,但是能改变this指向
>thisArg：必选项，函数执行时的 `this` 的值
>agr1,agr2：可选项，函数执行时的参数,传递的其他参数
>返回由指定的this值和初始化参数改造的 原函数拷贝 (新函数)
>因此如果我们只想改变this的指向,不想调用函数时,就可以使用bind,比如改变定时器中的this指向


```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>

<body>
  <button>发送短信</button>
  <script>
    const obj = {
      age: 18
    }
    function fn() {
      console.log(this)
    }

    // 1. bind 不会调用函数 
    // 2. 能改变this指向
    // 3. 返回值是个函数，  但是这个函数里面的this是更改过的obj
    const fun = fn.bind(obj)
    // console.log(fun) 
    fun()

    // 需求，有一个按钮，点击里面就禁用，2秒钟之后开启
    document.querySelector('button').addEventListener('click', function () {
      // 禁用按钮
      this.disabled = true
      window.setTimeout(function () {
        // 在这个普通函数里面，我们要this由原来的window 改为 btn
        this.disabled = false
      }.bind(this), 2000)   // 这里的this 和 btn 一样
    })
  </script>
</body>

</html>
```
#### call apply bind 总结

1. 相同点

都可以改变函数内部this指向

2. 区别

a. call和apply会调用函数,并改变函数内部的this指向

b. call和apply传递的参数不同,call传递aru1,aru2,apply传递的参数必须是数组形式

c. bind不会调用函数,可以改变函数内部this的指向

3. 应用场景

a. call调用函数并且可以传递参数

b. apply经常和数组有关系,比如借助于数学对象,求数组中的最大值

c. bind不调用函数,但是可以改变函数内部的this指向,比如改变定时器内部的this指向

## 防抖

1. 防抖（debounce）
所谓防抖，就是指触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间(例如：王者荣耀回城,只要被打断就需要重新执行)

>应用场景
a. 搜索框输入,只需用户最后一次输入完,再发送请求。
b. 手机号,邮箱验证输入检测

### 手写防抖函数(实现鼠标经过盒子显示文字)

要求：鼠标停止500ms之后,里面的数字+1

核心思路：
防抖函数的核心是定时器(setTimeout)实现

a. 声明一个定时器变量
b. 当鼠标每次滑动都先判断定时器是否存在,如果存在就清除定时器
c. 如果没有定时器,就创建一个定时器,存到定时器变量中
d. 在定时器中执行函数,并且清除定时器

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
    .box {
      width: 500px;
      height: 500px;
      background-color: #ccc;
      color: #fff;
      text-align: center;
      font-size: 100px;
    }
    </style>
</head>
<body>
    <div class="box">
        
    </div>
    <script>
        const box = document.querySelector(".box");
        let i = 1;
        function movemover(){
            box.innerHTML = i++;
        }
        function debounce(fn,t){
            let timer = null; //定时器
            return function(){
                if(timer){
                    clearTimeout(timer) //清除定时器
                }
                timer = setTimeout(function(){
                    fn();
                },t)
            }
        }
        box.addEventListener("mousemove",debounce(movemover,500));
    </script>
</body>
</html>
```



## 节流（throttle）

所谓节流，就是指连续触发事件但是在 n 秒中只执行一次函数(单位时间内频繁触发,但是只执行一次)

使用场景：
a. 滚动条事件(scroll),加载更多或滚到底部监听
b. 鼠标移动(mousemove)
c. 页面尺寸缩放


### 手写节流函数(实现鼠标经过盒子显示文字)


要求：鼠标移动的时候,不管移动多快,每隔500ms,里面的数字+1

核心思路：
节流函数的核心是定时器(setTimeout)实现

a. 声明一个定时器变量
b. 当鼠标每次滑动都先判断定时器是否存在,如果存在就不开启新定时器
c. 如果没有定时器,就创建一个定时器,存到定时器变量中 把定时器存放到定时器变量中(在定时器里调用要执行的函数,还要记得把定时器清空)


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
    .box {
      width: 500px;
      height: 500px;
      background-color: #ccc;
      color: #fff;
      text-align: center;
      font-size: 100px;
    }
    </style>
</head>
<body>
    <div class="box">
        
    </div>
    <script>
        const box = document.querySelector(".box");
        let i = 1;
        function movemover(){
            box.innerHTML = i++;
        }
        function throttle (fn,t){
            let timer = null; //定时器
            return function(){
                if(!timer){
                  timer = setTimeout(function(){
                    fn();
                    timer = null;
                  },t)
                }
            }
        }
        box.addEventListener("mousemove",throttle(movemover,500));
    </script>
</body>
</html>
```

#### 清除定时器问题


```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <script>
        let timer = null;
        timer = setTimeout(function(){
            clearTimeout(timer);
            console.log(timer);
        },1000)

        // 在定时器执行中是无法删除定时器的,因为定时器还在运作中,在定时器中清除定时器使用的是 timer = null;而不是 clearTimeout(timer);  
    </script>
</body>
</html>
```

### 节流小案例


```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Document</title>
  <style>
    .box {
      width: 500px;
      height: 500px;
      background-color: #ccc;
      color: #fff;
      text-align: center;
      font-size: 100px;
    }
  </style>
</head>

<body>
  <div class="box"></div>
  <script>
    const box = document.querySelector('.box')
    let i = 1  // 让这个变量++
    // 鼠标移动函数
    function mouseMove() {
      box.innerHTML = ++i
      // 如果里面存在大量操作 dom 的情况，可能会卡顿
    }
    // console.log(mouseMove)
    // 节流函数 throttle 
    function throttle(fn, t) {
      // 起始时间
      let startTime = 0
      return function () {
        // 得到当前的时间
        let now = Date.now()
        // 判断如果大于等于 500 采取调用函数
        if (now - startTime >= t) {
          // 调用函数
          fn()
          // 起始的时间 = 现在的时间   写在调用函数的下面 
          startTime = now
        }
      }
    }
    box.addEventListener('mousemove', throttle(mouseMove, 500))

    // throttle(mouseMove, 500) === function () { console.log(1) }


    // box.addEventListener('mousemove', function () {
    //   // 得到当前的时间
    //   let now = Date.now()
    //   // 判断如果大于等于 500 采取调用函数
    //   if (now - startTime >= t) {
    //     // 调用函数
    //     fn()
    //     // 起始的时间 = 现在的时间   写在调用函数的下面
    //     startTime = now
    //   }
    // })

  </script>
</body>

</html>
```



### 防抖小案例(手写)

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Document</title>
  <style>
    .box {
      width: 500px;
      height: 500px;
      background-color: #ccc;
      color: #fff;
      text-align: center;
      font-size: 100px;
    }
  </style>
</head>

<body>
  <div class="box"></div>
  <script>
    const box = document.querySelector('.box')
    let i = 1  // 让这个变量++
    // 鼠标移动函数
    function mouseMove() {
      box.innerHTML = ++i
      // 如果里面存在大量操作 dom 的情况，可能会卡顿
    }
    // 防抖函数
    function debounce(fn, t) {
      let timeId
      return function () {
        // 如果有定时器就清除
        if (timeId) clearTimeout(timeId)
        // 开启定时器 200
        timeId = setTimeout(function () {
          fn()
        }, t)
      }
    }
    // box.addEventListener('mousemove', mouseMove)
    box.addEventListener('mousemove', debounce(mouseMove, 200))

  </script>
</body>

</html>
```

### lodash节流和防抖

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Document</title>
  <style>
    .box {
      width: 500px;
      height: 500px;
      background-color: #ccc;
      color: #fff;
      text-align: center;
      font-size: 100px;
    }
  </style>
</head>

<body>
  <div class="box"></div>
  <script src="./lodash.min.js"></script>
  <script>
    const box = document.querySelector('.box')
    let i = 1  // 让这个变量++
    // 鼠标移动函数
    function mouseMove() {
      box.innerHTML = ++i
      // 如果里面存在大量操作 dom 的情况，可能会卡顿
    }

    // box.addEventListener('mousemove', mouseMove)
    // lodash 节流写法
    // box.addEventListener('mousemove', _.throttle(mouseMove, 500))
    // lodash 防抖的写法
    box.addEventListener('mousemove', _.debounce(mouseMove, 500))

  </script>
</body>

</html>
```

### 节流综合案例

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta http-equiv="X-UA-Compatible" content="IE=edge" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="referrer" content="never" />
  <title>综合案例</title>
  <style>
    * {
      padding: 0;
      margin: 0;
      box-sizing: border-box;
    }

    .container {
      width: 1200px;
      margin: 0 auto;
    }

    .video video {
      width: 100%;
      padding: 20px 0;
    }

    .elevator {
      position: fixed;
      top: 280px;
      right: 20px;
      z-index: 999;
      background: #fff;
      border: 1px solid #e4e4e4;
      width: 60px;
    }

    .elevator a {
      display: block;
      padding: 10px;
      text-decoration: none;
      text-align: center;
      color: #999;
    }

    .elevator a.active {
      color: #1286ff;
    }

    .outline {
      padding-bottom: 300px;
    }
  </style>
</head>

<body>
  <div class="container">
    <div class="header">
      <a href="http://pip.itcast.cn">
        <img src="https://pip.itcast.cn/img/logo_v3.29b9ba72.png" alt="" />
      </a>
    </div>
    <div class="video">
      <video src="https://v.itheima.net/LapADhV6.mp4" controls></video>
    </div>
    <div class="elevator">
      <a href="javascript:;" data-ref="video">视频介绍</a>
      <a href="javascript:;" data-ref="intro">课程简介</a>
      <a href="javascript:;" data-ref="outline">评论列表</a>
    </div>
  </div>
  <script src="https://cdn.jsdelivr.net/npm/lodash@4.17.21/lodash.min.js"></script>
  <script>
    // 1. 获取元素  要对视频进行操作
    const video = document.querySelector('video')
    video.ontimeupdate = _.throttle(() => {
      // console.log(video.currentTime) 获得当前的视频时间
      // 把当前的时间存储到本地存储
      localStorage.setItem('currentTime', video.currentTime)
    }, 1000)

    // 打开页面触发事件，就从本地存储里面取出记录的时间， 赋值给  video.currentTime
    video.onloadeddata = () => {
      // console.log(111)
      video.currentTime = localStorage.getItem('currentTime') || 0
    }

  </script>
</body>

</html>
```


