本教程主要参考了阮一峰老师的 [Javascript 教程](https://wangdoc.com/javascript/basic/grammar.html#break-%E8%AF%AD%E5%8F%A5%E5%92%8C-continue-%E8%AF%AD%E5%8F%A5) 等其他资料，浓缩了教程中的重要部分，主要是面向对 Javascript 再次复习的使用者。

**本笔记仅作为学习笔记使用。**

# 语句

```Javascript
// 常规的语句
var a = 1+3;

// 空语句
;;;
```

	Note
	1.有分号是语句，没有分号是表达式
	2.值 = 表达式 || 单个字符

# 变量
## 基本概念
变量是对值得引用，是给这个值起得一个名字。

```Javascript
var a = 1;
```

变量得声明与赋值时两个动作
```Javascript
var a;
a = 1;

// 只声明无赋值，该值为 undefined
var a；
a；// undefined
```

## 变量提升
Javascript 得运行机制是先解析代码，获取所有被声明得变量，再一行行执行。
我们通过下面得例子来解释。

```Javascript
console.log(a);
var a = 1;
```

解析：理论上 a 在打印得时候并没有声明和赋值，但是代码不会报错，就是因为变量提升了。

# 注释
单行注释
```Javascript
// 这是单行注释
```

这是多行注释
```Javascript
<!-- 
	这是多行注释
-->

```

# 条件语句
## if 结构
基本的 if 语句
```Javascript
if(1==2)
{
	alert(1);
}

```
基本的 if...else 语句

```Javascript
	if(1 == 2)
	{
		alert(1);
	}
	else
	{
		alert(2);
	}
```

switch 结构
```Javascript
switch(A){
    case 'A':
        // 执行的内容
        break;
    case 'B':
        // 执行的内容
        break;
    default:
        // 执行的内容
}

```

	Note：
	1.switch 后面的表达式和 case 的值采用的是严格等于（===），所以不发生类型转换，关于严
	格等于的内容会在后面提到。
```Javascript
var x = 1;

switch (x) {
  case true:
    console.log('x 发生类型转换');
    break;
  default:
    console.log('x 没有发生类型转换');
}
// 输出 x 没有发生类型转换
```

# 循环
## 基本的循环方式
Javascript 中有 while，do...while，for 等循环，这里不细讲。

## break 和 continue 语句
break 语句用于终止（跳出）所有循环
```Javascript
var i=0;
while(i<100){
    i++;
    if(i == 3){
        break;
    }
}

alert(i); // i 为 3

```

continue 用于跳出本次循环，并继续下一次循环
```Javascript
var i=0;
while(i<100){
    i++;
    if(i == 3){
        continue;
    }
console.log(i); // 当 i 为 3 的时候不会被打印出来
}

alert(i);
```













