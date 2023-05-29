---
title: JS基础
tags: JS基础
categories:
  - 前端
  - JS
  - JS基础
abbrlink: 1583066821
date: 2023-04-11 16:13:08
---
# 第一天
## 1. 编程语言

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        alert('我是编程语言，来控制电脑网页弹出你好');
        alert('我是编程语言，来控制电脑网页弹出你好');
    </script>
</head>

<body>

</body>

</html>
```
## 2.JS初体验

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style></style>
    <!-- 2.内嵌式的js -->
    <script>
        // alert('沙漠骆驼');
    </script>
    <!-- 3. 外部js script 双标签 -->
    <script src="my.js"></script>
</head>

<body>
    <!-- 1. 行内式的js 直接写到元素的内部 -->
    <!-- <input type="button" value="唐伯虎" onclick="alert('秋香姐')"> -->
</body>

</html>
```
## 3. JS注释

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. 单行注释  ctrl + /
        /* 2. 多行注释  默认的快捷键 shift +  alt  + a
           2. 多行注释  vscode 中修改多行注释的快捷键：  ctrl + shift + /
        */
    </script>
</head>

<body>

</body>

</html>
```

## 4. JS输入输出语句

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 这是一个输入框
        prompt('请输入您的年龄');
        // alert 弹出警示框 输出的 展示给用户的
        alert('计算的结果是');
        // console 控制台输出 给程序员测试用的  
        console.log('我是程序员能看到的');
    </script>
</head>

<body>

</body>

</html>
```
## 5. JS变量

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. 声明了一个age 的变量 
        var age;
        // 2. 赋值  把值存入这个变量中
        age = 18;
        // 3. 输出结果 
        console.log(age);
        // 4. 变量的初始化 
        var myname = 'pink老师';
        console.log(myname);
    </script>
</head>

<body>

</body>

</html>
```

## 6. 变量案例
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        var myname = '旗木卡卡西';
        var address = '火影村';
        var age = 30;
        var email = 'kakaxi@itcast.cn';
        var gz = 2000;
        console.log(myname);
        console.log(address);
        console.log(age);
        console.log(email);
        console.log(gz);
    </script>
</head>

<body>

</body>

</html>
```
## 7. 变量案例弹出用户名
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. 用户输入姓名  存储到一个 myname的变量里面
        var myname = prompt('请输入您的名字');
        // 2. 输出这个用户名
        alert(myname);
    </script>
</head>

<body>

</body>

</html>
```
## 8. 变量的语法拓展
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. 更新变量
        var myname = 'pink老师';
        console.log(myname);
        myname = '迪丽热巴';
        console.log(myname);
        // 2. 声明多个变量
        // var age = 18;
        // var address = '火影村';
        // var gz = 2000;
        var age = 18,
            address = '火影村',
            gz = 2000;
        // 3. 声明变量的特殊情况
        // 3.1 只声明不赋值 结果是？  程序也不知道里面存的是啥 所以结果是 undefined  未定义的
        var sex;
        console.log(sex); // undefined
        // 3.2  不声明 不赋值 直接使用某个变量会报错滴
        // console.log(tel);
        // 3.3 不声明直接赋值使用
        qq = 110;
        console.log(qq);
    </script>
</head>

<body>

</body>

</html>
```
## 9. 变量的命名规则
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        var app = 10;
        var App = 100;
        console.log(app);
        console.log(App);
        // var 18age;
        // var var; 因为var 有特殊意义了，这个叫做关键字 不能作为变量名的   for  while if
        // name 我们尽量不要直接使用name 作为变量名
        // console.log(tel);
        console.log(name);
    </script>
</head>

<body>

</body>

</html>
```
## 10. 交换两个变量
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // js 是编程语言有很强的逻辑性在里面： 实现这个要求的思路 先怎么做后怎么做 
        // 1. 我们需要一个临时变量帮我们
        // 2. 把apple1 给我们的临时变量 temp 
        // 3. 把apple2 里面的苹果给 apple1 
        // 4. 把临时变量里面的值 给 apple2 
        var temp; // 声明了一个临时变量为空
        var apple1 = '青苹果';
        var apple2 = '红苹果';
        temp = apple1; // 把右边给左边
        apple1 = apple2;
        apple2 = temp;
        console.log(apple1);
        console.log(apple2);
    </script>
</head>

<body>

</body>

</html>
```
## 11. 变量的数据类型
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // int num = 10;  java 
        // var num; // 这里的num 我们是不确定属于哪种数据类型的
        var num = 10; // num 属于数字型 
        // js 的变量数据类型是只有程序在运行过程中，根据等号右边的值来确定的
        var str = 'pink'; // str 字符串型
        // js是动态语言 变量的数据类型是可以变化的
        var x = 10; // x 是数字型 
        x = 'pink'; // x 字符串型
    </script>
</head>

<body>

</body>

