## 什么是JavaScript语言？
+ javaScript是一种轻量级的脚本语言，所谓脚本语言（script language），指的是它不具备开发操作系统的能力，而是只用来编写控制其他大型应用程序（比如浏览器的）脚本。
+ JavaScript 也是一种嵌入式（embedded）语言。本身不提供任何与 I/O（输入/输出）相关的 API，都要靠宿主环境（host）提供，所以 JavaScript 只合适嵌入更大型的应用程序环境，去调用宿主环境提供的底层 API。目前，已经嵌入 JavaScript 的宿主环境有多种，最常见的环境就是浏览器，另外还有服务器环境，也就是 Node 项目。
+ 从语法角度看，JavaScript 语言是一种“对象模型”语言。但是，JavaScript 并不是纯粹的“面向对象语言”，还支持其他编程范式（比如函数式编程）。这导致几乎任何一个问题，JavaScript 都有多种解决方法。
+ JavaScript 的核心语法部分相当精简，只包括两个部分：基本的语法构造（比如操作符、控制结构、语句）和标准库（就是一系列具有各种功能的对象比如Array、Date、Math等）。除此之外，各种宿主环境提供额外的 API（即只能在该环境使用的接口），以便 JavaScript 调用。以浏览器为例，它提供的额外 API 可以分成三大类。1、浏览器控制类：操作浏览器；2、DOM 类：操作网页的各种元素；3、Web 类：实现互联网的各种功能；如果宿主环境是服务器，则会提供各种操作系统的 API，比如文件操作 API、网络通信 API等等。

### 一、基本语法
#### 1、语句

JavaScript 程序的执行单位为行（line），也就是一行一行地执行。一般情况下，每一行就是一个语句。
语句（statement）是为了完成某种任务而进行的操作，比如下面就是一行赋值语句。
```
var a = 1 + 3;
```
1 + 3 叫做表达式（expression），指一个为了得到返回值的计算式。
语句以分号结尾，一个分号就表示一个语句结束。多个语句可以写在一行内。
```
var a = 1 + 3 ; var b = 'abc';
```
分号前面可以没有任何内容，JavaScript 引擎将其视为空语句。
```
;;;
```
上面的代码就表示3个空语句。

#### 2、变量
+ 2.1 概念
变量是对“值”的具名引用。变量就是为“值”起名，然后引用这个名字，就等同于引用这个值。变量的名字就是变量名。
```
var a = 1;
```
JavaScript 是一种动态类型语言，也就是说，变量的类型没有限制，变量可以随时更改类型。
```
var a = 1;
a = 'hello';
```

+ 2.2 变量提升
JavaScript 引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行地运行。这造成的结果，就是所有的变量的声明语句，都会被提升到代码的头部，这就叫做变量提升（hoisting）。
```
console.log(a);
var a = 1;
```
上面代码首先使用console.log方法，在控制台（console）显示变量a的值。这时变量a还没有声明和赋值，所以这是一种错误的做法，但是实际上不会报错。因为存在变量提升，真正运行的是下面的代码
```
var a;
console.log(a);
a = 1;
```
最后的结果是显示undefined，表示变量a已声明，但还未赋值。

#### 3、标志符

+ 标识符（identifier）指的是用来识别各种值的合法名称。最常见的标识符就是变量名，以及后面要提到的函数名。JavaScript 语言的标识符对大小写敏感，所以a和A是两个不同的标识符。
+ 标识符有一套命名规则，不符合规则的就是非法标识符。JavaScript 引擎遇到非法标识符，就会报错。
+ 简单说，标识符命名规则如下：
+ 1、第一个字符，可以是任意 Unicode 字母（包括英文字母和其他语言的字母），以及美元符号（$）和下划线（_）。
+ 2、第二个字符及后面的字符，除了 Unicode 字母、美元符号和下划线，还可以用数字0-9。
注意：中文是合法的标识符，可以用作变量名。
```
JavaScript 有一些保留字，不能用作标识符：arguments、break、case、catch、class、const、continue、debugger、default、delete、do、else、enum、eval、export、extends、false、finally、for、function、if、implements、import、in、instanceof、interface、let、new、null、package、private、protected、public、return、static、super、switch、this、throw、true、try、typeof、var、void、while、with、yield。
```


