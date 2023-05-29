---
title: jquery其他方法
tags: jquery其他方法
categories:
  - 前端
  - JS
  - jquery
abbrlink: 3126067608
date: 2023-04-03 16:12:51
---

# 1. jQuery 对象拷贝

如果想要把某个对象拷贝（合并） 给另外一个对象使用，此时可以使用 $.extend() 方法

![](/img/Jquery/img/41.png)

代码:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="jquery.min.js"></script>
    <script>
        $(function() {
            // var targetObj = {};
            // var obj = {
            //     id: 1,
            //     name: "andy"
            // };
            // // $.extend(target, obj);
            // $.extend(targetObj, obj);
            // console.log(targetObj);
            // var targetObj = {
            //     id: 0
            // };
            // var obj = {
            //     id: 1,
            //     name: "andy"
            // };
            // // $.extend(target, obj);
            // $.extend(targetObj, obj);
            // console.log(targetObj); // 会覆盖targetObj 里面原来的数据
            var targetObj = {
                id: 0,
                msg: {
                    sex: '男'
                }
            };
            var obj = {
                id: 1,
                name: "andy",
                msg: {
                    age: 18
                }
            };
            // // $.extend(target, obj);
            // $.extend(targetObj, obj);
            // console.log(targetObj); // 会覆盖targetObj 里面原来的数据

            // // 1. 浅拷贝把原来对象里面的复杂数据类型地址拷贝给目标对象
            // targetObj.msg.age = 20;
            // console.log(targetObj);
            // console.log(obj);

            // 2. 深拷贝把里面的数据完全复制一份给目标对象 如果里面有不冲突的属性,会合并到一起
            $.extend(true, targetObj, obj);
            // console.log(targetObj); // 会覆盖targetObj 里面原来的数据
            targetObj.msg.age = 20;
            console.log(targetObj); // msg :{sex: "男", age: 20}
            console.log(obj);




        })
    </script>
</head>

<body>

</body>

</html>
```

# 2. jQuery 多库共存

![](/img/Jquery/img/42.png)

代码:

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="jquery.min.js"></script>
    <script>
        $(function() {
            function $(ele) {
                return document.querySelector(ele);
            }
            console.log($("div"));
            // 1. 如果$ 符号冲突 我们就使用 jQuery
            jQuery.each();
            // 2. 让jquery 释放对$ 控制权 让用自己决定
            var suibian = jQuery.noConflict();
            console.log(suibian("span"));
            suibian.each();
        })
    </script>
</head>

<body>
    <div></div>
    <span></span>
</body>

</html>
```

# 3.jQuery插件

jQuery 功能比较有限，想要更复杂的特效效果，可以借助于 jQuery 插件完成。

注意: 这些插件也是依赖于jQuery来完成的，所以必须要先引入jQuery文件，因此也称为 jQuery 插件。

**jQuery 插件常用的网站：**

1. jQuery 插件库 http://www.jq22.com/

2. jQuery 之家 http://www.htmleaf.com/

**jQuery 插件使用步骤：**

1. 引入相关文件。（jQuery 文件 和 插件文件）
2. 复制相关html、css、js (调用插件)。

**jQuery 插件演示：**

1. 瀑布流

2. 图片懒加载（图片使用延迟加载在可提高网页下载速度。它也能帮助减轻服务器负载）

当我们页面滑动到可视区域，再显示图片。

我们使用 jquery 插件库 EasyLazyload。 注意，此时的js引入文件和js调用必须写到 DOM元素（图片）最后面

3. 全屏滚动（fullpage.js）

gitHub： https://github.com/alvarotrigo/fullPage.js

中文翻译网站： http://www.dowebok.com/demo/2014/77/

**bootstrap JS 插件：**

bootstrap 框架也是依赖于 jQuery 开发的，因此里面的 js插件使用 ，也必须引入jQuery 文件。

### 案例：toDoList

① 文本框里面输入内容，按下回车，就可以生成待办事项。

② 点击待办事项复选框，就可以把当前数据添加到已完成事项里面。

③ 点击已完成事项复选框，就可以把当前数据添加到待办事项里面。

④ **但是本页面内容刷新页面不会丢失。**

**案例分析:**

① 刷新页面不会丢失数据，因此需要用到本地存储 localStorage

**② 核心思路： 不管按下回车，还是点击复选框，都是把本地存储的数据加载到页面中，这样保证刷新关闭页面不会丢失数据**

③ 存储的数据格式：var todolist = [{ title : ‘xxx’, done: false}]

④ 注意点1： 本地存储 localStorage 里面只能存储字符串格式 ，因此需要把对象转换为字符串 JSON.stringify(data)。

⑤ 注意点2： 获取本地存储数据，需要把里面的字符串转换为对象格式JSON.parse() 我们才能使用里面的数据。

![](/img/Jquery/img/44.png)

![](/img/Jquery/img/43.png)

![](/img/Jquery/img/45.png)

![](/img/Jquery/img/46.png)

![](/img/Jquery/img/47.png)