</html>
```
## 12. 数字型Number
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        var num = 10; // num 数字型 
        var PI = 3.14 // PI 数字型
            // 1. 八进制  0 ~ 7  我们程序里面数字前面加0 表示八进制
        var num1 = 010;
        console.log(num1); //  010  八进制 转换为 10进制 就是  8 
        var num2 = 012;
        console.log(num2);
        // 2. 十六进制  0 ~ 9  a ~ f    #ffffff  数字的前面加 0x 表示十六进制
        var num3 = 0x9;
        console.log(num3);
        var num4 = 0xa;
        console.log(num4);
        // 3. 数字型的最大值
        console.log(Number.MAX_VALUE);
        // 4. 数字型的最小值
        console.log(Number.MIN_VALUE);
        // 5. 无穷大
        console.log(Number.MAX_VALUE * 2); // Infinity 无穷大  
        // 6. 无穷小
        console.log(-Number.MAX_VALUE * 2); // -Infinity 无穷大
        // 7. 非数字
        console.log('pink老师' - 100); // NaN
    </script>
</head>

<body>

</body>

</html>
```
## 13. isNaN() 判断是否是非数字
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // isNaN() 这个方法用来判断非数字   并且返回一个值 如果是数字返回的是 false 如果不是数字返回的是true
        console.log(isNaN(12)); // false
        console.log(isNaN('pink老师')); // true
    </script>
</head>

<body>

</body>

</html>
```
## 14. 字符串String
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 'pink'   'pink老师'  '12'   'true'
        var str = '我是一个"高富帅"的程序员';
        console.log(str);
        // 字符串转义字符  都是用 \ 开头 但是这些转义字符写道引号里面
        var str1 = "我是一个'高富帅'的\n程序员";
        console.log(str1);
    </script>
</head>

<body>

</body>

</html>
```
## 15. 弹出警示框
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        alert('酷热难耐，火辣的太阳底下，我挺拔的身姿，成为了最为独特的风景。\n我审视四周，这里，是我的舞台，我就是天地间的王者。\n这一刻，我豪气冲天，终于大喊一声："收破烂啦～"');
    </script>
</head>

<body>

</body>

</html>
```
## 16. 字符串拼接
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. 检测获取字符串的长度 length 
        var str = 'my name is andy';
        console.log(str.length); // 15
        // 2. 字符串的拼接 +  只要有字符串和其他类型相拼接 最终的结果是字符串类型
        console.log('沙漠' + '骆驼'); // 字符串的 沙漠骆驼
        console.log('pink老师' + 18); // 'pink老师18'
        console.log('pink' + true); // pinktrue
        console.log(12 + 12); // 24
        console.log('12' + 12); // '1212'
    </script>
</head>

<body>

</body>

</html>
```
## 17. 字符串拼接加强
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        console.log('pink老师' + 18); // pink老师18
        console.log('pink老师' + 18 + '岁');
        var age = 19;
        console.log('pink老师age岁');
        // 我们变量不要写到字符串里面，是通过和 字符串相连的方式实现的
        console.log('pink老师' + age + '岁');
        // 变量和字符串相连的口诀：  引引加加
        console.log('pink老师' + age + '岁');
    </script>
</head>

<body>

</body>

</html>
```
## 18. 显示年龄案例
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 弹出一个输入框（prompt)，让用户输入年龄（用户输入）
        // 把用户输入的值用变量保存起来,把刚才输入的年龄与所要输出的字符串拼接 （程序内部处理）
        // 使用alert语句弹出警示框（输出结果）
        var age = prompt('请输入您的年龄');
        var str = '您今年已经' + age + '岁了';
        alert(str);
    </script>
</head>

<body>

</body>

</html>
```
## 19. 布尔值Boolean
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        var flag = true; // flag 布尔型 
        var flag1 = false; // flag1 布尔型
        console.log(flag + 1); // true 参与加法运算当1来看
        console.log(flag1 + 1); // false 参与加法运算当 0来看
        // 如果一个变量声明未赋值 就是 undefined 未定义数据类型
        var str;
        console.log(str);
        var variable = undefined;
        console.log(variable + 'pink'); // undefinedpink
        console.log(variable + 1); // NaN  undefined 和数字相加 最后的结果是 NaN
        // null 空值
        var space = null;
        console.log(space + 'pink'); // nullpink
        console.log(space + 1); // 1
    </script>
</head>

<body>

</body>

</html>
```
## 20. 获取变量的数据类型
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        var num = 10;
        console.log(typeof num); // number
        var str = 'pink';
        console.log(typeof str); // string
        var flag = true;
        console.log(typeof flag); // boolean
        var vari = undefined;
        console.log(typeof vari); // undefined
        var timer = null;
        console.log(typeof timer); // object
        // prompt 取过来的值是 字符型的
        var age = prompt('请输入您的年龄');
        console.log(age);
        console.log(typeof age);
    </script>
</head>

<body>

</body>

</html>
```
## 21. 字面量
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        console.log(18);
        console.log('18');
        console.log(true);
        console.log(undefined);
        console.log(null);
    </script>