#### 4、注释
+ 源码中被 JavaScript 引擎忽略的部分就叫做注释，它的作用是对代码进行解释。JavaScript 提供两种注释的写法：一种是单行注释，用//起头；另一种是多行注释，放在/*和*/之间。
```
// 这是单行注释

/*
 这是
 多行
 注释
*/
```
+ 此外，由于历史上 JavaScript 可以兼容 HTML 代码的注释，所以<!--和-->也被视为合法的单行注释。
```
x = 1; <!-- x = 2;
--> x = 3;
```

#### 5、区块
+ JavaScript 使用大括号，将多个相关的语句组合在一起，称为“区块”（block）。
```
{
  var a = 1;
}
a // 1
```
对于var命令来说，JavaScript 的区块不构成单独的作用域（scope）。
上面代码在区块内部，使用var命令声明并赋值了变量a，然后在区块外部，变量a依然有效，区块对于var命令不构成单独的作用域，与不使用区块的情况没有任何区别。在 JavaScript 语言中，单独使用区块并不常见，区块往往用来构成其他更复杂的语法结构，比如for、if、while、function等。

#### 6、条件语句
+ JavaScript 提供if结构和switch和三元运算符结构，完成条件判断，即只有满足预设的条件，才会执行相应的语句。
#### 7、循环语句
循环语句用于重复执行某个操作，它有多种形式。
+ 1、while 循环：While语句包括一个循环条件和一段代码块，只要条件为真，就不断循环执行代码块。
+ 2、for 循环：for语句是循环命令的另一种形式，可以指定循环的起点、终点和终止条件。
+ 3、do...while 循环：do...while循环与while循环类似，唯一的区别就是先运行一次循环体，然后判断循环条件。
+ 4、break 语句和 continue 语句：break语句用于跳出代码块或循环。continue语句用于立即终止本轮循环，返回循环结构的头部，开始下一轮循环。
+ 5、标签（label）：JavaScript 语言允许，语句的前面有标签（label），相当于定位符，用于跳转到程序的任意位置，

### 二、数据类型
#### 1、简介
JavaScript 语言的每一个值，都属于某一种数据类型。JavaScript 的数据类型，共有六种。（ES6 又新增了第七种 Symbol 类型的值）
+ 数值（number）：整数和小数（比如1和3.14）。
+ 字符串（string）：文本（比如Hello World）。
+ 布尔值（boolean）：表示真伪的两个特殊值，即true（真）和false（假）。
+ undefined：表示“未定义”或不存在，即由于目前没有定义，所以此处暂时没有任何值。
+ null：表示空值，即此处的值为空。
+ 对象（object）：各种值组成的集合。

对象是最复杂的数据类型，又可以分成三个子类型。
+ 狭义的对象（object）
+ 数组（array）
+ 函数（function）

#### 2、typeof 运算符
+ typeof运算符（运算符可以返回一个值的数据类型。但是不能区分数组和对象，typeof运算符对数组也返回对象类型，注意：typeof null // "object"，null的类型是object）
+ instanceof运算符（instanceof运算符可以区分数组和对象）
+ Object.prototype.toString方法

#### 3、null 和 undefined
+ null与undefined都可以表示“没有”，含义非常相似。将一个变量赋值为undefined或null，老实说，语法效果几乎没区别。
+ 区别是这样的：null是一个表示“空”的对象，转为数值时为0；undefined是一个表示"此处无定义"的原始值，转为数值时为NaN。

#### 4、布尔值
+ 布尔值代表“真”和“假”两个状态。“真”用关键字true表示，“假”用关键字false表示。布尔值只有这两个值。
+ 转换规则是除了下面六个值被转为false，其他值都视为true。
```
undefined
null
false
0
NaN
""或''（空字符串）
```
#### 5、数值
JavaScript 内部，所有数字都是以64位浮点数形式储存，即使整数也是如此。所以，1与1.0是相同的，是同一个数。
+ 由于浮点数不是精确的值，所以涉及小数的比较和运算要特别小心。
```
0.1 + 0.2 === 0.3
// false

0.3 / 0.1
// 2.9999999999999996

(0.3 - 0.2) === (0.2 - 0.1)
// false
```
+ JavaScript 提供Number对象的MAX_VALUE和MIN_VALUE属性，返回可以表示的具体的最大值和最小值。
+ 与数值相关的全局方法
```
1、parseInt方法用于将字符串转为整数，parseInt方法还可以接受第二个参数（2到36之间），表示被解析的值的进制。
2、parseFloat方法用于将一个字符串转为浮点数。
3、isNaN方法可以用来判断一个值是否为NaN。
4、isFinite方法返回一个布尔值，表示某个值是否为正常的数值。
```
#### 6、字符串
+ 字符串就是零个或多个排在一起的字符，放在单引号或双引号之中。
+ 单引号字符串的内部，可以使用双引号。双引号字符串的内部，可以使用单引号。
+ 字符串可以被视为字符数组，因此可以使用数组的方括号运算符，用来返回某个位置的字符（位置编号从0开始）。
```
var s = 'hello';
s[0] // "h"
s[1] // "e"
s[4] // "o"

// 直接对字符串使用方括号运算符
'hello'[1] // "e"
```
+ length属性返回字符串的长度，该属性也是无法改变的。

