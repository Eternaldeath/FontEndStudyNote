本教程主要参考了阮一峰老师的 [Javascript 教程](https://wangdoc.com/javascript/basic/grammar.html#break-%E8%AF%AD%E5%8F%A5%E5%92%8C-continue-%E8%AF%AD%E5%8F%A5) 等其他资料，浓缩了教程中的重要部分，主要是面向对 Javascript 再次复习的使用者。

**本笔记仅作为学习笔记使用。**

# 1.概述

## 简介

![image.png](0)

<font color="red">
Note：

1.原始类型是指无法再分割的数据
2.undefined 和 null 的区别在于，undefined 是完全没有这个值的空间，而 null 是有空间但是值为	空。比如，菜地里，有 A 坑，坑里种了 “整数”，此为有值；有 B 坑，坑里什么也没有，**但是有坑哦**，此为 null 值；菜地里什么坑也没有，此为 undefined。			
</font>

## 确定值类型

![image.png](1)

1.typeof 运算符
	
	typeof 运算符返回值的数据类型

```JavaScript
function f(){};

typeof 123;         // number
typeof '123';       // string
typeof false;       // boolean

typeof f;           // function
typeof undefined;   // undefined
typeof v;           // undefined，未定义的值在 typeof 中用 undefined 表示

typeof window;      // object
typeof {};          // object
typeof [];          // object
typeof null;        // object，历史原因造成的

```


<font color="red">Note：剩余两种方式需要其他的知识，会在后面讲解。</font>

# 2.null, undefined 和布尔值
## null 和 undefined
null 和 undefined 是由于历史原因产生的，在 Javascript 的替代语言 Dart 中，就删除了 undefined 。

null 和 undefined 在下面的情况效果相同

1.if 语句中都是 false
```Javascript
if(!undefined){
    alert("false"); // 弹出 alert
}

if(!null){
    alert("false"); // 弹出 alert
}

```

2.== 相等运算符两者相等
```Javascript
undefined == null; // true

```

## 布尔值
以下六个特殊的值将被自动转换为 false， 其他情况视为 true 。
1.	undefined
2.	null
3.	0
4.	NaN（非数值）
5.	false
6.	"" 或 ''

关于[NaN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/NaN)可以参见这个链接。

<font color="red">Note：空字符串和空对象对应的布尔值是 true</font>
```Javascript
if({}){
	alert('true'); // true
}
if([]){
	alert('true'); // true
}

```

# 3.数值
## 概述
### 整型和浮点型
	Javascript 的底层没有整数的概念，所有数值以 64 位浮点数存储，整型运算时化为 32 位整数

**问题**
浮点数不精确，所以使用时要注意
```Javascript
0.1 + 0.2 === 0.3; // false

0.3 + 0.2 === 0.5; // true

```

### 数值的精确度
	JavaScript 是由 64 位浮点数组成，其构成如下
![image.png](3)

所以，Javascript 中，数值超过了 2^53^ 就不能精确表示了。
```Javascript
Math.pow(2,53); // 9007199254740992

Math.pow(2,54); // 18014398509481984 失真了

```

### 数值范围
Javascript 可以表示 2^1024^ 到 2^-1023^ 之间的数值，超过则溢出。

## 与数值相关的全局方法
### parseInt()
#### 基本用法
```Javascript
// 字符串转换为整数
parseInt('123') // 123

// 空格被自动忽略
parseInt(' 123') // 123

// 遇到不能转换的字符停止转换
parseInt('123**') //123

// 第一个字符都不能转换，则返回 NaN
parseInt('*123') // NaN

```

### 进制转换
```Javascript
// 16 进制
parseInt('0xffff') // 65535

// 10 进制
parseInt('099') // 99

```

指定进制转换
```Javascript
// 1100 视作 2 进制转换成 10 进制
parseInt('1100',2);
 
// 1100 视作 8 进制转换成 10 进制
parseInt('1100',8);

// 1100 视作 16 进制转换成 10 进制
parseInt('1100',16);

```

### parseFloat
```Javascript
// 将字符串转换为浮点数
parseFloat('3.14') // 3.14

// 遇上不能转换的字符停止转换
parseFloat('3.14***') // 3.14

// 不能转换的字符串，返回 NaN
parseFloat('djdj') // NaN
parseFloat('') // NaN

```

# 4.字符串
## 概述
### 定义
	关于单引号和双引号，我们约定俗成的是，字符串用单引号，属性值用双引号。

特殊用法
```Javascript
// 1.字符串不能直接多行书写，反斜杠用于实现字符串换行（多行）书写，显示的结果还是一行
var a = 'long \
long \
string';
alert(a);

// 显示 long long string

//2. + 号连接多个字符串
var a='hello'+'world';

```

### 字符串与字符数组
	字符串可以当作字符数组使用。
```Javascript
var a='hello';
var b=a[0];
console.log(b);

// 输出 h

```

	Note：字符数组不能改变字符串本身的内容。

### length 属性
	length 属性用于返回字符串的长度，但是不可以改变字符串的长度。

```Javascript
var a='hello';
var b=a.length;
console.log(b);

//输出 5

```

### 字符集
JavaScript 可以用 Unicode 码点来表示字符。
具体连接[字符集的码点](https://wangdoc.com/javascript/types/string.html)



# 5.对象
## 概述
### 生成方法
	对象，从代码书写来看，就是键值对的集合。
```Javascript
var people = {
	student:"zhangsan",
	teacher:"lisi"
};

```

### 键名
	所有的键名都是字符串。
1.上面的代码也可以这样书写
```Javascript
var people = {
	'student':"zhangsan",
	'teacher':"lisi"
};

```
2.如果键名是单纯的数字，则该数字被自动转换成字符
```Javascript
var obj = {
	1:"a",
	3.2:"b"
}

```

3.如果键名是非法字符，则需要加上单引号
```Javascript
var obj = {
	'1p':"a",
	'3.2 p':"b"
}
```

4.键名 = 属性，如果属性的值是函数，则该属性又叫方法，并且该属性（方法）可以像函数一样调用
```Javascript
var obj = {
	p:function(x){
		return 2 * x;
	}
};

obj.p(2);

// 输出 4

```

5.如果一个属性的值还是一个对象，那么就形成了链式调用
```Javascript
var p1 = {};
var p2 = {bar:"Hi"};

p1.foo = p2;
p1.foo.bar;

// 输出 Hi

```

6.属性可以动态创建，不必再声明中制定
```Javascript
var p1 = {};
p1.name = "zhangsan";
p1.name;

// 输出 zhangsan

```

### 对象的引用
	1.不同的变量名，指向同一个对象，本质上指向的是同一个内存地址，输出的结果是一样的。
	2.如果修改其中一个变量名的属性值，另一个也会改变。
	3.如果修改其中一个变量名的指向，另一个不会改变。
```Javascript
var o1 = {};
var o2 = o1;

o1.number = 1;
o2.number;

// 输出 1

o2.number = 2;
o1.number;

// 输出 2

o1 = 1;
// 取消了 o1 对 {} 对象的引用，转而指向 1
o2.number;

// o2.number 还是输出 2，与 o1 的改变无关

```

上面的情况只用于引用的是独享，如果是引用原始类型的值，那么变量都是值拷贝。
```Javascript
var x = 1;
var y = x;

x = 2;
y;

// 输出 1
```
在这里，y 其实获得的是将 x 对应的内存地址 A 中的值（就是 1 ），复制到 y 对应的内存地址 B 中（值还是 1 ),所以当 x 发生改变，y 的值不变。

## 属性的操作
### 属性的读取
	属性的读取有 . 运算符和 [] 运算符两种

```Javascript
var p1 = {
	name:"zhangsan",
	age: 11
}

p1.name; // zhangsan
p1['age']; // 11

```

	如果使用 [] 但是内部不加单引号，则会出错，此时引用的将是变量，而不是属性
```Javascript
var foo = 'bar';

var obj = {
  foo: 1,
  bar: 2
};

obj.foo  // 1
obj[foo]  // 2

```

obj[foo] 引用的顺序是：指向最上面的 var foo = 'bar'，得到 bar，再回到对象内部找到 bar 的属性值 2。比如，现在去掉 var foo = 'bar'，就会报错，foo 没有定义。

1.[] 运算符的好处是可以使用表达式
```Javascript
var p1 = {
	name:"zhangsan",
	age: 11
}

p1.name;
p1['ag'+'e']; // 11

```

2.如果 [] 内是数字可以不加引号，因为会自动转换为字符串
```Javascript
var obj = {
  0.7: 'Hello World'
};

obj['0.7'] // "Hello World"
obj[0.7] // "Hello World"

```

### 属性的获取
	通过 Object.keys(属性)，可以获取属性的集合
```Javascript
var obj = {
	key1: 1,
	key2: 2,
}

Object.keys(obj);
// 输出 ["key1", "key2"]

```

### 属性的删除
```Javascript
var obj = {
	key1: 1,
	key2: 2,
}

delete obj.key1; // 删除属性

Object.keys(obj);
// 输出 ["key2"]
```

<font color="red">Note：delete 只能删除本身的属性，不能删除继承的属性。</font>

### 属性是否存在运算符：in
```Javascript
var obj = {
	key1: 1,
	key2: 2,
}

delete obj.key1;

'key1' in obj;
// 因为 key1 不存在，所以返回 false

```

<font color="red">Note：in 运算符不能检测属性是继承还是本身的</font>
```Javascript
var obj = {
	key1: 1,
	key2: 2,
}

delete obj.key1;

'key1' in obj;

console.log(obj.hasOwnProperty('toString'));
// hasOwnProperty 用于验证属性是否属于本身

```










 

