</head>

<body>

</body>

</html>
```

## 22. 转换为字符串型
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. 把数字型转换为字符串型 变量.toString()
        var num = 10;
        var str = num.toString();
        console.log(str);
        console.log(typeof str);
        // 2. 我们利用 String(变量)   
        console.log(String(num));
        // 3. 利用 + 拼接字符串的方法实现转换效果 隐式转换
        console.log(num + '');
    </script>
</head>

<body>

</body>

</html>
```

## 23. 转换为数字型
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // var age = prompt('请输入您的年龄');
        // 1. parseInt(变量)  可以把 字符型的转换为数字型 得到是整数
        // console.log(parseInt(age));
        console.log(parseInt('3.14')); // 3 取整
        console.log(parseInt('3.94')); // 3 取整
        console.log(parseInt('120px')); // 120 会去到这个px单位
        console.log(parseInt('rem120px')); // NaN
        // 2. parseFloat(变量) 可以把 字符型的转换为数字型 得到是小数 浮点数
        console.log(parseFloat('3.14')); // 3.14
        console.log(parseFloat('120px')); // 120 会去掉这个px单位
        console.log(parseFloat('rem120px')); // NaN
        // 3. 利用 Number(变量) 
        var str = '123';
        console.log(Number(str));
        console.log(Number('12'));
        // 4. 利用了算数运算 -  *  /  隐式转换
        console.log('12' - 0); // 12
        console.log('123' - '120');
        console.log('123' * 1);
    </script>
</head>

<body>

</body>

</html>
```

## 24. 计算年龄案例
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 弹出一个输入框（prompt)，让用户输入出生年份 （用户输入）
        // 把用户输入的值用变量保存起来，然后用今年的年份减去变量值，结果就是现在的年龄  （程序内部处理）
        // 弹出警示框（alert) ， 把计算的结果输出 （输出结果）
        var year = prompt('请您输入您的出生年份');
        var age = 2018 - year; // year 取过来的是字符串型  但是这里用的减法 有隐式转换
        alert('您今年已经' + age + '岁了');
    </script>
</head>

<body>

</body>

</html>
```

## 25. 简单加法案例
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 先弹出第一个输入框，提示用户输入第一个值  保存起来
        // 再弹出第二个框，提示用户输入第二个值  保存起来
        // 把这两个值相加，并将结果赋给新的变量（注意数据类型转换）  
        // 弹出警示框（alert) ， 把计算的结果输出 （输出结果）
        var num1 = prompt('请您输入第一个值：');
        var num2 = prompt('请您输入第二个值：');
        var result = parseFloat(num1) + parseFloat(num2);
        alert('您的结果是:' + result);
    </script>
</head>

<body>

</body>

</html>
```

## 26. 转换为布尔型
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        console.log(Boolean('')); // false
        console.log(Boolean(0)); // false
        console.log(Boolean(NaN)); // false
        console.log(Boolean(null)); // false
        console.log(Boolean(undefined)); // false
        console.log('------------------------------');
        console.log(Boolean('123'));
        console.log(Boolean('你好吗'));
        console.log(Boolean('我很好'));
    </script>
</head>

<body>

</body>

</html>
```

# 第二天
## 1. 算术运算符
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        console.log(1 + 1); // 2
        console.log(1 - 1); // 0
        console.log(1 * 1); // 1
        console.log(1 / 1); // 1
        // 1. % 取余 （取模）  
        console.log(4 % 2); // 0
        console.log(5 % 3); // 2
        console.log(3 % 5); // 3
        // 2. 浮点数 算数运算里面会有问题
        console.log(0.1 + 0.2); // 0.30000000000000004
        console.log(0.07 * 100); // 7.000000000000001
        // 3. 我们不能直接拿着浮点数来进行相比较 是否相等
        var num = 0.1 + 0.2;
        console.log(num == 0.3); // false
    </script>
</head>

<body>

</body>

</html>
```

## 2. 表达式与返回值
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        //  是由数字、运算符、变量等组成的式子 我们成为表达式   1 + 1 
        console.log(1 + 1); // 2 就是返回值
        // 1 + 1 = 2
        // 在我们程序里面  2 = 1 + 1   把我们的右边表达式计算完毕把返回值给左边
        var num = 1 + 1;
    </script>
</head>

<body>

</body>

</html>
```

## 3. 前置自增自减
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. 想要一个变量自己加1   num = num + 1 比较麻烦
        var num = 1;
        num = num + 1; // ++num
        num = num + 1;
        console.log(num); // 3
        // 2. 前置递增运算符  ++ 写在变量的前面
        var age = 10;
        ++age; // 类似于 age = age + 1
        console.log(age);
        // 3. 先加1  后返回值
        var p = 10;
        console.log(++p + 10);
    </script>
</head>

<body>

</body>