### 7、对象
对象（object）是 JavaScript 语言的核心概念，也是最重要的数据类型。
什么是对象？简单说，对象就是一组“键值对”（key-value）的集合，是一种无序的复合数据集合。
+ 如果不同的变量名指向同一个对象，那么它们都是这个对象的引用，也就是说指向同一个内存地址，修改其中一个变量，会影响到其他所有变量。
+ 读取对象的属性，有两种方法，一种是使用点运算符，还有一种是使用方括号运算符。
```
var obj = {
  p: 'Hello World'
};
obj.p // "Hello World"
obj['p'] // "Hello World"
```
+ 点运算符和方括号运算符，不仅可以用来读取值，还可以用来赋值。
```
var obj = {};
obj.foo = 'Hello';
obj['bar'] = 'World';
```
+ JavaScript 允许属性的“后绑定”，也就是说，你可以在任意时刻新增属性，没必要在定义对象的时候，就定义好属性。
```
var obj = { p: 1 };
// 等价于
var obj = {};
obj.p = 1;
```
+ 查看一个对象本身的所有属性，可以使用Object.keys方法。
```
var obj = {
  key1: 1,
  key2: 2
};
Object.keys(obj);
// ['key1', 'key2']
```
+ delete命令用于删除对象的属性，删除成功后返回true,只有一种情况，delete命令会返回false，那就是该属性存在，且不得删除。
```
var obj = Object.defineProperty({}, 'p', {
  value: 123,
  configurable: false
});
obj.p // 123
delete obj.p // false
```
+ in运算符用于检查对象是否包含某个属性,n运算符的一个问题是，它不能识别哪些属性是对象自身的，哪些属性是继承的。这时，可以使用对象的hasOwnProperty方法判断一下，是否为对象自身的属性。
```
var obj = {};
if ('toString' in obj) {
  console.log(obj.hasOwnProperty('toString')) // false
}
```
+ for...in循环用来遍历一个对象的全部属性。
+ for...in循环有两个使用注意点:1、它遍历的是对象所有可遍历（enumerable）的属性，会跳过不可遍历的属性。2、它不仅遍历对象自身的属性，还遍历继承的属性。
```
var obj = {a: 1, b: 2, c: 3};

for (var i in obj) {
  console.log('键名：', i);
  console.log('键值：', obj[i]);
}
```
+ JavaScript 中 call()、apply()、bind()都是用来重定义 this 这个对象的（修改this指向）！
```
var name = "神里",age = 16;
var obj = {
	name:'阿晴',
	age:this.age,
	myFun:function(a,b){
		console.log(this.name + '年龄' + this.age,'来自' + a + '去往' + b)
	}
}
var newObj = {
	name:"旅行者",
	age:999
}
obj.myFun.call(newObj,'璃月','稻期')；　　　　 // 旅行者年龄999，来自璃月去往稻期
obj.myFun.apply(newObj,['璃月','稻期']);      // 旅行者年龄999，来自璃月去往稻期  
obj.myFun.bind(newObj,'璃月','稻期')();       // 旅行者年龄999，来自璃月去往稻期
obj.myFun.bind(newObj,['璃月','稻期'])();　　 // 旅行者年龄999，来自璃月,稻期去往undefined

call 、bind 、 apply 这三个函数的第一个参数都是 this 的指向对象，第二个参数差别就来了：
call的参数是直接放进去的，第二第三第n个参数全都用逗号分隔，直接放到后面 obj.myFun.call(newObj,'璃月','稻期')；
apply的所有参数都必须放在一个数组里面传进去 obj.myFun.apply(newObj,['璃月','稻期']);
bind除了返回是函数以外，它的参数和call 一样。

```