</html>
```

## 4. 后置自增自减
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        var num = 10;
        num++; // num = num + 1    ++num;
        console.log(num);
        // 1. 前置自增和后置自增如果单独使用 效果是一样的
        // 2. 后置自增 口诀：先返回原值 后自加1 
        var age = 10;
        console.log(age++ + 10);
        console.log(age);
    </script>
</head>

<body>

</body>

</html>
```

## 5. 递增运算符
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        var a = 10;
        ++a; // ++a  11    a = 11
        var b = ++a + 2; // a = 12   ++a = 12
        console.log(b); // 14

        var c = 10;
        c++; // c++ 11  c = 11
        var d = c++ + 2; //  c++  = 11     c = 12
        console.log(d); // 13

        var e = 10;
        var f = e++ + ++e; // 1. e++ =  10  e = 11  2. e = 12  ++e = 12
        console.log(f); // 22
        // 后置自增  先表达式返回原值 后面变量再自加1
    </script>
</head>

<body>

</body>

</html>
```

## 6. 比较运算符
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        console.log(3 >= 5); // false
        console.log(2 <= 4); // true
        //1. 我们程序里面的等于符号 是 ==  默认转换数据类型 会把字符串型的数据转换为数字型 只要求值相等就可以
        console.log(3 == 5); // false
        console.log('pink老师' == '刘德华'); // flase
        console.log(18 == 18); // true
        console.log(18 == '18'); // true
        console.log(18 != 18); // false
        // 2. 我们程序里面有全等 一模一样  要求 两侧的值 还有 数据类型完全一致才可以 true
        console.log(18 === 18);
        console.log(18 === '18'); // false
    </script>
</head>

<body>

</body>

</html>
```

## 7. 逻辑运算符
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. 逻辑与 &&  and 两侧都为true  结果才是 true  只要有一侧为false  结果就为false 
        console.log(3 > 5 && 3 > 2); // false
        console.log(3 < 5 && 3 > 2); // true
        // 2. 逻辑或 || or  两侧都为false  结果才是假 false  只要有一侧为true  结果就是true
        console.log(3 > 5 || 3 > 2); // true 
        console.log(3 > 5 || 3 < 2); // false
        // 3. 逻辑非  not  ！ 
        console.log(!true); // false
    </script>
</head>

<body>

</body>

</html>
```

## 8. 逻辑运算符的练习
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        var num = 7;
        var str = "我爱你~中国~";

        console.log(num > 5 && str.length >= num); // true

        console.log(num < 5 && str.length >= num); // false

        console.log(!(num < 10)); // false

        console.log(!(num < 10 || str.length == num)); // false
    </script>
</head>

<body>

</body>

</html>
```

## 9. 短路运算符（逻辑中断）
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. 用我们的布尔值参与的逻辑运算  true && false  == false 
        // 2. 123 && 456  是值 或者是 表达式 参与逻辑运算？ 
        // 3. 逻辑与短路运算  如果表达式1 结果为真 则返回表达式2  如果表达式1为假 那么返回表达式1
        console.log(123 && 456); // 456
        console.log(0 && 456); //  0
        console.log(0 && 1 + 2 && 456 * 56789); // 0
        console.log('' && 1 + 2 && 456 * 56789); // ''
        // 如果有空的或者否定的为假 其余是真的  0  ''  null undefined  NaN
        // 4. 逻辑或短路运算  如果表达式1 结果为真 则返回的是表达式1 如果表达式1 结果为假 则返回表达式2
        console.log(123 || 456); // 123
        console.log(123 || 456 || 456 + 123); // 123
        console.log(0 || 456 || 456 + 123); // 456
        // 逻辑中断很重要 它会影响我们程序运行结果思密达
        var num = 0;
        console.log(123 || num++);
        console.log(num); // 0
    </script>
</head>

<body>

</body>

</html>
```

## 10. 赋值运算符
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        var num = 10;
        // num = num + 1;   num++
        // num = num + 2; // num += 2;
        // num += 2;
        num += 5;
        console.log(num);
        var age = 2;
        age *= 3;
        console.log(age);
    </script>
</head>

<body>

</body>

</html>
```

## 11. 运算符优先级
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        //  ++num   !num     2 + 3
        console.log(4 >= 6 || '人' != '阿凡达' && !(12 * 2 == 144) && true)
        var num = 10;
        console.log(5 == num / 2 && (2 + 2 * num).toString() === '22');
        console.log('-------------------');
        var a = 3 > 5 && 2 < 7 && 3 == 4;
        console.log(a);

        var b = 3 <= 4 || 3 > 1 || 3 != 2;
        console.log(b);

        var c = 2 === "2";
        console.log(c);

        var d = !c || b && a;
        console.log(d);
    </script>
</head>

<body>

</body>

</html>
```

## 12. if语句
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. if 的语法结构   如果if
        // if (条件表达式) {
        //     // 执行语句
        // }

        // 2. 执行思路  如果 if 里面的条件表达式结果为真 true 则执行大括号里面的 执行语句 
        // 如果if 条件表达式结果为假 则不执行大括号里面的语句 则执行if 语句后面的代码
        // 3. 代码体验
        if (3 < 5) {
            alert('沙漠骆驼');
        }
    </script>
</head>

<body>

</body>

</html>
```

## 13. 进入网吧案例
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        //         弹出 prompt 输入框，用户输入年龄， 程序把这个值取过来保存到变量中
        // 使用 if 语句来判断年龄，如果年龄大于18 就执行 if 大括号里面的输出语句
        var age = prompt('请输入您的年龄:');
        if (age >= 18) {
            alert('我想带你去网吧偷耳机');
        }
    </script>
</head>

<body>

</body>

</html>
```

## 14. if else语句
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. 语法结构  if 如果  else 否则
        // if (条件表达式) {
        //     // 执行语句1
        // } else {
        //     // 执行语句2 
        // }
        // 2. 执行思路 如果表达式结果为真 那么执行语句1  否则  执行语句2
        // 3. 代码验证
        var age = prompt('请输入您的年龄:');
        if (age >= 18) {
            alert('我想带你去网吧偷耳机');
        } else {
            alert('滚， 回家做作业去');
        }
        // 5. if里面的语句1 和 else 里面的语句2 最终只能有一个语句执行  2选1
        // 6.  else 后面直接跟大括号
    </script>
</head>

<body>

</body>

</html>
```

## 15. 判断闰年案例
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        //         算法：能被4整除且不能整除100的为闰年（如2004年就是闰年，1901年不是闰年）或者能够被 400 整除的就是闰年
        // 弹出prompt 输入框，让用户输入年份，把这个值取过来保存到变量中
        // 使用 if 语句来判断是否是闰年，如果是闰年，就执行 if 大括号里面的输出语句，否则就执行 else里面的输出语句
        // 一定要注意里面的且 &&  还有或者 || 的写法，同时注意判断整除的方法是取余为 0
        var year = prompt('请您输入年份：');
        if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0) {
            alert('您输入的年份是闰年');
        } else {
            alert('您输入的年份是平年');
        }
    </script>
</head>

<body>

</body>

</html>
```

## 16. if else if else语句
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. 多分支语句   就是利用多个条件来选择不同的语句执行 得到不同的结果  多选1 的过程
        // 2. if else if语句是多分支语句
        // 3. 语法规范
        if (条件表达式1) {
            // 语句1;
        } else if (条件表达式2) {
            // 语句2;
        } else if (条件表达式3) {
            // 语句3;
        } else {
            // 最后的语句;
        }
        // 4. 执行思路
        // 如果条件表达式1 满足就执行 语句1 执行完毕后，退出整个if 分支语句  
        // 如果条件表达式1 不满足，则判断条件表达式2  满足的话，执行语句2 以此类推
        // 如果上面的所有条件表达式都不成立，则执行else 里面的语句
        // 5. 注意点
        // (1) 多分支语句还是多选1 最后只能有一个语句执行
        // (2) else if 里面的条件理论上是可以任意多个的
        // (3) else if 中间有个空格了
    </script>
</head>

<body>

</body>

</html>
```

## 17. 判断成绩案例
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        //  伪代码       按照从大到小判断的思路
        // 弹出prompt输入框，让用户输入分数（score），把这个值取过来保存到变量中
        // 使用多分支 if else if 语句来分别判断输出不同的值
        var score = prompt('请您输入分数:');
        if (score >= 90) {
            alert('宝贝，你是我的骄傲');
        } else if (score >= 80) {
            alert('宝贝，你已经很出色了');
        } else if (score >= 70) {
            alert('你要继续加油喽');
        } else if (score >= 60) {
            alert('孩子，你很危险');
        } else {
            alert('熊孩子，我不想和你说话，我只想用鞭子和你说话');
        }
    </script>
</head>

<body>

</body>

</html>
```

## 18. 三元表达式
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. 有三元运算符组成的式子我们称为三元表达式
        // 2. ++num     3 + 5     ? :
        // 3. 语法结构 
        // 条件表达式 ？ 表达式1 ： 表达式2
        // 4. 执行思路
        // 如果条件表达式结果为真 则 返回 表达式1 的值 如果条件表达式结果为假 则返回 表达式2 的值
        // 5. 代码体验
        var num = 10;
        var result = num > 5 ? '是的' : '不是的'; // 我们知道表达式是有返回值的
        console.log(result);
        // if (num > 5) {
        //     result = '是的';
        // } else {
        //     result = '不是的';
        // }
    </script>
</head>

<body>

</body>

</html>
```

## 19. 数字补零案例
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        //         用户输入0~59之间的一个数字
        // 如果数字小于10，则在这个数字前面补0,（加0 拼接） 否则  不做操作
        // 用一个变量接受这个返回值，输出
        var time = prompt('请您输入一个 0 ~ 59 之间的一个数字');
        // 三元表达式   表达式 ？ 表达式1 ：表达式2 
        var result = time < 10 ? '0' + time : time; //   把返回值赋值给一个变量
        alert(result);
    </script>