#### 8、函数
JavaScript 有三种声明函数的方法。
+ （1）function 命令
```
function print(s) {
  console.log(s);
}
```
+ （2）函数表达式
```
var print = function(s) {
  console.log(s);
};
```
+ （3）Function 构造函数
```
var add = new Function(
  'x',
  'y',
  'return x + y'
);

// 等同于
function add(x, y) {
  return x + y;
}
```
+ 如果同一个函数被多次声明，后面的声明就会覆盖前面的声明。
+ 调用函数时，要使用圆括号运算符。圆括号之中，可以加入函数的参数。
+ 函数可以调用自身，这就是递归（recursion）。
+ JavaScript 语言将函数看作一种值，与其它值（数值、字符串、布尔值等等）地位相同，所以在 JavaScript 语言中又称函数为第一等公民。
+ JavaScript 引擎将函数名视同变量名，所以采用function命令声明函数时，整个函数会像变量声明一样，被提升到代码头部。所以，下面的代码不会报错。
```
f();
function f() {}
```
+ 函数执行时所在的作用域，是定义时的作用域，而不是调用时所在的作用域。
```
 // 定义在外部
var x = function () {
  console.log(a);
};

function y(f) {
  var a = 2;
  f();
}

y(x)
// ReferenceError: a is not defined

// 定义在内部
function foo() {
  var x = 1;
  function bar() {
    console.log(x);
  }
  return bar;
}

var x = 2;
var f = foo();
f() // 1
```
+ 函数参数如果是原始类型的值（数值、字符串、布尔值），传递方式是传值传递（passes by value）。这意味着，在函数体内修改参数值，不会影响到函数外部。
```
var p = 2;
function f(p) {
  p = 3;
}
f(p);
p // 2
```
+ 如果函数参数是复合类型的值（数组、对象、其他函数），传递方式是传址传递（pass by reference）。也就是说，传入函数的原始值的地址，因此在函数内部修改参数，将会影响到原始值。
```
var obj = { p: 1 };
function f(o) {
  o.p = 2;
}
f(obj);
obj.p // 2
```
+ 如果有同名的参数，则取最后出现的那个值。
```
function f(a, a) {
  console.log(a);
}
f(1, 2) // 2
```
#### arguments 对象
+ 由于 JavaScript 允许函数有不定数目的参数，所以需要一种机制，可以在函数体内部读取所有参数。这就是arguments对象的由来。
+ arguments对象包含了函数运行时的所有参数，arguments[0]就是第一个参数，arguments[1]就是第二个参数，以此类推。这个对象只有在函数体内部，才可以使用。
```
var f = function (one) {
  console.log(arguments[0]);
  console.log(arguments[1]);
  console.log(arguments[2]);
}
f(1, 2, 3)
// 1
// 2
// 3
```
+ 正常模式下，arguments对象可以在运行时修改。
```
var f = function(a, b) {
  arguments[0] = 3;
  arguments[1] = 2;
  return a + b;
}
f(1, 1) // 5
```
+ 严格模式下，arguments对象与函数参数不具有联动关系。也就是说，修改arguments对象不会影响到实际的函数参数。
```
var f = function(a, b) {
  'use strict'; // 开启严格模式
  arguments[0] = 3;
  arguments[1] = 2;
  return a + b;
}
f(1, 1) // 2
```
+ 通过arguments对象的length属性，可以判断函数调用时到底带几个参数。
```
function f() {
  return arguments.length;
}
f(1, 2, 3) // 3
f(1) // 1
f() // 0
```
+ 需要注意的是，虽然arguments很像数组，但它是一个对象。数组专有的方法（比如slice和forEach），不能在arguments对象上直接使用。如果要让arguments对象使用数组方法，真正的解决方法是将arguments转为真正的数组。下面是两种常用的转换方法：slice方法和逐一填入新数组。
```
var args = Array.prototype.slice.call(arguments);
// 也可以这样写
var args = [].slice.call(arguments);

// 或者
var args = [];
for (var i = 0; i < arguments.length; i++) {
  args.push(arguments[i]);
}
```
+ arguments对象带有一个callee属性，返回它所对应的原函数，可以通过arguments.callee，达到调用函数自身的目的，这个属性在严格模式里面是禁用的，因此不建议使用。
```
var f = function () {
  console.log(arguments.callee === f);
}
f() // true
```
#### 闭包（能够读取其他函数内部变量的函数）
闭包（closure）是 JavaScript 语言的一个难点，也是它的特色，很多高级应用都要依靠闭包实现。
+ 理解闭包，首先必须理解变量作用域。前面提到，JavaScript 有两种作用域：全局作用域和函数作用域。函数内部可以直接读取全局变量。
```
var n = 999;
function f1() {
  console.log(n);
}
f1() // 999
```
+ 但是，正常情况下，函数外部无法读取函数内部声明的变量。
```
function f1() {
  var n = 999;
}
console.log(n)
// Uncaught ReferenceError: n is not defined(
```
+ 如果出于种种原因，需要得到函数内的局部变量。正常情况下，这是办不到的，只有通过变通方法才能实现。那就是在函数的内部，再定义一个函数。
```
function f1() {
  var n = 999;
  function f2() {
　　console.log(n); // 999
  }
}
```
+ 上面代码中，函数f2就在函数f1内部，这时f1内部的所有局部变量，对f2都是可见的。但是反过来就不行，f2内部的局部变量，对f1就是不可见的。这就是 JavaScript 语言特有的"链式作用域"结构（chain scope），子对象会一级一级地向上寻找所有父对象的变量。所以，父对象的所有变量，对子对象都是可见的，反之则不成立。既然f2可以读取f1的局部变量，那么只要把f2作为返回值，我们不就可以在f1外部读取它的内部变量了吗！
```
function f1() {
  var n = 999;
  function f2() {
    console.log(n);
  }
  return f2;
}
var result = f1();
result(); // 999
```
+ 闭包就是函数f2，即能够读取其他函数内部变量的函数。由于在 JavaScript 语言中，只有函数内部的子函数才能读取内部变量，因此可以把闭包简单理解成“定义在一个函数内部的函数”。闭包最大的特点，就是它可以“记住”诞生的环境，比如f2记住了它诞生的环境f1，所以从f2可以得到f1的内部变量。在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。
+ 闭包的最大用处有两个，一个是可以读取外层函数内部的变量，另一个就是让这些变量始终保持在内存中，即闭包可以使得它诞生环境一直存在。请看下面的例子，闭包使得内部变量记住上一次调用时的运算结果。
```
function createIncrementor(start) {
  return function () {
    return start++;
  };
}
var inc = createIncrementor(5);
inc() // 5
inc() // 6
inc() // 7
```
+ 为什么闭包能够返回外层函数的内部变量？原因是闭包（上例的inc）用到了外层变量（start），导致外层函数（createIncrementor）不能从内存释放。只要闭包没有被垃圾回收机制清除，外层函数提供的运行环境也不会被清除，它的内部变量就始终保存着当前值，供闭包读取。
+ 闭包的另一个用处，是封装对象的私有属性和私有方法。
```
function Person(name) {
  var _age;
  function setAge(n) {
    _age = n;
  }
  function getAge() {
    return _age;
  }

  return {
    name: name,
    getAge: getAge,
    setAge: setAge
  };
}

var p1 = Person('张三');
p1.setAge(25);
p1.getAge() // 25
```
+ 上面代码中，函数Person的内部变量_age，通过闭包getAge和setAge，变成了返回对象p1的私有变量。
+ 注意，外层函数每次运行，都会生成一个新的闭包，而这个闭包又会保留外层函数的内部变量，所以内存消耗很大。因此不能滥用闭包，否则会造成网页的性能问题。