</head>

<body>

</body>

</html>
```

## 20. switch语句
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. switch 语句也是多分支语句 也可以实现多选1
        // 2. 语法结构 switch 转换、开关  case 小例子或者选项的意思
        // switch (表达式) {
        //     case value1:
        //         执行语句1;
        //         break;
        //     case value2:
        //         执行语句2;
        //         break;
        //         ...
        //         default:
        //             执行最后的语句;
        // }
        // 3. 执行思路  利用我们的表达式的值 和 case 后面的选项值相匹配 如果匹配上，就执行该case 里面的语句  如果都没有匹配上，那么执行 default里面的语句
        // 4. 代码验证
        switch (8) {
            case 1:
                console.log('这是1');
                break;
            case 2:
                console.log('这是2');
                break;
            case 3:
                console.log('这是3');
                break;
            default:
                console.log('没有匹配结果');

        }
    </script>
</head>

<body>

</body>

</html>
```

## 21. switch注意事项
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // switch注意事项
        var num = 1;
        switch (num) {
            case 1:
                console.log(1);

            case 2:
                console.log(2);

            case 3:
                console.log(3);
                break;


        }
        // 1. 我们开发里面 表达式我们经常写成变量
        // 2. 我们num 的值 和 case 里面的值相匹配的时候是 全等   必须是值和数据类型一致才可以 num === 1
        // 3. break 如果当前的case里面没有break 则不会退出switch 是继续执行下一个case
    </script>
</head>

<body>

</body>

</html>
```

## 22. 查询水果案例
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        //         弹出 prompt 输入框，让用户输入水果名称，把这个值取过来保存到变量中。
        // 将这个变量作为 switch 括号里面的表达式。
        // case 后面的值写几个不同的水果名称，注意一定要加引号 ，因为必须是全等匹配。
        // 弹出不同价格即可。同样注意每个 case 之后加上 break ，以便退出 switch 语句。
        // 将 default 设置为没有此水果。
        var fruit = prompt('请您输入查询的水果:');
        switch (fruit) {
            case '苹果':
                alert('苹果的价格是 3.5/斤');
                break;
            case '榴莲':
                alert('榴莲的价格是 35/斤');
                break;
            default:
                alert('没有此水果');
        }
    </script>
</head>

<body>

</body>

</html>
```

# 第三天
## 1. 循环的目的
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 循环的目的：可以重复执行某些代码
        console.log('媳妇我错了');
        console.log('媳妇我错了');
        console.log('媳妇我错了');
        console.log('---------------------');
        for (var i = 1; i <= 1000; i++) {
            console.log('媳妇我错了');

        }
    </script>
</head>

<body>

</body>

</html>
```

## 2. for循环
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. for 重复执行某些代码， 通常跟计数有关系
        // 2. for 语法结构
        // for (初始化变量; 条件表达式; 操作表达式) {
        //     // 循环体
        // }
        // 3. 初始化变量 就是用var 声明的一个普通变量， 通常用于作为计数器使用 
        // 4. 条件表达式 就是用来决定每一次循环是否继续执行 就是终止的条件
        // 5. 操作表达式 是每次循环最后执行的代码 经常用于我们计数器变量进行更新（递增或者递减）
        // 6. 代码体验 我们重复打印100局 你好
        for (var i = 1; i <= 100; i++) {
            console.log('你好吗');
        }
    </script>
</head>

<body>

</body>

</html>
```

## 3. for循环执行过程
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // for 循环的执行过程
        for (var i = 1; i <= 100; i++) {
            console.log('你好吗');
        }
        // 1. 首先执行里面的计数器变量  var i = 1 .但是这句话在for 里面只执行一次  index
        // 2. 去 i <= 100 来判断是否满足条件， 如果满足条件  就去执行 循环体  不满足条件退出循环 
        // 3. 最后去执行 i++   i++是单独写的代码 递增  第一轮结束 
        // 4. 接着去执行 i <= 100 如果满足条件  就去执行 循环体  不满足条件退出循环   第二轮
    </script>
</head>

<body>

</body>

</html>
```

## 4. for循环执行相同代码
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // for 循环可以执行相同的代码
        for (var i = 1; i <= 10; i++) {
            console.log('媳妇我错了');

        }
        // 我们可以让用户控制输出的次数
        var num = prompt('请您输入次数');
        for (var i = 1; i <= num; i++) {
            console.log('媳妇我错了');

        }
    </script>
</head>

<body>

</body>

</html>
```

## 5. for循环执行不同代码

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // for 循环可以重复执行不同的代码  因为我们有计数器变量 i 的存在 i每次循环值都会变化
        // 我们想要输出1个人 1~100岁
        // for (var i = 1; i <= 100; i++) {
        //     console.log('这个人今年' + i + '岁了');

        // }
        for (var i = 1; i <= 100; i++) {
            if (i == 1) {
                console.log('这个人今年1岁了，他出生了');
            } else if (i == 100) {
                console.log('这个人今年100岁了，他死了');
            } else {
                console.log('这个人今年' + i + '岁了');

            }
        }
    </script>
</head>

<body>

</body>

</html>
```

## 6. for循环执行某些操作
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // for 循环重复执行某些操作 比如说我们做了100次加法运算
        // 求 1~100 之间的整数累加和
        //         需要循环100次，我们需要一个计数器  i  
        // 我们需要一个存储结果的变量 sum ，但是初始值一定是 0
        // 核心算法：1 + 2 + 3 + 4 ....   ，sum  =  sum + i;
        var sum = 0; // 求和 的变量
        for (var i = 1; i <= 100; i++) {
            // sum = sum + i;
            sum += i;
        }
        console.log(sum);
    </script>
</head>

<body>

</body>

</html>
```

## 7. for循环案例
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. 求1-100之间所有数的平均值   需要一个 sum 和的变量 还需要一个平均值 average 变量
        var sum = 0;
        var average = 0;
        for (var i = 1; i <= 100; i++) {
            sum = sum + i;
        }
        average = sum / 100;
        console.log(average);

        // 2. 求1-100之间所有偶数和奇数的和   我们需要一个偶数的和变量 even  还需要一个奇数 odd
        var even = 0;
        var odd = 0;
        for (var i = 1; i <= 100; i++) {
            if (i % 2 == 0) {
                even = even + i;
            } else {
                odd = odd + i;
            }
        }
        console.log('1~100 之间所有的偶数和是' + even);
        console.log('1~100 之间所有的奇数和是' + odd);

        // 3. 求1-100之间所有能被3整除的数字的和   
        var result = 0;
        for (var i = 1; i <= 100; i++) {
            if (i % 3 == 0) {
                // result = result + i;
                result += i;
            }
        }
        console.log('1~100之间能够被3整数的数字的和是：' + result);
    </script>
</head>

<body>

</body>

</html>
```
## 8. 求学生成绩案例
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 弹出输入框输入总的班级人数(num)
        // 依次输入学生的成绩（ 保存起来 score）， 此时我们需要用到
        // for 循环， 弹出的次数跟班级总人数有关系 条件表达式 i <= num
        // 进行业务处理: 计算成绩。 先求总成绩（ sum）， 之后求平均成绩（ average）
        // 弹出结果
        var num = prompt('请输入班级的总人数:'); // num 总的班级人数
        var sum = 0; // 求和的变量
        var average = 0; // 求平均值的变量
        for (var i = 1; i <= num; i++) {
            var score = prompt('请您输入第' + i + '个学生成绩');
            // 因为从prompt取过来的数据是 字符串型的需要转换为数字型
            sum = sum + parseFloat(score);
        }
        average = sum / num;
        alert('班级总的成绩是' + sum);
        alert('班级平均分是：' + average);
    </script>
</head>

<body>

</body>

</html>
```
## 9. 打印五角星
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 一行打印五个星星 
        // console.log('★★★★★');
        // for (var i = 1; i <= 5; i++) {
        //     console.log('★');

        // }
        // var str = '';
        // for (var i = 1; i <= 5; i++) {
        //     str = str + '★';
        // }
        // console.log(str);
        var num = prompt('请输入星星的个数');
        var str = '';
        for (var i = 1; i <= num; i++) {
            str = str + '★'
        }
        console.log(str);
    </script>
</head>

<body>

</body>

</html>
```

## 10. 双重for循环
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. 双重for循环 语法结构
        // for (外层的初始化变量; 外层的条件表达式; 外层的操作表达式) {
        //     for (里层的初始化变量; 里层的条件表达式; 里层的操作表达式) {
        //         // 执行语句;
        //     }
        // }
        // 2. 我们可以把里面的循环看做是外层循环的语句
        // 3. 外层循环循环一次， 里面的循环执行全部
        // 4. 代码验证
        for (var i = 1; i <= 3; i++) {
            console.log('这是外层循环第' + i + '次');
            for (var j = 1; j <= 3; j++) {
                console.log('这是里层的循环第' + j + '次');

            }
        }
    </script>
</head>

<body>

</body>

</html>
```
## 11. 打印五行五列五角星
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 打印五行五列星星
        var str = '';
        for (var i = 1; i <= 5; i++) { // 外层循环负责打印五行
            for (var j = 1; j <= 5; j++) { // 里层循环负责一行打印五个星星
                str = str + '★';
            }
            // 如果一行打印完毕5个星星就要另起一行 加 \n
            str = str + '\n';
        }
        console.log(str);
    </script>
</head>

<body>

</body>