#### 立即调用的函数表达式（IIFE）
根据 JavaScript 的语法，圆括号()跟在函数名之后，表示调用该函数。比如，print()就表示调用print函数。
+ 有时，我们需要在定义函数之后，立即调用该函数。这时，你不能在函数的定义之后加上圆括号，这会产生语法错误。
```
function(){ /* code */ }();
// SyntaxError: Unexpected token (
```
+ 产生这个错误的原因是，function这个关键字既可以当作语句，也可以当作表达式。
```
// 语句
function f() {}

// 表达式
var f = function f() {}
```
+ 当作表达式时，函数可以定义后直接加圆括号调用。
```
var f = function f(){ return 1}();
f // 1
```
+ 上面的代码中，函数定义后直接加圆括号调用，没有报错。原因就是function作为表达式，引擎就把函数定义当作一个值。这种情况下，就不会报错。为了避免解析的歧义，JavaScript 规定，如果function关键字出现在行首，一律解释成语句。因此，引擎看到行首是function关键字之后，认为这一段都是函数的定义，不应该以圆括号结尾，所以就报错了。
+ 函数定义后立即调用的解决方法，就是不要让function出现在行首，让引擎将其理解成一个表达式，最简单的处理，就是将其放在一个圆括号里面。
```
(function(){ /* code */ }());
// 或者
(function(){ /* code */ })();
```
+ 上面两种写法都是以圆括号开头，引擎就会认为后面跟的是一个表达式，而不是函数定义语句，所以就避免了错误。这就叫做“立即调用的函数表达式”（Immediately-Invoked Function Expression），简称 IIFE。
+ 注意，上面两种写法最后的分号都是必须的。如果省略分号，遇到连着两个 IIFE，可能就会报错。
+ 推而广之，任何让解释器以表达式来处理函数定义的方法，都能产生同样的效果，比如下面三种写法。
```
var i = function(){ return 10; }();
true && function(){ /* code */ }();
0, function(){ /* code */ }();
```
+ 甚至像下面这样写，也是可以的。
```
!function () { /* code */ }();
~function () { /* code */ }();
-function () { /* code */ }();
+function () { /* code */ }();
```
+ 通常情况下，只对匿名函数使用这种“立即执行的函数表达式”。它的目的有两个：一是不必为函数命名，避免了污染全局变量；二是 IIFE 内部形成了一个单独的作用域，可以封装一些外部无法读取的私有变量。
```
// 写法一
var tmp = newData;
processData(tmp);
storeData(tmp);

// 写法二
(function () {
  var tmp = newData;
  processData(tmp);
  storeData(tmp);
}());
```
+ 上面代码中，写法二比写法一更好，因为完全避免了污染全局变量。

#### 9、数组
数组（array）是按次序排列的一组值。每个值的位置都有编号（从0开始），整个数组用方括号表示。
+ 本质上，数组属于一种特殊的对象。typeof运算符会返回数组的类型是object。
```
typeof [1, 2, 3] // "object"
```
+ 数组的特殊性体现在，它的键名是按次序排列的一组整数（0，1，2...）。
```
var arr = ['a', 'b', 'c'];
Object.keys(arr)
// ["0", "1", "2"]
```
+ 上面代码中，Object.keys方法返回数组的所有键名。可以看到数组的键名就是整数0、1、2。
+ 对象有两种读取成员的方法：点结构（object.key）和方括号结构（object[key]）。但是，对于数值的键名，不能使用点结构。
```
var arr = [1, 2, 3];
arr.0 // SyntaxError
```
+ 上面代码中，arr.0的写法不合法，因为单独的数值不能作为标识符（identifier）。所以，数组成员只能用方括号arr[0]表示（方括号是运算符，可以接受数值）。
+ 数组的length属性，返回数组的成员数量。
```
['a', 'b', 'c'].length // 3
```
+ 只要是数组，就一定有length属性。该属性是一个动态的值，等于键名中的最大整数加上1。
+ length属性是可写的。如果人为设置一个小于当前成员个数的值，该数组的成员数量会自动减少到length设置的值。
```
var arr = [ 'a', 'b', 'c' ];
arr.length // 3
arr.length = 2;
arr // ["a", "b"]
```
### in 运算符 
+ 检查某个键名是否存在的运算符in，适用于对象，也适用于数组。
```
var arr = [ 'a', 'b', 'c' ];
2 in arr  // true
'2' in arr // true
4 in arr // false
```
#### for...in 循环和数组的遍历
+ for...in循环不仅可以遍历对象，也可以遍历数组，毕竟数组只是一种特殊对象。
```
var a = [1, 2, 3];
for (var i in a) {
  console.log(a[i]);
}
// 1
// 2
// 3
```
+ 但是，for...in不仅会遍历数组所有的数字键，还会遍历非数字键。
```
var a = [1, 2, 3];
a.foo = true;

for (var key in a) {
  console.log(key);
}
// 0
// 1
// 2
// foo
```
+ 上面代码在遍历数组时，也遍历到了非整数键foo。所以，不推荐使用for...in遍历数组。数组的遍历可以考虑使用for循环或while循环。
```
var a = [1, 2, 3];

// for循环
for(var i = 0; i < a.length; i++) {
  console.log(a[i]);
}

// while循环
var i = 0;
while (i < a.length) {
  console.log(a[i]);
  i++;
}

var l = a.length;
while (l--) {
  console.log(a[l]);
}
```
+ 数组的forEach方法，也可以用来遍历数组
```
var colors = ['red', 'green', 'blue'];
colors.forEach(function (color) {
  console.log(color);
});
// red
// green
// blue
```
#### 数组的空位
+ 当数组的某个位置是空元素，即两个逗号之间没有任何值，我们称该数组存在空位（hole）。
```
var a = [1, , 1];
a.length // 3
```
+ 数组的空位是可以读取的，返回undefined。
```
var a = [, , ,];
a[1] // undefined
```
+ 使用delete命令删除一个数组成员，会形成空位，并且不会影响length属性。
```
var a = [1, 2, 3];
delete a[1];

a[1] // undefined
a.length // 3
```
+ 上面代码用delete命令删除了数组的第二个元素，这个位置就形成了空位，但是对length属性没有影响。也就是说，length属性不过滤空位。所以，使用length属性进行数组遍历，一定要非常小心。
+ 数组的某个位置是空位，与某个位置是undefined，是不一样的。如果是空位，使用数组的forEach方法、for...in结构、以及Object.keys方法进行遍历，空位都会被跳过。
```
var a = [, , ,];

a.forEach(function (x, i) {
  console.log(i + '. ' + x);
})
// 不产生任何输出

for (var i in a) {
  console.log(i);
}
// 不产生任何输出

Object.keys(a)
// []
```
+ 如果某个位置是undefined，遍历的时候就不会被跳过。
```
var a = [undefined, undefined, undefined];

a.forEach(function (x, i) {
  console.log(i + '. ' + x);
});
// 0. undefined
// 1. undefined
// 2. undefined

for (var i in a) {
  console.log(i);
}
// 0
// 1
// 2

Object.keys(a)
// ['0', '1', '2']
```
+ 这就是说，空位就是数组没有这个元素，所以不会被遍历到，而undefined则表示数组有这个元素，值是undefined，所以遍历不会跳过。
#### 类似数组的对象
如果一个对象的所有键名都是正整数或零，并且有length属性，那么这个对象就很像数组，语法上称为“类似数组的对象”（array-like object）。
+ 典型的“类似数组的对象”是函数的arguments对象，以及大多数 DOM 元素集，还有字符串。
```
// arguments对象
function args() { return arguments }
var arrayLike = args('a', 'b');

arrayLike[0] // 'a'
arrayLike.length // 2
arrayLike instanceof Array // false

// DOM元素集
var elts = document.getElementsByTagName('h3');
elts.length // 3
elts instanceof Array // false

// 字符串
'abc'[1] // 'b'
'abc'.length // 3
'abc' instanceof Array // false
```
+ 上面代码包含三个例子，它们都不是数组（instanceof运算符返回false），但是看上去都非常像数组。
+ 数组的slice方法可以将“类似数组的对象”变成真正的数组。
```
var args = Array.prototype.slice.call(arrayLike);
// 也可以这样写
var args = [].slice.call(arrayLike);
```
+ 除了转为真正的数组，“类似数组的对象”还有一个办法可以使用数组的方法，就是通过call()把数组的方法放到对象上面。
```
function print(value, index) {
  console.log(index + ' : ' + value);
}
Array.prototype.forEach.call(arrayLike, print);
```
+ 上面代码中，arrayLike代表一个类似数组的对象，本来是不可以使用数组的forEach()方法的，但是通过call()，可以把forEach()嫁接到arrayLike上面调用。
+ 下面的例子就是通过这种方法，在arguments对象上面调用forEach方法。
```
// forEach 方法
function logArgs() {
  Array.prototype.forEach.call(arguments, function (elem, i) {
    console.log(i + '. ' + elem);
  });
}

// 等同于 for 循环
function logArgs() {
  for (var i = 0; i < arguments.length; i++) {
    console.log(i + '. ' + arguments[i]);
  }
}
```
+ 字符串也是类似数组的对象，所以也可以用Array.prototype.forEach.call遍历。
```
Array.prototype.forEach.call('abc', function (chr) {
  console.log(chr);
});
// a
// b
// c
```
+ 注意，这种方法比直接使用数组原生的forEach要慢，所以最好还是先将“类似数组的对象”转为真正的数组，然后再直接调用数组的forEach方法。
```
var arr = Array.prototype.slice.call('abc');
arr.forEach(function (chr) {
  console.log(chr);
});
// a
// b
// c
```
### 三、运算符