</html>
```

## 12. 打印n行n列五角星

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 打印n行n列的星星
        var rows = prompt('请您输入行数:');
        var cols = prompt('请您输入列数:');
        var str = '';
        for (var i = 1; i <= rows; i++) {
            for (var j = 1; j <= cols; j++) {
                str = str + '★';
            }
            str += '\n';
        }
        console.log(str);
    </script>
</head>

<body>

</body>

</html>
```
## 13. 打印倒三角形
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 打印倒三角形案例
        var str = '';
        for (var i = 1; i <= 10; i++) { // 外层循环控制行数
            for (var j = i; j <= 10; j++) { // 里层循环打印的个数不一样  j = i
                str = str + '★';
            }
            str += '\n';
        }
        console.log(str);
    </script>
</head>

<body>

</body>

</html>
```
## 14. 打印乘法口诀表
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 九九乘法表
        // 一共有9行，但是每行的个数不一样，因此需要用到双重 for 循环
        // 外层的 for 循环控制行数 i ，循环9次 ，可以打印 9 行  
        // 内层的 for 循环控制每行公式  j  
        // 核心算法：每一行 公式的个数正好和行数一致， j <= i;
        // 每行打印完毕，都需要重新换一行
        var str = '';
        for (var i = 1; i <= 9; i++) { // 外层循环控制行数
            for (var j = 1; j <= i; j++) { // 里层循环控制每一行的个数  j <= i
                // 1 × 2 = 2
                // str = str + '★';
                str += j + '×' + i + '=' + i * j + '\t';
            }
            str += '\n';
        }
        console.log(str);
    </script>
</head>

<body>

</body>

</html>
```
## 15. while循环
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1. while 循环语法结构  while 当...的时候
        // while (条件表达式) {
        //     // 循环体
        // }
        // 2. 执行思路  当条件表达式结果为true 则执行循环体 否则 退出循环
        // 3. 代码验证
        var num = 1;
        while (num <= 100) {
            console.log('好啊有');
            num++;
        }
        // 4. 里面应该也有计数器 初始化变量
        // 5. 里面应该也有操作表达式  完成计数器的更新 防止死循环
    </script>
</head>

<body>

</body>

</html>
```
## 16. while循环案例
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // while循环案例
        // 1. 打印人的一生，从1岁到100岁
        var i = 1;
        while (i <= 100) {
            console.log('这个人今年' + i + '岁了');
            i++;
        }
        // 2. 计算 1 ~ 100 之间所有整数的和
        var sum = 0;
        var j = 1;
        while (j <= 100) {
            sum += j;
            j++
        }
        console.log(sum);

        // 3. 弹出一个提示框， 你爱我吗？  如果输入我爱你，就提示结束，否则，一直询问。
        var message = prompt('你爱我吗?');
        while (message !== '我爱你') {
            message = prompt('你爱我吗?');
        }
        alert('我也爱你啊！');
    </script>
</head>

<body>

</body>

</html>
```
## 17. do while循环案例
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // 1.do while 循环 语法结构
        do {
            // 循环体
        } while (条件表达式)
        // 2.  执行思路 跟while不同的地方在于 do while 先执行一次循环体 在判断条件 如果条件表达式结果为真，则继续执行循环体，否则退出循环
        // 3. 代码验证
        var i = 1;
        do {
            console.log('how are you?');
            i++;
        } while (i <= 100)
        // 4. 我们的do while 循环体至少执行一次
    </script>
</head>

<body>

</body>

</html>
```
## 18. do while循环案例
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // while循环案例

        // 1. 打印人的一生，从1岁到100岁
        var i = 1;
        do {
            console.log('这个人今年' + i + '岁了');
            i++;
        } while (i <= 100)
        // 2. 计算 1 ~ 100 之间所有整数的和
        var sum = 0;
        var j = 1;
        do {
            sum += j;
            j++;
        } while (j <= 100)
        console.log(sum);

        // 3. 弹出一个提示框， 你爱我吗？  如果输入我爱你，就提示结束，否则，一直询问。
        do {
            var message = prompt('你爱我吗?');
        } while (message !== '我爱你')
        alert('我也爱你啊');
    </script>
</head>

<body>

</body>

</html>
```
## 19. continue
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // continue 关键字   退出本次（当前次的循环）  继续执行剩余次数循环
        for (var i = 1; i <= 5; i++) {
            if (i == 3) {
                continue; // 只要遇见 continue就退出本次循环 直接跳到 i++
            }
            console.log('我正在吃第' + i + '个包子');

        }
        // 1. 求1~100 之间， 除了能被7整除之外的整数和 
        var sum = 0;
        for (var i = 1; i <= 100; i++) {
            if (i % 7 == 0) {
                continue;
            }
            sum += i;
        }
        console.log(sum);
    </script>
</head>

<body>

</body>

</html>
```
## 20. break
```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script>
        // break 退出整个循环
        for (var i = 1; i <= 5; i++) {
            if (i == 3) {
                break;
            }
            console.log('我正在吃第' + i + '个包子');

        }
    </script>
</head>

<body>

</body>

</html>
```
# 第四天
## 1. 