#### 1、概述
JavaScript 共提供10个算术运算符，用来完成基本的算术运算。
+ 加法运算符：x + y
+ 减法运算符： x - y
+ 乘法运算符： x * y
+ 除法运算符：x / y
+ 指数运算符：x ** y
+ 余数运算符：x % y
+ 自增运算符：++x 或者 x++
+ 自减运算符：--x 或者 x--
+ 数值运算符： +x
+ 负数值运算符：-x
+ 减法、乘法、除法运算法比较单纯，就是执行相应的数学运算，下面介绍其他几个算术运算符，重点是加法运算符。

#### 2、加法运算符
+ 加法运算符（+）是最常见的运算符，用来求两个数值的和。
+ 加法运算符是在运行时决定，到底是执行相加，还是执行连接。也就是说，运算子的不同，导致了不同的语法行为，这种现象称为“重载”（overload）。由于加法运算符存在重载，可能执行两种运算，使用的时候必须很小心。
```
3 + 4 + 5 // 12
'3' + 4 + 5 // "345"
3 + 4 + '5' // "75"
```
#### 对象的相加
+ 如果运算子是对象，必须先转成原始类型的值，然后再相加。
```
var obj = { p: 1 };
obj + 2 // "[object Object]2"
```
+ 对象转成原始类型的值，规则如下：首先，自动调用对象的valueOf方法。
```
var obj = { p: 1 };
obj.valueOf() // { p: 1 }
```
+ 一般来说，对象的valueOf方法总是返回对象自身，这时再自动调用对象的toString方法，将其转为字符串。
```
var obj = { p: 1 };
obj.valueOf().toString() // "[object Object]"
```
+ 对象的toString方法默认返回[object Object]，所以就得到了最前面那个例子的结果。知道了这个规则以后，就可以自己定义valueOf方法或toString方法，得到想要的结果。
```
var obj = {
  valueOf: function () {
    return 1;
  }
};

obj + 2 // 3

var obj2 = {
  toString: function () {
    return 'hello';
  }
};

obj2 + 2 // "hello2"
```
+ 这里有一个特例，如果运算子是一个Date对象的实例，那么会优先执行toString方法。
```
var obj = new Date();
obj.valueOf = function () { return 1 };
obj.toString = function () { return 'hello' };
obj + 2 // "hello2"
```

#### 3、余数运算符
余数运算符（%）返回前一个运算子被后一个运算子除，所得的余数，需要注意的是，运算结果的正负号由第一个运算子的正负号决定。
```
12 % 5 // 2
-1 % 2 // -1
1 % -2 // 1
```
+ 所以，为了得到负数的正确余数值，可以先使用绝对值函数。
```
// 错误的写法
function isOdd(n) {
  return n % 2 === 1;
}
isOdd(-5) // false
isOdd(-4) // false

// 正确的写法
function isOdd(n) {
  return Math.abs(n % 2) === 1;
}
isOdd(-5) // true
isOdd(-4) // false
```
+ 余数运算符还可以用于浮点数的运算。但是，由于浮点数不是精确的值，无法得到完全准确的结果。
```
6.5 % 2.1
// 0.19999999999999973
```
### 4、自增和自减运算符
自增和自减运算符，是一元运算符，只需要一个运算子。它们的作用是将运算子首先转为数值，然后加上1或者减去1。它们会修改原始变量。
```
var x = 1;
++x // 2
x // 2

--x // 1
x // 1
```
+ 上面代码的变量x自增后，返回2，再进行自减，返回1。这两种情况都会使得，原始变量x的值发生改变。
+ 运算之后，变量的值发生变化，这种效应叫做运算的副作用（side effect）。自增和自减运算符是仅有的两个具有副作用的运算符，其他运算符都不会改变变量的值。
+ 自增和自减运算符有一个需要注意的地方，就是放在变量之后，会先返回变量操作前的值，再进行自增/自减操作；放在变量之前，会先进行自增/自减操作，再返回变量操作后的值。
```
var x = 1;
var y = 1;

x++ // 1
x // 2

++y // 2
y // 2
```
