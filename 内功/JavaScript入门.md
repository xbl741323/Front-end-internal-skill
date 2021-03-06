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

#### 7、对象
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
+ JavaScript 中 call()、apply()、bind()都是用来重定义 this 这个对象的（修改函数内部this的指向）！
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

#### 一、概述
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

#### 二、算数运算符
运算符是处理数据的基本方法，用来从现有的值得到新的值。JavaScript 提供了多种运算符，覆盖了所有主要的运算。

##### 1、加法运算符
+ 加法运算符（+）是最常见的运算符，用来求两个数值的和。
+ 加法运算符是在运行时决定，到底是执行相加，还是执行连接。也就是说，运算子的不同，导致了不同的语法行为，这种现象称为“重载”（overload）。由于加法运算符存在重载，可能执行两种运算，使用的时候必须很小心。
```
3 + 4 + 5 // 12
'3' + 4 + 5 // "345"
3 + 4 + '5' // "75"
```
##### 对象的相加
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

##### 3、余数运算符
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
##### 4、自增和自减运算符
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
##### 5、数值运算符，负数值运算符
数值运算符（+）同样使用加号，但它是一元运算符（只需要一个操作数），而加法运算符是二元运算符（需要两个操作数）。
+ 数值运算符的作用在于可以将任何值转为数值（与Number函数的作用相同）。
```
+true // 1
+[] // 0
+{} // NaN  (NaN是数值类型)
```
+ 负数值运算符（-），也同样具有将一个值转为数值的功能，只不过得到的值正负相反。连用两个负数值运算符，等同于数值运算符。
```
var x = 1;
-x // -1
-(-x) // 1
```
+ 数值运算符号和负数值运算符，都会返回一个新的值，而不会改变原始变量的值。

#####  6、指数运算符
指数运算符完成指数运算，前一个运算子是底数，后一个运算子是指数。
```
2 ** 4 // 16
```
+ 注意，指数运算符是右结合，而不是左结合。即多个指数运算符连用时，先进行最右边的计算。
```
// 相当于 2 ** (3 ** 2)
2 ** 3 ** 2
// 512
```
##### 7、赋值运算符
赋值运算符（Assignment Operators）用于给变量赋值。最常见的赋值运算符，当然就是等号（=）。
```
// 将 1 赋值给变量 x
var x = 1;

// 将变量 y 的值赋值给变量 x
var x = y;
```
+ 赋值运算符还可以与其他运算符结合，形成变体。下面是与算术运算符的结合。
```
// 等同于 x = x + y
x += y

// 等同于 x = x - y
x -= y

// 等同于 x = x * y
x *= y

// 等同于 x = x / y
x /= y

// 等同于 x = x % y
x %= y

// 等同于 x = x ** y
x **= y
```
+ 下面是与位运算符的结合（关于位运算符，请见后文的介绍）。
```
// 等同于 x = x >> y
x >>= y

// 等同于 x = x << y
x <<= y

// 等同于 x = x >>> y
x >>>= y

// 等同于 x = x & y
x &= y

// 等同于 x = x | y
x |= y

// 等同于 x = x ^ y
x ^= y
```
+ 这些复合的赋值运算符，都是先进行指定运算，然后将得到值返回给左边的变量。

#### 三、比较运算

##### 1、概述
比较运算符用于比较两个值的大小，然后返回一个布尔值，表示是否满足指定的条件。

```
2 > 1 // true
```
+ 注意，比较运算符可以比较各种类型的值，不仅仅是数值。
+ JavaScript 一共提供了8个比较运算符：
+ > 大于运算符
+ < 小于运算符
+ <= 小于或等于运算符
+ >= 大于或等于运算符
+ == 相等运算符
+ === 严格相等运算符
+ != 不相等运算符
+ !== 严格不相等运算符

##### 2、非相等运算符：字符串的比较
+ 字符串按照字典顺序进行比较。
```
'cat' > 'dog' // false
'cat' > 'catalog' // false
```
```
'cat' > 'Cat' // true'
```
+ 上面代码中，小写的c的 Unicode 码点（99）大于大写的C的 Unicode 码点（67），所以返回true。
+ 由于所有字符都有 Unicode 码点，因此汉字也可以比较。
```
'大' > '小' // false
```
##### 3、非相等运算符：非字符串的比较
如果两个运算子之中，至少有一个不是字符串，需要分成以下两种情况。
+ （1）原始类型值
+ 如果两个运算子都是原始类型的值，则是先转成数值再比较，字符串和布尔值都会先转成数值，再进行比较。
```
5 > '4' // true
// 等同于 5 > Number('4')
// 即 5 > 4

true > false // true
// 等同于 Number(true) > Number(false)
// 即 1 > 0

2 > true // true
// 等同于 2 > Number(true)
// 即 2 > 1
```
+ 这里需要注意与NaN的比较。任何值（包括NaN本身）与NaN使用非相等运算符进行比较，返回的都是false。
```
1 > NaN // false
1 <= NaN // false
'1' > NaN // false
'1' <= NaN // false
NaN > NaN // false
NaN <= NaN // false
```
+ （2）对象
如果运算子是对象，会转为原始类型的值，再进行比较。
+ 对象转换成原始类型的值，算法是先调用valueOf方法；如果返回的还是对象，再接着调用toString方法。
```
var x = [2];
x > '11' // true
// 等同于 [2].valueOf().toString() > '11'
// 即 '2' > '11'

x.valueOf = function () { return '1' };
x > '11' // false
// 等同于 [2].valueOf() > '11'
// 即 '1' > '11'
```
+ 两个对象之间的比较也是如此。
```
[2] > [1] // true
// 等同于 [2].valueOf().toString() > [1].valueOf().toString()
// 即 '2' > '1'

[2] > [11] // true
// 等同于 [2].valueOf().toString() > [11].valueOf().toString()
// 即 '2' > '11'

{ x: 2 } >= { x: 1 } // true
// 等同于 { x: 2 }.valueOf().toString() >= { x: 1 }.valueOf().toString()
// 即 '[object Object]' >= '[object Object]'
```
##### 4、严格相等运算符
JavaScript 提供两种相等运算符：== 和 ===。
+ 简单说，它们的区别是相等运算符（==）比较两个值是否相等，严格相等运算符（===）比较它们是否为“同一个值”。如果两个值不是同一类型，严格相等运算符（===）直接返回false，而相等运算符（==）会将它们转换成同一个类型，再用严格相等运算符进行比较。
+ （1）不同类型的值
如果两个值的类型不同，直接返回false。
```
1 === "1" // false
true === "true" // false
```
+ （2）同一类的原始类型值
同一类型的原始类型的值（数值、字符串、布尔值）比较时，值相同就返回true，值不同就返回false。
```
1 === 0x1 // true
```
+ 需要注意的是，NaN与任何值都不相等（包括自身）。另外，正0等于负0。
```
NaN === NaN  // false
+0 === -0 // true
```
+ （3）复合类型值
两个复合类型（对象、数组、函数）的数据比较时，不是比较它们的值是否相等，而是比较它们是否指向同一个地址。
```
{} === {} // false
[] === [] // false
(function () {} === function () {}) // false
```
+ 上面代码分别比较两个空对象、两个空数组、两个空函数，结果都是不相等。原因是对于复合类型的值，严格相等运算比较的是，它们是否引用同一个内存地址，而运算符两边的空对象、空数组、空函数的值，都存放在不同的内存地址，结果当然是false。

+ 如果两个变量引用同一个对象，则它们相等。
```
var v1 = {};
var v2 = v1;
v1 === v2 // true
```
+ 注意，对于两个对象的比较，严格相等运算符比较的是地址，而大于或小于运算符比较的是值。
```
var obj1 = {};
var obj2 = {};

obj1 > obj2 // false
obj1 < obj2 // false
obj1 === obj2 // false
```
上面的三个比较，前两个比较的是值，最后一个比较的是地址，所以都返回false。

+ （4）undefined 和 null
+ undefined和null与自身严格相等。
```
undefined === undefined // true
null === null // true
```
+ 由于变量声明后默认值是undefined，因此两个只声明未赋值的变量是相等的。
```
var v1;
var v2;
v1 === v2 // true
```
##### 5、严格不相等运算符
严格相等运算符有一个对应的“严格不相等运算符”（!==），它的算法就是先求严格相等运算符的结果，然后返回相反值。
```
1 !== '1' // true
// 等同于
!(1 === '1')
```
+ 上面代码中，感叹号!是求出后面表达式的相反值。

##### 6、相等运算符
相等运算符用来比较相同类型的数据时，与严格相等运算符完全一样。
```
1 == 1.0
// 等同于
1 === 1.0
```
+ 比较不同类型的数据时，相等运算符会先将数据进行类型转换，然后再用严格相等运算符比较。下面分成几种情况，讨论不同类型的值互相比较的规则。
+ （1）原始类型值
+ 原始类型的值会转换成数值再进行比较。
```
1 == true // true
// 等同于 1 === Number(true)

0 == false // true
// 等同于 0 === Number(false)

2 == true // false
// 等同于 2 === Number(true)

2 == false // false
// 等同于 2 === Number(false)

'true' == true // false
// 等同于 Number('true') === Number(true)
// 等同于 NaN === 1

'' == 0 // true
// 等同于 Number('') === 0
// 等同于 0 === 0

'' == false  // true
// 等同于 Number('') === Number(false)
// 等同于 0 === 0

'1' == true  // true
// 等同于 Number('1') === Number(true)
// 等同于 1 === 1

'\n  123  \t' == 123 // true
// 因为字符串转为数字时，省略前置和后置的空格
```
+ （2）对象与原始类型值比较
+ 对象（这里指广义的对象，包括数组和函数）与原始类型的值比较时，对象转换成原始类型的值，再进行比较。
+ 具体来说，先调用对象的valueOf()方法，如果得到原始类型的值，就按照上一小节的规则，互相比较；如果得到的还是对象，则再调用toString()方法，得到字符串形式，再进行比较。
```
// 数组与数值的比较
[1] == 1 // true

// 数组与字符串的比较
[1] == '1' // true
[1, 2] == '1,2' // true

// 对象与布尔值的比较
[1] == true // true
[2] == true // false
```
+ 上面例子中，JavaScript 引擎会先对数组[1]调用数组的valueOf()方法，由于返回的还是一个数组，所以会接着调用数组的toString()方法，得到字符串形式，再按照上一小节的规则进行比较。
```
const obj = {
  valueOf: function () {
    console.log('执行 valueOf()');
    return obj;
  },
  toString: function () {
    console.log('执行 toString()');
    return 'foo';
  }
};

obj == 'foo'
// 执行 valueOf()
// 执行 toString()
// true
```
+ 上面例子中，obj是一个自定义了valueOf()和toString()方法的对象。这个对象与字符串'foo'进行比较时，会依次调用valueOf()和toString()方法，最后返回'foo'，所以比较结果是true。
+ （3）undefined 和 null
+ undefined和null只有与自身比较，或者互相比较时，才会返回true；与其他类型的值比较时，结果都为false。
```
ndefined == undefined // true
null == null // true
undefined == null // true

false == null // false
false == undefined // false

0 == null // false
0 == undefined // false
```
+ （4）相等运算符的缺点
+ 相等运算符隐藏的类型转换，会带来一些违反直觉的结果。
```
0 == ''             // true
0 == '0'            // true

2 == true           // false
2 == false          // false

false == 'false'    // false
false == '0'        // true

false == undefined  // false
false == null       // false
null == undefined   // true

' \t\r\n ' == 0     // true
```
+ 面这些表达式都不同于直觉，很容易出错。因此建议不要使用相等运算符（==），最好只使用严格相等运算符（===）。

##### 7、不相等运算符
相等运算符有一个对应的“不相等运算符”（!=），它的算法就是先求相等运算符的结果，然后返回相反值。
```
1 != '1' // false

// 等同于
!(1 == '1')
```

#### 四、布尔运算符

##### 1、概述
布尔运算符用于将表达式转为布尔值，一共包含四个运算符。
+ 取反运算符：!
+ 且运算符：&&
+ 或运算符：||
+ 三元运算符：?:

##### 2、取反运算符（!）
取反运算符是一个感叹号，用于将布尔值变为相反值，即true变成false，false变成true。
```
!true // false
!false // true
```
+ 对于非布尔值，取反运算符会将其转为布尔值。可以这样记忆，以下六个值取反后为true，其他值都为false。
```
!undefined // true
!null // true
!false // true
!0 // true
!NaN // true
!"" // true
```
+ 如果对一个值连续做两次取反运算，等于将其转为对应的布尔值，与Boolean函数的作用相同。这是一种常用的类型转换的写法。
```
!!x
// 等同于
Boolean(x)
```
##### 3、且运算符（&&）
且运算符（&&）往往用于多个表达式的求值。
+ 它的运算规则是：如果第一个运算子的布尔值为true，则返回第二个运算子的值（注意是值，不是布尔值）；如果第一个运算子的布尔值为false，则直接返回第一个运算子的值，且不再对第二个运算子求值。
```
't' && '' // ""
't' && 'f' // "f"
't' && (1 + 2) // 3
'' && 'f' // ""
'' && '' // ""

var x = 1;
(1 - 1) && ( x += 1) // 0
x // 1
```
+ 这种跳过第二个运算子的机制，被称为“短路”。有些程序员喜欢用它取代if结构，比如下面是一段if结构的代码，就可以用且运算符改写。
```
if (i) {
  doSomething();
}
// 等价于
i && doSomething();
```
+ 上面代码的两种写法是等价的，但是后一种不容易看出目的，也不容易除错，建议谨慎使用。

##### 4、或运算符（||）
或运算符（||）也用于多个表达式的求值。它的运算规则是：如果第一个运算子的布尔值为true，则返回第一个运算子的值，且不再对第二个运算子求值；如果第一个运算子的布尔值为false，则返回第二个运算子的值。
+ 短路规则对这个运算符也适用。
```
var x = 1;
true || (x = 2) // true
x // 1
```
##### 5、三元条件运算符（?:）
三元条件运算符由问号（?）和冒号（:）组成，分隔三个表达式。它是 JavaScript 语言唯一一个需要三个运算子的运算符。如果第一个表达式的布尔值为true，则返回第二个表达式的值，否则返回第三个表达式的值。
```
't' ? 'hello' : 'world' // "hello"
0 ? 'hello' : 'world' // "world"
```

#### 五、二进制位运算符（此处暂不做记载）

#### 六、其他运算符，运算顺序

###### 1、void 运算符
void运算符的作用是执行一个表达式，然后不返回任何值，或者说返回undefined。
```
void 0 // undefined
void(0) // undefined
```
+ 这个运算符的主要用途是浏览器的书签工具（Bookmarklet），以及在超级链接中插入代码防止网页跳转,请看下面的代码。
```
<a href="javascript: void(f())">文字</a>
<a href="javascript: void(document.form.submit())">
  提交
</a>
```

##### 2、逗号运算符
逗号运算符用于对两个表达式求值，并返回后一个表达式的值。
```
'a', 'b' // "b"

var x = 0;
var y = (x++, 10);
x // 1
y // 10
```
##### 3、运算顺序
JavaScript 各种运算符的优先级别（Operator Precedence）是不一样的。优先级高的运算符先执行，优先级低的运算符后执行。
+ 根据语言规格，运算符的优先级从高到低依次为：小于等于（<=)、严格相等（===）、或（||）、三元（?:）、等号（=）。
+ 圆括号（()）可以用来提高运算的优先级，因为它的优先级是最高的，即圆括号中的表达式会第一个运算。

##### 4、左结合与右结合
```
// 方式一
(a OP b) OP c
// 方式二
a OP (b OP c)
```
+ 上面的两种方式，得到的计算结果往往是不一样的。方式一是将左侧两个运算数结合在一起，采用这种解释方式的运算符，称为“左结合”（left-to-right associativity）运算符；方式二是将右侧两个运算数结合在一起，这样的运算符称为“右结合”运算符（right-to-left associativity）。

+ JavaScript 语言的大多数运算符是“左结合”，请看下面加法运算符的例子。
```
x + y + z
// 引擎解释如下
(x + y) + z
```
+ 注意：指数运算符是右结合。
```
2 ** 3 ** 2
// 相当于 2 ** (3 ** 2)
// 512
```

### 四、语法专题

#### 一、数据类型的转换

##### 1、概述
JavaScript 是一种动态类型语言，变量没有类型限制，可以随时赋予任意值。
+ 强制转换主要指使用Number()、String()和Boolean()三个函数，手动将各种类型的值，分别转换成数字、字符串或者布尔值。

##### 2、Number()
使用Number函数，可以将任意类型的值转化成数值。
+ （1）原始类型值
```
// 数值：转换后还是原来的值
Number(324) // 324

// 字符串：如果可以被解析为数值，则转换为相应的数值
Number('324') // 324

// 字符串：如果不可以被解析为数值，返回 NaN
Number('324abc') // NaN

// 空字符串转为0
Number('') // 0

// 布尔值：true 转成 1，false 转成 0
Number(true) // 1
Number(false) // 0

// undefined：转成 NaN
Number(undefined) // NaN

// null：转成0
Number(null) // 0
```
+ Number函数将字符串转为数值，要比parseInt函数严格很多。基本上，只要有一个字符无法转成数值，整个字符串就会被转为NaN。
```
parseInt('42 cats') // 42
Number('42 cats') // NaN
```
+ （2）对象 
简单的规则是，Number方法的参数是对象时，将返回NaN，除非是包含单个数值的数组。
```
Number({a: 1}) // NaN
Number([1, 2, 3]) // NaN
Number([5]) // 5
```
+ 之所以会这样，是因为Number背后的转换规则比较复杂。
+ 第一步，调用对象自身的valueOf方法。如果返回原始类型的值，则直接对该值使用Number函数，不再进行后续步骤。
+ 第二步，如果valueOf方法返回的还是对象，则改为调用对象自身的toString方法。如果toString方法返回原始类型的值，则对该值使用Number函数，不再进行后续步骤。
+ 第三步，如果toString方法返回的是对象，就报错。
+ 请看下面的例子。
```
var obj = {x: 1};
Number(obj) // NaN

// 等同于
if (typeof obj.valueOf() === 'object') {
  Number(obj.toString());
} else {
  Number(obj.valueOf());
}
```
##### 3、String()
String函数可以将任意类型的值转化成字符串，转换规则如下。
+（1）原始类型值
+ 数值：转为相应的字符串。
+ 字符串：转换后还是原来的值。
+ 布尔值：true转为字符串"true"，false转为字符串"false"。
+ undefined：转为字符串"undefined"。
+ null：转为字符串"null"。
```
String(123) // "123"
String('abc') // "abc"
String(true) // "true"
String(undefined) // "undefined"
String(null) // "null"
```
+（2）对象
String方法的参数如果是对象，返回一个类型字符串；如果是数组，返回该数组的字符串形式。
```
String({a: 1}) // "[object Object]"
String([1, 2, 3]) // "1,2,3"
```
+ String方法背后的转换规则，与Number方法基本相同，只是互换了valueOf方法和toString方法的执行顺序。
+ 第一步，先调用对象自身的toString方法。如果返回原始类型的值，则对该值使用String函数，不再进行以下步骤。
+ 第二步，如果toString方法返回的是对象，再调用原对象的valueOf方法。如果valueOf方法返回原始类型的值，则对该值使用String函数，不再进行以下步骤。
+ 第三步，如果valueOf方法返回的是对象，就报错。

##### 4、Boolean()
Boolean()函数可以将任意类型的值转为布尔值。它的转换规则相对简单：除了以下五个值的转换结果为false，其他的值全部为true。
```
Boolean(undefined) // false
Boolean(null) // false
Boolean(0) // false
Boolean(NaN) // false
Boolean('') // false
```
+ 当然，true和false这两个布尔值不会发生变化。
```
Boolean(true) // true
Boolean(false) // false
```
+ 注意，所有对象（包括空对象）的转换结果都是true，甚至连false对应的布尔对象new Boolean(false)也是true
```
Boolean({}) // true
Boolean([]) // true
Boolean(new Boolean(false)) // true
```
##### 5、自动转换
下面介绍自动转换，它是以强制转换为基础的。遇到以下三种情况时，JavaScript 会自动转换数据类型，即转换是自动完成的，用户不可见。
+ 第一种情况，不同类型的数据互相运算。
```
123 + 'abc' // "123abc"
```
+ 第二种情况，对非布尔值类型的数据求布尔值。
```
if ('abc') {
  console.log('hello')
}  // "hello"
```
+ 第三种情况，对非数值类型的值使用一元运算符（即+和-）。
```
+ {foo: 'bar'} // NaN
- [1, 2, 3] // NaN
```
+ 由于自动转换具有不确定性，而且不易除错，建议在预期为布尔值、数值、字符串的地方，全部使用Boolean()、Number()和String()函数进行显式转换。

##### 5.1、自动转换为布尔值
JavaScript 遇到预期为布尔值的地方（比如if语句的条件部分），就会将非布尔值的参数自动转换为布尔值。系统内部会自动调用Boolean()函数。
+ 因此除了以下五个值，其他都是自动转为true。
+ undefined
+ null
+ +0或-0
+ NaN
+ ''（空字符串）

##### 5.2、自动转换为字符串
JavaScript 遇到预期为字符串的地方，就会将非字符串的值自动转为字符串。具体规则是，先将复合类型的值转为原始类型的值，再将原始类型的值转为字符串。
+ 字符串的自动转换，主要发生在字符串的加法运算时。当一个值为字符串，另一个值为非字符串，则后者转为字符串。

##### 5.3、自动转换为布尔值
JavaScript 遇到预期为数值的地方，就会将参数值自动转换为数值。系统内部会自动调用Number()函数。
+ 除了加法运算符（+）有可能把运算子转为字符串，其他运算符都会把运算子自动转成数值。
```
'5' - '2' // 3
'5' * '2' // 10
true - 1  // 0
false - 1 // -1
'1' - 1   // 0
'5' * []    // 0
false / '5' // 0
'abc' - 1   // NaN
null + 1 // 1
undefined + 1 // NaN
```
+ 注意：null转为数值时为0，而undefined转为数值时为NaN。
+ 一元运算符也会把运算子转成数值。
```
+'abc' // NaN
-'abc' // NaN
+true // 1
-false // 0
```

#### 二、错误处理机制
##### 1、Error 实例对象
JavaScript 解析或运行时，一旦发生错误，引擎就会抛出一个错误对象。JavaScript 原生提供Error构造函数，所有抛出的错误都是这个构造函数的实例。
```
var err = new Error('出错了');
err.message // "出错了"
```
##### 2、throw 语句
throw语句的作用是手动中断程序执行，抛出一个错误。
```
var x = -1;

if (x <= 0) {
  throw new Error('x 必须为正数');
}
// Uncaught Error: x 必须为正数
```
##### 3、try...catch 结构
一旦发生错误，程序就中止执行了。JavaScript 提供了try...catch结构，允许对错误进行处理，选择是否往下执行。
```
try {
  throw new Error('出错了!');
} catch (e) {
  console.log(e.name + ": " + e.message);
  console.log(e.stack);
}
// Error: 出错了!
//   at <anonymous>:3:9
//   ...
```
##### 4、finally 代码块
try...catch结构允许在最后添加一个finally代码块，表示不管是否出现错误，都必需在最后运行的语句。
```
function cleansUp() {
  try {
    throw new Error('出错了……');
    console.log('此行不会执行');
  } finally {
    console.log('完成清理工作');
  }
}

cleansUp()
// 完成清理工作
// Uncaught Error: 出错了……
//    at cleansUp (<anonymous>:3:11)
//    at <anonymous>:10:1
```

#### 三、编程风格
##### 1、概述
“编程风格”（programming style）指的是编写代码的样式规则。不同的程序员，往往有不同的编程风格。
+ 编译器的规范叫做“语法规则”（grammar），这是程序员必须遵守的；而编译器忽略的部分，就叫“编程风格”（programming style），这是程序员可以自由选择的。
+ 这种说法不完全正确，程序员固然可以自由选择编程风格，但是好的编程风格有助于写出质量更高、错误更少、更易于维护的程序。
+ 必须牢记的一点是，如果你选定了一种“编程风格”，就应该坚持遵守，切忌多种风格混用。如果你加入他人的项目，就应该遵守现有的风格。

##### 2、缩进
行首的空格和 Tab 键，都可以产生代码缩进效果（indent）。
+ Tab 键可以节省击键次数，但不同的文本编辑器对 Tab 的显示不尽相同，有的显示四个空格，有的显示两个空格，所以有人觉得，空格键可以使得显示效果更统一。
+ 无论你选择哪一种方法，都是可以接受的，要做的就是始终坚持这一种选择。不要一会使用 Tab 键，一会使用空格键。

##### 3、区块
+ 如果循环和判断的代码体只有一行，JavaScript 允许该区块（block）省略大括号。
```
if (a)
  b();
  c();
```
+ 上面代码的原意可能是下面这样。
```
if (a) {
  b();
  c();
}
```
+ 但是，实际效果却是下面这样。
```
if (a) {
  b();
}
  c();
```
+ 因此，建议总是使用大括号表示区块。

##### 4、圆括号
圆括号（parentheses）在 JavaScript 中有两种作用，一种表示函数的调用，另一种表示表达式的组合（grouping）。
```
// 圆括号表示函数的调用
console.log('abc');

// 圆括号表示表达式的组合
(1 + 2) * 3
```
##### 5、行尾的分号
分号表示一条语句的结束。JavaScript 允许省略行尾的分号。事实上，确实有一些开发者行尾从来不写分号，建议还是不要省略这个分号。

##### 6、全局变量
+ JavaScript 最大的语法缺点，可能就是全局变量对于任何一个代码块，都是可读可写。这对代码的模块化和重复使用，非常不利。
+ 因此，建议避免使用全局变量。如果不得不使用，可以考虑用大写字母表示变量名，这样更容易看出这是全局变量，比如UPPER_CASE。

##### 7、变量声明
JavaScript 会自动将变量声明“提升”（hoist）到代码块（block）的头部。
+ 所有函数都应该在使用之前定义。函数内部的变量声明，都应该放在函数的头部。

##### 8、with 语句
with可以减少代码的书写，但是会造成混淆，因此，不要使用with语句。

##### 9、相等和严格相等
JavaScript 有两个表示相等的运算符：“相等”（==）和“严格相等”（===）。
+ 相等运算符会自动转换变量类型，造成很多意想不到的情况。
```
0 == ''// true
1 == true // true
2 == true // false
0 == '0' // true
false == 'false' // false
false == '0' // true
' \t\r\n ' == 0 // true
```
+ 因此，建议不要使用相等运算符（==），只使用严格相等运算符（===）。

##### 10、自增和自减运算符
自增（++）和自减（--）运算符，放在变量的前面或后面，返回的值不一样，很容易发生错误。事实上，所有的++运算符都可以用+= 1代替。
```
++x
// 等同于
x += 1;
```
+ 改用+= 1，代码变得更清晰了。建议自增（++）和自减（--）运算符尽量使用+=和-=代替。

##### 11、switch...case 结构
switch...case结构要求，在每一个case的最后一行必须是break语句，否则会接着运行下一个case。

#### 四、console 对象与控制台
##### 1、console 对象
console对象是 JavaScript 的原生对象，它有点像 Unix 系统的标准输出stdout和标准错误stderr，可以输出各种信息到控制台，并且还提供了很多有用的辅助方法。
+ console的常见用途有两个：
+ 调试程序，显示网页代码运行时的错误信息。
+ 提供了一个命令行接口，用来与网页代码互动。

console对象的浏览器实现，包含在浏览器自带的开发工具之中。以 Chrome 浏览器的“开发者工具”（Developer Tools）为例，可以使用下面三种方法的打开它。
```
按 F12 或者Control + Shift + i（PC）/ Command + Option + i（Mac）。
浏览器菜单选择“工具/开发者工具”。
在一个页面元素上，打开右键菜单，选择其中的“Inspect Element”。
打开开发者工具以后，顶端有多个面板。
Elements：查看网页的 HTML 源码和 CSS 代码。
Resources：查看网页加载的各种资源文件（比如代码文件、字体文件 CSS 文件等），以及在硬盘上创建的各种内容
（比如本地缓存、Cookie、Local Storage等）。
Network：查看网页的 HTTP 通信情况。
Sources：查看网页加载的脚本源码。
Timeline：查看各种网页行为随时间变化的情况。
Performance：查看网页的性能情况，比如 CPU 和内存消耗。
```
+ Console：用来运行 JavaScript 命令。
+ 这些面板都有各自的用途，以下只介绍Console面板（又称为控制台）。
+ Console面板基本上就是一个命令行窗口，你可以在提示符下，键入各种命令。

##### 2、console 对象的静态方法
+ console.log方法用于在控制台输出信息。它可以接受一个或多个参数，将它们连接起来输出。
+ console.info是console.log方法的别名，用法完全一样。只不过console.info方法会在输出信息的前面，加上一个蓝色图标。
+ console.debug方法与console.log方法类似，会在控制台输出调试信息。但是，默认情况下，console.debug输出的信息不会显示，只有在打开显示级别在verbose的情况下，才会显示。
+ console对象的所有方法，都可以被覆盖。因此，可以按照自己的需要，定义console.log方法。
```
['log', 'info', 'warn', 'error'].forEach(function(method) {
  console[method] = console[method].bind(
    console,
    new Date().toISOString()
  );
});

console.log("出错了！");
// 2014-05-18T09:00.000Z 出错了！
```
##### 3、console.warn()，console.error()
warn方法和error方法也是在控制台输出信息，它们与log方法的不同之处在于:
+ warn方法输出信息时，在最前面加一个黄色三角，表示警告；
+ error方法输出信息时，在最前面加一个红色的叉，表示出错。同时，还会高亮显示输出文字和错误发生的堆栈。其他方面都一样。
```
console.error('Error: %s (%i)', 'Server is not responding', 500)
// Error: Server is not responding (500)
console.warn('Warning! Too few nodes (%d)', document.childNodes.length)
// Warning! Too few nodes (1)
```
##### 4、console.table()
对于某些复合类型的数据，console.table方法可以将其转为表格显示。
```
var languages = [
  { name: "JavaScript", fileExtension: ".js" },
  { name: "TypeScript", fileExtension: ".ts" },
  { name: "CoffeeScript", fileExtension: ".coffee" }
];

console.table(languages);
```
+ 上面代码的language变量，转为表格显示如下。
```
(index)	name	fileExtension
0	"JavaScript"	".js"
1	"TypeScript"	".ts"
2	"CoffeeScript"	".coffee"
```
##### 5、console.count()
count方法用于计数，输出它被调用了多少次。
```
function greet(user) {
  console.count();
  return 'hi ' + user;
}

greet('bob')
//  : 1
// "hi bob"

greet('alice')
//  : 2
// "hi alice"

greet('bob')
//  : 3
// "hi bob"
```
+ 该方法可以接受一个字符串作为参数，作为标签，对执行次数进行分类。
```
function greet(user) {
  console.count(user);
  return "hi " + user;
}

greet('bob')
// bob: 1
// "hi bob"

greet('alice')
// alice: 1
// "hi alice"

greet('bob')
// bob: 2
// "hi bob"
```
+ 上面代码根据参数的不同，显示bob执行了两次，alice执行了一次。
##### 6、console.dir()，console.dirxml()
+ dir方法用来对一个对象进行检查（inspect），并以易于阅读和打印的格式显示。
```
console.log({f1: 'foo', f2: 'bar'})
// Object {f1: "foo", f2: "bar"}

console.dir({f1: 'foo', f2: 'bar'})
// Object
//   f1: "foo"
//   f2: "bar"
//   __proto__: Object
```
+ 上面代码显示dir方法的输出结果，比log方法更易读，信息也更丰富。
+ 该方法对于输出 DOM 对象非常有用，因为会显示 DOM 对象的所有属性。
+ Node 环境之中，还可以指定以代码高亮的形式输出。
```
console.dir(obj, {colors: true})
```
+ dirxml方法主要用于以目录树的形式，显示 DOM 节点
```
console.dirxml(document.body)
```
+ 如果参数不是 DOM 节点，而是普通的 JavaScript 对象，console.dirxml等同于console.dir。
```
console.dirxml([1, 2, 3])
// 等同于
console.dir([1, 2, 3])
```
##### 7、console.assert()
console.assert方法主要用于程序运行过程中，进行条件判断，如果不满足条件，就显示一个错误，但不会中断程序执行。这样就相当于提示用户，内部状态不正确。
+ 它接受两个参数，第一个参数是表达式，第二个参数是字符串。只有当第一个参数为false，才会提示有错误，在控制台输出第二个参数，否则不会有任何结果。
```
onsole.assert(false, '判断条件不成立')
// Assertion failed: 判断条件不成立

// 相当于
try {
  if (!false) {
    throw new Error('判断条件不成立');
  }
} catch(e) {
  console.error(e);
}
```
下面是一个例子，判断子节点的个数是否大于等于500。
```
console.assert(list.childNodes.length < 500, '节点个数大于等于500')
```
+ 上面代码中，如果符合条件的节点小于500个，不会有任何输出；只有大于等于500时，才会在控制台提示错误，并且显示指定文本。

##### 8、console.time()，console.timeEnd()
这两个方法用于计时，可以算出一个操作所花费的准确时间。
```
console.time('Array initialize');

var array= new Array(1000000);
for (var i = array.length - 1; i >= 0; i--) {
  array[i] = new Object();
};

console.timeEnd('Array initialize');
// Array initialize: 1914.481ms
```
+ time方法表示计时开始，timeEnd方法表示计时结束。它们的参数是计时器的名称。调用timeEnd方法之后，控制台会显示“计时器名称: 所耗费的时间”。

##### 9、console.group()，console.groupEnd()，console.groupCollapsed()
console.group和console.groupEnd这两个方法用于将显示的信息分组。它只在输出大量信息时有用，分在一组的信息，可以用鼠标折叠/展开。
```
console.group('一级分组');
console.log('一级分组的内容');

console.group('二级分组');
console.log('二级分组的内容');

console.groupEnd(); // 二级分组结束
console.groupEnd(); // 一级分组结束
```
+ console.groupCollapsed方法与console.group方法很类似，唯一的区别是该组的内容，在第一次显示时是收起的（collapsed），而不是展开的。
```
console.groupCollapsed('Fetching Data');

console.log('Request Sent');
console.error('Error: Server not responding (500)');

console.groupEnd();
```
+ 上面代码只显示一行”Fetching Data“，点击后才会展开，显示其中包含的两行。

##### 10、console.trace()，console.clear()
+ console.trace方法显示当前执行的代码在堆栈中的调用路径。
+ console.clear方法用于清除当前控制台的所有输出，将光标回置到第一行。如果用户选中了控制台的“Preserve log”选项，console.clear方法将不起作用。

##### 11、debugger 语句
debugger语句主要用于除错，作用是设置断点。如果有正在运行的除错工具，程序运行到debugger语句时会自动停下。
+ 如果没有除错工具，debugger语句不会产生任何结果，JavaScript 引擎自动跳过这一句。
+ Chrome 浏览器中，当代码运行到debugger语句时，就会暂停运行，自动打开脚本源码界面。
```
for(var i = 0; i < 5; i++){
  console.log(i);
  if (i === 2) debugger;
}
```
上面代码打印出0，1，2以后，就会暂停，自动打开源码界面，等待进一步处理。

### 五、标准库

#### 一、Object 对象
##### 1、概述
JavaScript 原生提供Object对象（注意起首的O是大写），本章介绍该对象原生的各种方法。
+ JavaScript 的所有其他对象都继承自Object对象，即那些对象都是Object的实例。
+ （1）Object对象本身的方法
所谓“本身的方法”就是直接定义在Object对象的方法。
```
Object.print = function (o) { console.log(o) };
```
+ （2）Object的实例方法
所谓实例方法就是定义在Object原型对象Object.prototype上的方法。它可以被Object实例直接使用。
```
Object.prototype.print = function () {
  console.log(this);
};

var obj = new Object();
obj.print() // Object
```
+ 以下先介绍Object作为函数的用法，然后再介绍Object对象的原生方法，分成对象自身的方法（又称为“静态方法”）和实例方法两部分。

##### 2、Object()
Object本身是一个函数，可以当作工具方法使用，将任意值转为对象。这个方法常用于保证某个值一定是对象。
+ 如果参数为空（或者为undefined和null），Object()返回一个空对象。
```
var obj = Object();
// 等同于
var obj = Object(undefined);
var obj = Object(null);
obj instanceof Object // true
```
+ instanceof运算符用来验证，一个对象是否为指定的构造函数的实例。obj instanceof Object返回true，就表示obj对象是Object的实例。
+ 如果参数是原始类型的值，Object方法将其转为对应的包装对象的实例。
```
var obj = Object(1);
obj instanceof Object // true
obj instanceof Number // true

var obj = Object('foo');
obj instanceof Object // true
obj instanceof String // true

var obj = Object(true);
obj instanceof Object // true
obj instanceof Boolean // true
```
##### 3、Object 构造函数
Object不仅可以当作工具函数使用，还可以当作构造函数使用，即前面可以使用new命令。
+ Object构造函数的首要用途，是直接通过它来生成新对象。
```
var obj = new Object();
```
+ 注意，通过var obj = new Object()的写法生成新对象，与字面量的写法var obj = {}是等价的。或者说，后者只是前者的一种简便写法。
+ Object构造函数的用法与工具方法很相似，几乎一模一样。使用时，可以接受一个参数，如果该参数是一个对象，则直接返回这个对象；如果是一个原始类型的值，则返回该值对应的包装对象。
```
var o1 = {a: 1};
var o2 = new Object(o1);
o1 === o2 // true

var obj = new Object(123);
obj instanceof Number // true
```
##### 4、Object 的静态方法
+ Object.keys()，Object.getOwnPropertyNames() 
+ Object.keys方法的参数是一个对象，返回一个数组。该数组的成员都是该对象自身的（而不是继承的）所有属性名。
```
var obj = {
  p1: 123,
  p2: 456
};

Object.keys(obj) // ["p1", "p2"]
```
+ Object.getOwnPropertyNames方法与Object.keys类似，也是接受一个对象作为参数，返回一个数组，包含了该对象自身的所有属性名。
```
var obj = {
  p1: 123,
  p2: 456
};
Object.getOwnPropertyNames(obj) // ["p1", "p2"]
```
+ 对于一般的对象来说，Object.keys()和Object.getOwnPropertyNames()返回的结果是一样的。只有涉及不可枚举属性时，才会有不一样的结果。Object.keys方法只返回可枚举的属性，Object.getOwnPropertyNames方法还返回不可枚举的属性名。
```
var a = ['Hello', 'World'];

Object.keys(a) // ["0", "1"]
Object.getOwnPropertyNames(a) // ["0", "1", "length"]
```
+ 上面代码中，数组的length属性是不可枚举的属性，所以只出现在Object.getOwnPropertyNames方法的返回结果中。
+ 由于 JavaScript 没有提供计算对象属性个数的方法，所以可以用这两个方法代替。
```
var obj = {
  p1: 123,
  p2: 456
};

Object.keys(obj).length // 2
Object.getOwnPropertyNames(obj).length // 2
```
##### 5、Object 的实例方法
+ 除了静态方法，还有不少方法定义在Object.prototype对象。它们称为实例方法，所有Object的实例对象都继承了这些方法。
Object实例对象的方法，主要有以下六个:
```
Object.prototype.valueOf()：返回当前对象对应的值。
Object.prototype.toString()：返回当前对象对应的字符串形式。
Object.prototype.toLocaleString()：返回当前对象对应的本地字符串形式。
Object.prototype.hasOwnProperty()：判断某个属性是否为当前对象自身的属性，还是继承自原型对象的属性。
Object.prototype.isPrototypeOf()：判断当前对象是否为另一个对象的原型。
Object.prototype.propertyIsEnumerable()：判断某个属性是否可枚举。
```
#### 二、属性描述对象（暂不记录）

#### 三、Array 对象
##### 1、构造函数
Array是 JavaScript 的原生对象，同时也是一个构造函数，可以用它生成新的数组。
```
var arr = new Array(2);
arr.length // 2
arr // [ empty x 2 ]
```
+ 上面代码中，Array()构造函数的参数2，表示生成一个两个成员的数组，每个位置都是空值。
+ 如果没有使用new关键字，运行结果也是一样的。
```
var arr = Array(2);
// 等同于
var arr = new Array(2);
```
+ 考虑到语义性，以及与其他构造函数用法保持一致，建议总是加上new。
```
var arr = new Array(2);
arr.length // 2
arr // [ empty x 2 ]
```
+ Array()构造函数有一个很大的缺陷，不同的参数个数会导致不一致的行为。
```
/ 无参数时，返回一个空数组
new Array() // []

// 单个正整数参数，表示返回的新数组的长度
new Array(1) // [ empty ]
new Array(2) // [ empty x 2 ]

// 非正整数的数值作为参数，会报错
new Array(3.2) // RangeError: Invalid array length
new Array(-3) // RangeError: Invalid array length

// 单个非数值（比如字符串、布尔值、对象等）作为参数，
// 则该参数是返回的新数组的成员
new Array('abc') // ['abc']
new Array([1]) // [Array[1]]

// 多参数时，所有参数都是返回的新数组的成员
new Array(1, 2) // [1, 2]
new Array('a', 'b', 'c') // ['a', 'b', 'c']
```
+ 可以看到，Array()作为构造函数，行为很不一致。因此，不建议使用它生成新数组，直接使用数组字面量是更好的做法。
```
// bad
var arr = new Array(1, 2);
// good
var arr = [1, 2];
```
+ 注意，如果参数是一个正整数，返回数组的成员都是空位。虽然读取的时候返回undefined，但实际上该位置没有任何值。虽然这时可以读取到length属性，但是取不到键名。
```
var a = new Array(3);
var b = [undefined, undefined, undefined];

a.length // 3
b.length // 3

a[0] // undefined
b[0] // undefined

0 in a // false
0 in b // true
```
##### 2、静态方法
+ Array.isArray方法返回一个布尔值，表示参数是否为数组。它可以弥补typeof运算符的不足。
```
var arr = [1, 2, 3];
typeof arr // "object"
Array.isArray(arr) // true
```
+ 上面代码中，typeof运算符只能显示数组的类型是Object，而Array.isArray方法可以识别数组。

##### 3、实例方法
3.1、valueOf()，toString()
+ valueOf方法是一个所有对象都拥有的方法，表示对该对象求值。不同对象的valueOf方法不尽一致，数组的valueOf方法返回数组本身。
```
var arr = [1, 2, 3];
arr.valueOf() // [1, 2, 3]
```
+ toString方法也是对象的通用方法，数组的toString方法返回数组的字符串形式。
```
var arr = [1, 2, 3];
arr.toString() // "1,2,3"

var arr = [1, 2, 3, [4, 5, 6]];
arr.toString() // "1,2,3,4,5,6"
```

3.2、push()，pop()
+ push方法用于在数组的末端添加一个或多个元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组。
```
var arr = [];
arr.push(1) // 1
arr.push('a') // 2
arr.push(true, {}) // 4
arr // [1, 'a', true, {}]
```
+ pop方法用于删除数组的最后一个元素，并返回该元素。注意，该方法会改变原数组。
```
var arr = ['a', 'b', 'c'];
arr.pop() // 'c'
arr // ['a', 'b']
```
+ push和pop结合使用，就构成了“后进先出”的栈结构（stack）。
```
var arr = [];
arr.push(1, 2);
arr.push(3);
arr.pop();
arr // [1, 2]
```

3.3、shift()，unshift() 
+ shift()方法用于删除数组的第一个元素，并返回该元素。注意，该方法会改变原数组。
```
var a = ['a', 'b', 'c'];
a.shift() // 'a'
a // ['b', 'c']
```
+ push()和shift()结合使用，就构成了“先进先出”的队列结构（queue）
+ unshift()方法用于在数组的第一个位置添加元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组。
```
var a = ['a', 'b', 'c'];
a.unshift('x'); // 4
a // ['x', 'a', 'b', 'c']
```
+ unshift()方法可以接受多个参数，这些参数都会添加到目标数组头部。
```
var arr = [ 'c', 'd' ];
arr.unshift('a', 'b') // 4
arr // [ 'a', 'b', 'c', 'd' ]
```

3.4、join()
+ join()方法以指定参数作为分隔符，将所有数组成员连接为一个字符串返回。如果不提供参数，默认用逗号分隔。
```
var a = [1, 2, 3, 4];
a.join(' ') // '1 2 3 4'
a.join(' | ') // "1 | 2 | 3 | 4"
a.join() // "1,2,3,4"
```
+ 如果数组成员是undefined或null或空位，会被转成空字符串。
```
[undefined, null].join('#')
// '#'
['a',, 'b'].join('-')
// 'a--b'
```
+ 通过call方法，这个方法也可以用于字符串或类似数组的对象。
```
Array.prototype.join.call('hello', '-')
// "h-e-l-l-o"

var obj = { 0: 'a', 1: 'b', length: 2 };
Array.prototype.join.call(obj, '-')
// 'a-b'
```

3.5、concat()
+ concat方法用于多个数组的合并。它将新数组的成员，添加到原数组成员的后部，然后返回一个新数组，原数组不变。
```
'hello'].concat(['world'])
// ["hello", "world"]

['hello'].concat(['world'], ['!'])
// ["hello", "world", "!"]

[].concat({a: 1}, {b: 2})
// [{ a: 1 }, { b: 2 }]

[2].concat({a: 1})
// [2, {a: 1}]
```
+ 除了数组作为参数，concat也接受其他类型的值作为参数，添加到目标数组尾部。
```
[1, 2, 3].concat(4, 5, 6)
// [1, 2, 3, 4, 5, 6]
```
+ 如果数组成员包括对象，concat方法返回当前数组的一个浅拷贝。所谓“浅拷贝”，指的是新数组拷贝的是对象的引用。
+ 一般讨论到浅拷贝和深拷贝的都是针对引用类型的，像Object和Array这样的复杂类型，
+ 浅拷贝后的值来源于一个内存，新值变化原值也变化（如果是拷贝对象是对象和数组，（通过concat()或silce()进行拷贝）第一层值修改，原值不会变化），深拷贝后的值内存不一样，互相不影响。

3.6、reverse()
+ reverse方法用于颠倒排列数组元素，返回改变后的数组。注意，该方法将改变原数组。
```
var a = ['a', 'b', 'c'];
a.reverse() // ["c", "b", "a"]
a // ["c", "b", "a"]
```

3.7、slice()
+ slice()方法用于提取目标数组的一部分，返回一个新数组，原数组不变。
```
arr.slice(start, end);
```
+ 它的第一个参数为起始位置（从0开始，会包括在返回的新数组之中），第二个参数为终止位置（但该位置的元素本身不包括在内）。如果省略第二个参数，则一直返回到原数组的最后一个成员。
```
var a = ['a', 'b', 'c'];
a.slice(0) // ["a", "b", "c"]
a.slice(1) // ["b", "c"]
a.slice(1, 2) // ["b"]
a.slice(2, 6) // ["c"]
a.slice() // ["a", "b", "c"]
```
+ 上面代码中，最后一个例子slice()没有参数，实际上等于返回一个原数组的拷贝。
+ 如果slice()方法的参数是负数，则表示倒数计算的位置（第一个参数不会包括在返回的新数组之中，第二个会）。
```
var a = ['a', 'b', 'c'];
a.slice(-2) // ["b", "c"]
a.slice(-2, -1) // ["b"]
```
+ slice()方法的一个重要应用，是将类似数组的对象转为真正的数组。
```
Array.prototype.slice.call({ 0: 'a', 1: 'b', length: 2 })
// ['a', 'b']

Array.prototype.slice.call(document.querySelectorAll("div"));
Array.prototype.slice.call(arguments);
```
+ 上面代码的参数都不是数组，但是通过call方法，在它们上面调用slice()方法，就可以把它们转为真正的数组。

#### 四、包装对象

##### 1、定义
对象是 JavaScript 语言最主要的数据类型，三种原始类型的值——数值、字符串、布尔值——在一定条件下，也会自动转为对象，也就是原始类型的“包装对象”（wrapper）。
+ 所谓“包装对象”，指的是与数值、字符串、布尔值分别相对应的Number、String、Boolean三个原生对象。这三个原生对象可以把原始类型的值变成（包装成）对象
```
var v1 = new Number(123);
var v2 = new String('abc');
var v3 = new Boolean(true);

typeof v1 // "object"
typeof v2 // "object"
typeof v3 // "object"

v1 === 123 // false
v2 === 'abc' // false
v3 === true // false
```
+ Number、String和Boolean这三个原生对象，如果不作为构造函数调用（即调用时不加new），而是作为普通函数调用，常常用于将任意类型的值转为数值、字符串和布尔值。
```
// 字符串转为数值
Number('123') // 123

// 数值转为字符串
String(123) // "123"

// 数值转为布尔值
Boolean(123) // true
```
##### 2、实例方法
三种包装对象各自提供了许多实例方法，详见后文。这里介绍两种它们共同具有、从Object对象继承的方法：valueOf()和toString()。
+ 2.1 valueOf()
valueOf()方法返回包装对象实例对应的原始类型的值。
```
new Number(123).valueOf()  // 123
new String('abc').valueOf() // "abc"
new Boolean(true).valueOf() // true
```

+ 2.2 toString()
toString()方法返回对应的字符串形式。
```
new Number(123).toString() // "123"
new String('abc').toString() // "abc"
new Boolean(true).toString() // "true"
```

##### 3、原始类型与实例对象的自动转换
某些场合，原始类型的值会自动当作包装对象调用，即调用包装对象的属性和方法。这时，JavaScript 引擎会自动将原始类型的值转为包装对象实例，并在使用后立刻销毁实例。
+ 比如，字符串可以调用length属性，返回字符串的长度。
```
'abc'.length // 3
```
+ 上面代码中，abc是一个字符串，本身不是对象，不能调用length属性。JavaScript 引擎自动将其转为包装对象，在这个对象上调用length属性。调用结束后，这个临时对象就会被销毁。这就叫原始类型与实例对象的自动转换。
```
var str = 'abc';
str.length // 3

// 等同于
var strObj = new String(str)
// String {
//   0: "a", 1: "b", 2: "c", length: 3, [[PrimitiveValue]]: "abc"
// }
strObj.length // 3
```
+ 自动转换生成的包装对象是只读的，无法修改。所以，字符串无法添加新属性。
```
var s = 'Hello World';
s.x = 123;
s.x // undefined
```
+ 另一方面，调用结束后，包装对象实例会自动销毁。这意味着，下一次调用字符串的属性时，实际是调用一个新生成的对象，而不是上一次调用时生成的那个对象，所以取不到赋值在上一个对象的属性。如果要为字符串添加属性，只有在它的原型对象String.prototype上定义

##### 4、自定义方法
除了原生的实例方法，包装对象还可以自定义方法和属性，供原始类型的值直接调用，比如，我们可以新增一个double方法，使得字符串和数字翻倍。
```
String.prototype.double = function () {
  return this.valueOf() + this.valueOf();
};

'abc'.double()
// abcabc

Number.prototype.double = function () {
  return this.valueOf() + this.valueOf();
};

(123).double() // 246
```

#### 五、Boolean 对象

##### 1、概述
Boolean对象是 JavaScript 的三个包装对象之一。作为构造函数，它主要用于生成布尔值的包装对象实例。
```
var b = new Boolean(true);
typeof b // "object"
b.valueOf() // true
```
##### 2、Boolean 函数的类型转换作用
Boolean对象除了可以作为构造函数，还可以单独使用，将任意值转为布尔值。这时Boolean就是一个单纯的工具方法。
```
Boolean(undefined) // false
Boolean(null) // false
Boolean(0) // false
Boolean('') // false
Boolean(NaN) // false
Boolean(1) // true
Boolean('false') // true
Boolean([]) // true
Boolean({}) // true
Boolean(function () {}) // true
Boolean(/foo/) // true
```
+ 顺便提一下，使用双重的否运算符（!）也可以将任意值转为对应的布尔值。
```
!!undefined // false
!!null // false
!!0 // false
!!'' // false
!!NaN // false

!!1 // true
!!'false' // true
!![] // true
!!{} // true
!!function(){} // true
!!/foo/ // true
```
+ 最后，对于一些特殊值，Boolean对象前面加不加new，会得到完全相反的结果，必须小心。
```
if (Boolean(false)) {
  console.log('true');
} // 无输出

if (new Boolean(false)) {
  console.log('true');
} // true

if (Boolean(null)) {
  console.log('true');
} // 无输出

if (new Boolean(null)) {
  console.log('true');
} // true
```

#### 六、Number 对象

##### 1、概述
Number对象是数值对应的包装对象，可以作为构造函数使用，也可以作为工具函数使用，作为构造函数时，它用于生成值为数值的对象。
```
var n = new Number(1);
typeof n // "object"
```
+ 作为工具函数时，它可以将任何类型的值转为数值。
```
Number(true) // 1
```
##### 2、静态属性
Number对象拥有以下一些静态属性（即直接定义在Number对象上的属性，而不是定义在实例上的属性）。
+ Number.POSITIVE_INFINITY：正的无限，指向Infinity。
+ Number.NEGATIVE_INFINITY：负的无限，指向-Infinity。
+ Number.NaN：表示非数值，指向NaN。
+ Number.MIN_VALUE：表示最小的正数（即最接近0的正数，在64位浮点数体系中为5e-324），相应的，最接近0的负数为-Number.MIN_VALUE。
+ Number.MAX_SAFE_INTEGER：表示能够精确表示的最大整数，即9007199254740991。
+ Number.MIN_SAFE_INTEGER：表示能够精确表示的最小整数，即-9007199254740991。

##### 3、实例方法
+ 3.1 Number.prototype.toString()
Number对象部署了自己的toString方法，用来将一个数值转为字符串形式。

+ toString方法可以接受一个参数，表示输出的进制。如果省略这个参数，默认将数值先转为十进制，再输出字符串；否则，就根据参数指定的进制，将一个数字转化成某个进制的字符串。
```
(10).toString(2) // "1010"
(10).toString(8) // "12"
(10).toString(16) // "a"
```

+ 3.2 Number.prototype.toFixed()
toFixed()方法先将一个数转为指定位数的小数，然后返回这个小数对应的字符串。
```
(10).toFixed(2) // "10.00"
10.005.toFixed(2) // "10.01"
```

+ 3.3 Number.prototype.toExponential()
toExponential方法用于将一个数转为科学计数法形式。
```
(10).toExponential()  // "1e+1"
(10).toExponential(1) // "1.0e+1"
(10).toExponential(2) // "1.00e+1"

(1234).toExponential()  // "1.234e+3"
(1234).toExponential(1) // "1.2e+3"
(1234).toExponential(2) // "1.23e+3"
```

+ 3.4 Number.prototype.toPrecision()
Number.prototype.toPrecision()方法用于将一个数转为指定位数的有效数字。
```
(12.34).toPrecision(1) // "1e+1"
(12.34).toPrecision(2) // "12"
(12.34).toPrecision(3) // "12.3"
(12.34).toPrecision(4) // "12.34"
(12.34).toPrecision(5) // "12.340"
```
+ 该方法用于四舍五入时不太可靠，跟浮点数不是精确储存有关。
```
(12.35).toPrecision(3) // "12.3"
(12.25).toPrecision(3) // "12.3"
(12.15).toPrecision(3) // "12.2"
(12.45).toPrecision(3) // "12.4"
```

+ 3.5 Number.prototype.toLocaleString()
Number.prototype.toLocaleString()方法接受一个地区码作为参数，返回一个字符串，表示当前数字在该地区的当地书写形式。
```
(123).toLocaleString('zh-Hans-CN-u-nu-hanidec')
// "一二三"
```
+ 该方法还可以接受第二个参数配置对象，用来定制指定用途的返回字符串。该对象的style属性指定输出样式，默认值是decimal，表示输出十进制形式。如果值为percent，表示输出百分数。
```
(123).toLocaleString('zh-Hans-CN', { style: 'percent' })
// "12,300%"
```
+ 如果style属性的值为currency，则可以搭配currency属性，输出指定格式的货币字符串形式。
```
(123).toLocaleString('zh-Hans-CN', { style: 'currency', currency: 'CNY' })
// "￥123.00"

(123).toLocaleString('de-DE', { style: 'currency', currency: 'EUR' })
// "123,00 €"

(123).toLocaleString('en-US', { style: 'currency', currency: 'USD' })
// "$123.00"
```
#### 七、String 对象

##### 1、概述
String对象是 JavaScript 原生提供的三个包装对象之一，用来生成字符串对象。
```
var s1 = 'abc';
var s2 = new String('abc');

typeof s1 // "string"
typeof s2 // "object"
s2.valueOf() // "abc"
```
##### 2、静态方法
+ 2.1 String.fromCharCode()
String对象提供的静态方法（即定义在对象本身，而不是定义在对象实例的方法），主要是String.fromCharCode()。该方法的参数是一个或多个数值，代表 Unicode 码点，返回值是这些码点组成的字符串。
```
String.fromCharCode() // ""
String.fromCharCode(97) // "a"
String.fromCharCode(104, 101, 108, 108, 111)
// "hello"
```
##### 3、实例属性 String.prototype.length
字符串实例的length属性返回字符串的长度。
```
'abc'.length // 3
```
##### 4、实例方法
+ 4.1、String.prototype.charAt()
charAt方法返回指定位置的字符，参数是从0开始编号的位置。
```
var s = new String('abc');
s.charAt(1) // "b"
s.charAt(s.length - 1) // "c"
```
+ 4.2 String.prototype.charCodeAt()
charCodeAt()方法返回字符串指定位置的 Unicode 码点（十进制表示），相当于String.fromCharCode()的逆操作。
```
'abc'.charCodeAt(1) // 98
```
+ 4.3 String.prototype.concat() 
concat方法用于连接两个字符串，返回一个新字符串，不改变原字符串。
```
var s1 = 'abc';
var s2 = 'def';

s1.concat(s2) // "abcdef"
s1 // "abc"
'a'.concat('b', 'c') // "abc"
```
+ 如果参数不是字符串，concat方法会将其先转为字符串，然后再连接。
```
var one = 1;
var two = 2;
var three = '3';

''.concat(one, two, three) // "123"
one + two + three // "33"
```
+ 4.4 String.prototype.slice()
slice()方法用于从原字符串取出子字符串并返回，不改变原字符串。它的第一个参数是子字符串的开始位置，第二个参数是子字符串的结束位置（不含该位置）。
```
'JavaScript'.slice(0, 4) // "Java"
'JavaScript'.slice(4) // "Script"
```
+ 如果参数是负值，表示从结尾开始倒数计算的位置，即该负值加上字符串长度。
```
'JavaScript'.slice(-6) // "Script"
'JavaScript'.slice(0, -6) // "Java"
'JavaScript'.slice(-2, -1) // "p"
```
+ 如果第一个参数大于第二个参数（正数情况下），slice()方法返回一个空字符串。
```
'JavaScript'.slice(2, 1) // ""
```
+ 4.5 String.prototype.substring() 
substring方法用于从原字符串取出子字符串并返回，不改变原字符串，跟slice方法很相像。它的第一个参数表示子字符串的开始位置，第二个位置表示结束位置（返回结果不含该位置）。
```
'JavaScript'.substring(0, 4) // "Java"
```
+ 如果第一个参数大于第二个参数，substring方法会自动更换两个参数的位置。
```
'JavaScript'.substring(10, 4) // "Script"
// 等同于
'JavaScript'.substring(4, 10) // "Script"
```
+ 如果参数是负数，substring方法会自动将负数转为0。
```
'JavaScript'.substring(-3) // "JavaScript"
'JavaScript'.substring(4, -3) // "Java"
```
+ 4.6 String.prototype.substr()
substr方法用于从原字符串取出子字符串并返回，不改变原字符串，跟slice和substring方法的作用相同
+ substr方法的第一个参数是子字符串的开始位置（从0开始计算），第二个参数是子字符串的长度。
```
'JavaScript'.substr(4, 6) // "Script"
```
+ 如果省略第二个参数，则表示子字符串一直到原字符串的结束。
```
'JavaScript'.substr(4) // "Script"
```
+ 如果第一个参数是负数，表示倒数计算的字符位置。如果第二个参数是负数，将被自动转为0，因此会返回空字符串。
```
'JavaScript'.substr(-6) // "Script"
'JavaScript'.substr(4, -1) // ""
```
+ 4.7 String.prototype.indexOf()，String.prototype.lastIndexOf()
indexOf方法用于确定一个字符串在另一个字符串中第一次出现的位置，返回结果是匹配开始的位置。如果返回-1，就表示不匹配。
```
'hello world'.indexOf('o') // 4
'JavaScript'.indexOf('script') // -1
```
+ indexOf方法还可以接受第二个参数，表示从该位置开始向后匹配。
```
'hello world'.indexOf('o', 6) // 7
```
+ lastIndexOf方法的用法跟indexOf方法一致，主要的区别是lastIndexOf从尾部开始匹配，indexOf则是从头部开始匹配。
```
'hello world'.lastIndexOf('o') // 7
```
+ 另外，lastIndexOf的第二个参数表示从该位置起向前匹配。
```
'hello world'.lastIndexOf('o', 6) // 4
```
+ 4.8 String.prototype.trim()
trim方法用于去除字符串两端的空格，返回一个新字符串，不改变原字符串。
```
'  hello world  '.trim()
// "hello world"
```
+ 该方法去除的不仅是空格，还包括制表符（\t、\v）、换行符（\n）和回车符（\r）。
```
'\r\nabc \t'.trim() // 'abc'
```
+ 4.9 String.prototype.toLowerCase()，String.prototype.toUpperCase()
toLowerCase方法用于将一个字符串全部转为小写，toUpperCase则是全部转为大写。它们都返回一个新字符串，不改变原字符串。
```
'Hello World'.toLowerCase()
// "hello world"

'Hello World'.toUpperCase()
// "HELLO WORLD"
```
+ 4.10 String.prototype.match() 
match方法用于确定原字符串是否匹配某个子字符串，返回一个数组，成员为匹配的第一个字符串。如果没有找到匹配，则返回null。
```
'cat, bat, sat, fat'.match('at') // ["at"]
'cat, bat, sat, fat'.match('xt') // null
```
+ 返回的数组还有index属性和input属性，分别表示匹配字符串开始的位置和原始字符串。
```
var matches = 'cat, bat, sat, fat'.match('at');
matches.index // 1
matches.input // "cat, bat, sat, fat"
```
+ match方法还可以使用正则表达式作为参数
+ 4.11 String.prototype.search()，String.prototype.replace()
search方法的用法基本等同于match，但是返回值为匹配的第一个位置。如果没有找到匹配，则返回-1。
```
'cat, bat, sat, fat'.search('at') // 1
```
+ search方法还可以使用正则表达式作为参数
+ replace方法用于替换匹配的子字符串，一般情况下只替换第一个匹配（除非使用带有g修饰符的正则表达式）。
```
'aaa'.replace('a', 'b') // "baa"
```
+ 4.12 String.prototype.split() 
split方法按照给定规则分割字符串，返回一个由分割出来的子字符串组成的数组。
```
'a|b|c'.split('|') // ["a", "b", "c"]
'a|b|c'.split('') // ["a", "|", "b", "|", "c"]
'a|b|c'.split() // ["a|b|c"]
```
+ 如果满足分割规则的两个部分紧邻着（即两个分割符中间没有其他字符），则返回数组之中会有一个空字符串。
```
'a||c'.split('|') // ['a', '', 'c']
```
+ 如果满足分割规则的部分处于字符串的开头或结尾（即它的前面或后面没有其他字符），则返回数组的第一个或最后一个成员是一个空字符串。
```
'|b|c'.split('|') // ["", "b", "c"]
'a|b|'.split('|') // ["a", "b", ""]
```
+ split方法还可以接受第二个参数，限定返回数组的最大成员数。
```
'a|b|c'.split('|', 0) // []
'a|b|c'.split('|', 1) // ["a"]
'a|b|c'.split('|', 2) // ["a", "b"]
'a|b|c'.split('|', 3) // ["a", "b", "c"]
'a|b|c'.split('|', 4) // ["a", "b", "c"]
```
+ 4.13 String.prototype.localeCompare()
localeCompare方法用于比较两个字符串。它返回一个整数，如果小于0，表示第一个字符串小于第二个字符串；如果等于0，表示两者相等；如果大于0，表示第一个字符串大于第二个字符串。
```
'apple'.localeCompare('banana') // -1
'apple'.localeCompare('apple') // 0
```
+ 该方法的最大特点，就是会考虑自然语言的顺序。举例来说，正常情况下，大写的英文字母小于小写字母。
```
'B' > 'a' // false
```

+ 上面代码中，字母B小于字母a。因为 JavaScript 采用的是 Unicode 码点比较，B的码点是66，而a的码点是97，但是，localeCompare方法会考虑自然语言的排序情况，将B排在a的前面。
```
'B'.localeCompare('a') // 1
```
+ localeCompare还可以有第二个参数，指定所使用的语言（默认是英语），然后根据该语言的规则进行比较。
```
'ä'.localeCompare('z', 'de') // -1
'ä'.localeCompare('z', 'sv') // 1
```
+ 上面代码中，de表示德语，sv表示瑞典语。德语中，ä小于z，所以返回-1；瑞典语中，ä大于z，所以返回1。

#### 八、Math 对象

##### 1、静态属性
Math对象的静态属性，提供以下一些数学常数。
+ Math.E：常数e。
+ Math.LN2：2 的自然对数。
+ Math.LN10：10 的自然对数。
+ Math.LOG2E：以 2 为底的e的对数。
+ Math.LOG10E：以 10 为底的e的对数。
+ Math.PI：常数π。
+ Math.SQRT1_2：0.5 的平方根。
+ Math.SQRT2：2 的平方根。
```
Math.E // 2.718281828459045
Math.LN2 // 0.6931471805599453
Math.LN10 // 2.302585092994046
Math.LOG2E // 1.4426950408889634
Math.LOG10E // 0.4342944819032518
Math.PI // 3.141592653589793
Math.SQRT1_2 // 0.7071067811865476
Math.SQRT2 // 1.4142135623730951
```
+ 这些属性都是只读的，不能修改。

##### 2、静态方法
Math对象提供以下一些静态方法。
+ Math.abs()：绝对值
+ Math.ceil()：向上取整
+ Math.floor()：向下取整
+ Math.max()：最大值
+ Math.min()：最小值
+ Math.pow()：幂运算
+ Math.sqrt()：平方根
+ Math.log()：自然对数
+ Math.exp()：e的指数
+ Math.round()：四舍五入
+ Math.random()：随机数

##### 3、三角函数方法
Math对象还提供一系列三角函数方法。
+ Math.sin()：返回参数的正弦（参数为弧度值）
+ Math.cos()：返回参数的余弦（参数为弧度值）
+ Math.tan()：返回参数的正切（参数为弧度值）
+ Math.asin()：返回参数的反正弦（返回值为弧度值）
+ Math.acos()：返回参数的反余弦（返回值为弧度值）
+ Math.atan()：返回参数的反正切（返回值为弧度值）
```
Math.sin(0) // 0
Math.cos(0) // 1
Math.tan(0) // 0
Math.sin(Math.PI / 2) // 1
Math.asin(1) // 1.5707963267948966
Math.acos(1) // 0
Math.atan(1) // 0.7853981633974483
```

#### 九、Date 对象
Date对象是 JavaScript 原生的时间库。它以国际标准时间（UTC）1970年1月1日00:00:00作为时间的零点，可以表示的时间范围是前后各1亿天（单位为毫秒）。

##### 1、普通函数的用法
Date对象可以作为普通函数直接调用，返回一个代表当前时间的字符串。
```
Date()
// "Wed Dec 15 2021 16:24:47 GMT+0800 (中国标准时间)"
```

##### 2、构造函数的用法
Date还可以当作构造函数使用。对它使用new命令，会返回一个Date对象的实例。如果不加参数，实例代表的就是当前时间。
```
var today = new Date();

today
// "Wed Dec 15 2021 16:24:47 GMT+0800 (中国标准时间)"

// 等同于
today.toString()
// "Wed Dec 15 2021 16:24:47 GMT+0800 (中国标准时间)"
```
+ 作为构造函数时，Date对象可以接受多种格式的参数，返回一个该参数对应的时间实例。
```
// 参数为时间零点开始计算的毫秒数
new Date(1378218728000)
// Tue Sep 03 2013 22:32:08 GMT+0800 (CST)

// 参数为日期字符串
new Date('January 6, 2013');
// Sun Jan 06 2013 00:00:00 GMT+0800 (CST)

// 参数为多个整数，
// 代表年、月、日、小时、分钟、秒、毫秒
new Date(2013, 0, 1, 0, 0, 0, 0)
// Tue Jan 01 2013 00:00:00 GMT+0800 (CST)
```
##### 3、日期的运算
类型自动转换时，Date实例如果转为数值，则等于对应的毫秒数；如果转为字符串，则等于对应的日期字符串。所以，两个日期实例对象进行减法运算时，返回的是它们间隔的毫秒数；进行加法运算时，返回的是两个字符串连接而成的新字符串。
```
var d1 = new Date(2000, 2, 1);
var d2 = new Date(2000, 3, 1);

d2 - d1
// 2678400000
d2 + d1
// "Sat Apr 01 2000 00:00:00 GMT+0800 (CST)Wed Mar 01 2000 00:00:00 GMT+0800 (CST)"
```
##### 4、静态方法
+ 4.1 Date.now() 
+ Date.now方法返回当前时间距离时间零点（1970年1月1日 00:00:00 UTC）的毫秒数，相当于 Unix 时间戳乘以1000。
```
Date.now() // 1364026285194
```
+ 4.2 Date.parse()
+ Date.parse方法用来解析日期字符串，返回该时间距离时间零点（1970年1月1日 00:00:00）的毫秒数，日期字符串应该符合 RFC 2822 和 ISO 8061 这两个标准，即YYYY-MM-DDTHH:mm:ss.sssZ格式，其中最后的Z表示时区。但是，其他格式也可以被解析，如下：
```
Date.parse('Aug 9, 1995')
Date.parse('January 26, 2011 13:51:50')
Date.parse('Mon, 25 Dec 1995 13:30:00 GMT')
Date.parse('Mon, 25 Dec 1995 13:30:00 +0430')
Date.parse('2011-10-10')
Date.parse('2011-10-10T14:48:00')
```
+ 如果解析失败，返回NaN。
```
Date.parse('xxx') // NaN
```
+ 4.3 Date.UTC()
+ Date.UTC方法接受年、月、日等变量作为参数，返回该时间距离时间零点（1970年1月1日 00:00:00 UTC）的毫秒数。
```
// 格式
Date.UTC(year, month[, date[, hrs[, min[, sec[, ms]]]]])

// 用法
Date.UTC(2011, 0, 1, 2, 3, 4, 567)
// 1293847384567
```

##### 5、实例方法
Date的实例对象，有几十个自己的方法，除了valueOf和toString，可以分为以下三类：
+ to类：从Date对象返回一个字符串，表示指定的时间。
+ get类：获取Date对象的日期和时间。
+ set类：设置Date对象的日期和时间。
+ 5.1 Date.prototype.valueOf()
valueOf方法返回实例对象距离时间零点（1970年1月1日00:00:00 UTC）对应的毫秒数，该方法等同于getTime方法。
```
var d = new Date();
d.valueOf() // 1362790014817
d.getTime() // 1362790014817
```
+ 预期为数值的场合，Date实例会自动调用该方法，所以可以用下面的方法计算时间的间隔。
```
var start = new Date();
// ...
var end = new Date();
var elapsed = end - start;
```
+ 5.2 to 类方法
+ （1）Date.prototype.toString()
+ toString方法返回一个完整的日期字符串。
```
var d = new Date(2013, 0, 1);
d.toString()
// "Tue Jan 01 2013 00:00:00 GMT+0800 (CST)"
d
// "Tue Jan 01 2013 00:00:00 GMT+0800 (CST)"
```
+ 因为toString是默认的调用方法，所以如果直接读取Date实例，就相当于调用这个方法。
+ （2）Date.prototype.toUTCString()
+ toUTCString方法返回对应的 UTC 时间，也就是比北京时间晚8个小时。
```
var d = new Date(2013, 0, 1);
d.toUTCString()
// "Mon, 31 Dec 2012 16:00:00 GMT"
```
+ （3）Date.prototype.toISOString()
+ toISOString方法返回对应时间的 ISO8601 写法。
```
var d = new Date(2013, 0, 1);
d.toISOString()
// "2012-12-31T16:00:00.000Z"
```
+ （4）Date.prototype.toJSON()
+ toJSON方法返回一个符合 JSON 格式的 ISO 日期字符串，与toISOString方法的返回结果完全相同。
```
var d = new Date(2013, 0, 1);
d.toJSON()
// "2012-12-31T16:00:00.000Z"
```
+ （5）Date.prototype.toDateString()
+ toDateString方法返回日期字符串（不含小时、分和秒）。
```
var d = new Date(2013, 0, 1);
d.toDateString() // "Tue Jan 01 2013"
```
+ （6）Date.prototype.toTimeString()
+ toTimeString方法返回时间字符串（不含年月日）。
```
var d = new Date(2013, 0, 1);
d.toTimeString() // "00:00:00 GMT+0800 (CST)"
```
+ （7）本地时间
+ 以下三种方法，可以将 Date 实例转为表示本地时间的字符串。
+ Date.prototype.toLocaleString()：完整的本地时间。
+ Date.prototype.toLocaleDateString()：本地日期（不含小时、分和秒）。
+ Date.prototype.toLocaleTimeString()：本地时间（不含年月日）。
```
var d = new Date(2013, 0, 1);

d.toLocaleString()
// 中文版浏览器为"2013年1月1日 上午12:00:00"
// 英文版浏览器为"1/1/2013 12:00:00 AM"

d.toLocaleDateString()
// 中文版浏览器为"2013年1月1日"
// 英文版浏览器为"1/1/2013"

d.toLocaleTimeString()
// 中文版浏览器为"上午12:00:00"
// 英文版浏览器为"12:00:00 AM"
```
+ 5.3 get 类方法
+ Date对象提供了一系列get*方法，用来获取实例对象某个方面的值。
+ getTime()：返回实例距离1970年1月1日00:00:00的毫秒数，等同于valueOf方法。
+ getDate()：返回实例对象对应每个月的几号（从1开始）。
+ getDay()：返回星期几，星期日为0，星期一为1，以此类推。
+ getFullYear()：返回四位的年份。
+ getMonth()：返回月份（0表示1月，11表示12月）。
+ getHours()：返回小时（0-23）。
+ getMilliseconds()：返回毫秒（0-999）。
+ getMinutes()：返回分钟（0-59）。
+ getSeconds()：返回秒（0-59）。
+ getTimezoneOffset()：返回当前时间与 UTC 的时区差异，以分钟表示，返回结果考虑到了夏令时因素。
+ 上面这些get*方法返回的都是当前时区的时间，Date对象还提供了这些方法对应的 UTC 版本，用来返回 UTC 时间。
+ getUTCDate()
+ getUTCFullYear()
+ getUTCMonth()
+ getUTCDay()
+ getUTCHours()
+ getUTCMinutes()
+ getUTCSeconds()
+ getUTCMilliseconds()
+ 5.4 set 类方法
+ Date对象提供了一系列set*方法，用来设置实例对象的各个方面。
+ setDate(date)：设置实例对象对应的每个月的几号（1-31），返回改变后毫秒时间戳。
+ setFullYear(year [, month, date])：设置四位年份。
+ setHours(hour [, min, sec, ms])：设置小时（0-23）。
+ setMilliseconds()：设置毫秒（0-999）。
+ setMinutes(min [, sec, ms])：设置分钟（0-59）。
+ setMonth(month [, date])：设置月份（0-11）。
+ setSeconds(sec [, ms])：设置秒（0-59）。
+ setTime(milliseconds)：设置毫秒时间戳。


#### 十、RegExp 对象

##### 1、概述
正则表达式（regular expression）是一种表达文本模式（即字符串结构）的方法，有点像字符串的模板，常常用来按照“给定模式”匹配文本。比如，正则表达式给出一个 Email 地址的模式，然后用它来确定一个字符串是否为 Email 地址。JavaScript 的正则表达式体系是参照 Perl 5 建立的。
+ 新建正则表达式有两种方法。一种是使用字面量，以斜杠表示开始和结束。
```
var regex = /xyz/;
```
+ 另一种是使用RegExp构造函数。
```
var regex = new RegExp('xyz');
```
+ 它们的主要区别是，第一种方法在引擎编译代码时，就会新建正则表达式，第二种方法在运行时新建正则表达式，所以前者的效率较高。而且，前者比较便利和直观，所以实际应用中，基本上都采用字面量定义正则表达式。
+ RegExp构造函数还可以接受第二个参数，表示修饰符（详细解释见下文）。
```
var regex = new RegExp('xyz', 'i');
// 等价于
var regex = /xyz/i;
```
+ 上面代码中，正则表达式/xyz/有一个修饰符i。

##### 2、实例属性
+ 2.1 正则对象的实例属性分成两类。
一类是修饰符相关，用于了解设置了什么修饰符。
+ RegExp.prototype.ignoreCase：返回一个布尔值，表示是否设置了i修饰符。
+ RegExp.prototype.global：返回一个布尔值，表示是否设置了g修饰符。
+ RegExp.prototype.multiline：返回一个布尔值，表示是否设置了m修饰符。
+ RegExp.prototype.flags：返回一个字符串，包含了已经设置的所有修饰符，按字母排序。
+ 上面四个属性都是只读的。
```
var r = /abc/igm;
r.ignoreCase // true
r.global // true
r.multiline // true
r.flags // 'gim'
```
+ 2.2 另一类是与修饰符无关的属性，主要是下面两个。
+ RegExp.prototype.lastIndex：返回一个整数，表示下一次开始搜索的位置。该属性可读写，但是只在进行连续搜索时有意义，详细介绍请看后文。
+ RegExp.prototype.source：返回正则表达式的字符串形式（不包括反斜杠），该属性只读。
```
var r = /abc/igm;
r.lastIndex // 0
r.source // "abc"
```
##### 3、实例方法
+ 3.1 RegExp.prototype.test()
正则实例对象的test方法返回一个布尔值，表示当前模式是否能匹配参数字符串。
```
/cat/.test('cats and dogs') // true
```
+ 如果正则表达式带有g修饰符，则每一次test方法都从上一次结束的位置开始向后匹配。
```
var r = /x/g;
var s = '_x_x';

r.lastIndex // 0
r.test(s) // true

r.lastIndex // 2
r.test(s) // true

r.lastIndex // 4
r.test(s) // false
```
+ 带有g修饰符时，可以通过正则对象的lastIndex属性指定开始搜索的位置。
```
var r = /x/g;
var s = '_x_x';

r.lastIndex = 4;
r.test(s) // false

r.lastIndex // 0
r.test(s)
```
+ 3.2 RegExp.prototype.exec()
正则实例对象的exec()方法，用来返回匹配结果。如果发现匹配，就返回一个数组，成员是匹配成功的子字符串，否则返回null。
```
var s = '_x_x';
var r1 = /x/;
var r2 = /y/;

r1.exec(s) // ["x"]
r2.exec(s) // null
```
+ 如果正则表示式包含圆括号（即含有“组匹配”），则返回的数组会包括多个成员。第一个成员是整个匹配成功的结果，后面的成员就是圆括号对应的匹配成功的组。
```
var s = '_x_x';
var r = /_(x)/;
r.exec(s) // ["_x", "x"]
```
+ exec()方法的返回数组还包含以下两个属性：
```
input：整个原字符串。
index：模式匹配成功的开始位置（从0开始计数）。

var r = /a(b+)a/;
var arr = r.exec('_abbba_aba_');
arr // ["abbba", "bbb"]

arr.index // 1
arr.input // "_abbba_aba_"
```
##### 4、字符串的实例方法
字符串的实例方法之中，有4种与正则表达式有关。
+ String.prototype.match()：返回一个数组，成员是所有匹配的子字符串。
+ String.prototype.search()：按照给定的正则表达式进行搜索，返回一个整数，表示匹配开始的位置。
+ String.prototype.replace()：按照给定的正则表达式进行替换，返回替换后的字符串。
+ String.prototype.split()：按照给定规则进行字符串分割，返回一个数组，包含分割后的各个成员。
+ 4.1 String.prototype.match()
字符串实例对象的match方法对字符串进行正则匹配，返回匹配结果。
```
var s = '_x_x';
var r1 = /x/;
var r2 = /y/;

s.match(r1) // ["x"]
s.match(r2) // null
```
+ 从上面代码可以看到，字符串的match方法与正则对象的exec方法非常类似：匹配成功返回一个数组，匹配失败返回null如果正则表达式带有g修饰符，则该方法与正则对象的exec方法行为不同，会一次性返回所有匹配成功的结果。
```
var s = 'abba';
var r = /a/g;

s.match(r) // ["a", "a"]
r.exec(s) // ["a"]
```
+ 4.2 String.prototype.search()
字符串对象的search方法，返回第一个满足条件的匹配结果在整个字符串中的位置。如果没有任何匹配，则返回-1。
```
'_x_x'.search(/x/)
// 1
```
+ 4.3 String.prototype.replace()
字符串对象的replace方法可以替换匹配的值。它接受两个参数，第一个是正则表达式，表示搜索模式，第二个是替换的内容。
```
str.replace(search, replacement)
```
+ 正则表达式如果不加g修饰符，就替换第一个匹配成功的值，否则替换所有匹配成功的值。
```
'aaa'.replace('a', 'b') // "baa"
'aaa'.replace(/a/, 'b') // "baa"
'aaa'.replace(/a/g, 'b') // "bbb"
```
+ 4.4 String.prototype.split()
字符串对象的split方法按照正则规则分割字符串，返回一个由分割后的各个部分组成的数组。
+ str.split(separator, [limit])
+ 该方法接受两个参数，第一个参数是正则表达式，表示分隔规则，第二个参数是返回数组的最大成员数。
```
// 非正则分隔
'a,  b,c, d'.split(',')
// [ 'a', '  b', 'c', ' d' ]

// 正则分隔，去除多余的空格
'a,  b,c, d'.split(/, */)
// [ 'a', 'b', 'c', 'd' ]

// 指定返回数组的最大成员
'a,  b,c, d'.split(/, */, 2)
[ 'a', 'b' ]
```
##### 5、 匹配规则
正则表达式的规则很复杂，下面一一介绍这些规则。
+ 5.1 字面量字符和元字符
+ 大部分字符在正则表达式中，就是字面的含义，比如/a/匹配a，/b/匹配b。如果在正则表达式之中，某个字符只表示它字面的含义（就像前面的a和b），那么它们就叫做“字面量字符”（literal characters）。
```
/dog/.test('old dog') // true
```
+ 上面代码中正则表达式的dog，就是字面量字符，所以/dog/匹配old dog，因为它就表示d、o、g三个字母连在一起。
+ 除了字面量字符以外，还有一部分字符有特殊含义，不代表字面的意思。它们叫做“元字符”（metacharacters），主要有以下几个。
+ （1）点字符（.)
+ 点字符（.）匹配除回车（\r）、换行(\n) 、行分隔符（\u2028）和段分隔符（\u2029）以外的所有字符。注意，对于码点大于0xFFFF字符，点字符不能正确匹配，会认为这是两个字符。
```
/c.t/.test('cat'); // true
/c.a/.test('c-a'); // true
/c.t/.test('coot'); // false
```
+ 上面代码中，c.t匹配c和t之间包含任意一个字符的情况，只要这三个字符在同一行，比如cat、c2t、c-t等等，但是不匹配coot。
+ （2）位置字符
+ 位置字符用来提示字符所处的位置，主要有两个字符。
+ ^ 表示字符串的开始位置
+ $ 表示字符串的结束位置
```
// test必须出现在开始位置
/^test/.test('test123') // true

// test必须出现在结束位置
/test$/.test('new test') // true

// 从开始位置到结束位置只有test
/^test$/.test('test') // true
/^test$/.test('test test') // false
```
+ （3）选择符（|）
+ 竖线符号（|）在正则表达式中表示“或关系”（OR），即cat|dog表示匹配cat或dog。
```
/11|22/.test('911') // true
```
+ 选择符会包括它前后的多个字符，比如/ab|cd/指的是匹配ab或者cd，而不是指匹配b或者c。如果想修改这个行为，可以使用圆括号。
```
/a( |\t)b/.test('a\tb') // true
```
+ 面代码指的是，a和b之间有一个空格或者一个制表符。其他的元字符还包括\、*、+、?、()、[]、{}等，将在下文解释。
+ 5.2 转义符
+ 正则表达式中那些有特殊含义的元字符，如果要匹配它们本身，就需要在它们前面要加上反斜杠。比如要匹配+，就要写成\+。
```
/1+1/.test('1+1')
// false

/1\+1/.test('1+1')
// true
```
+ 上面代码中，第一个正则表达式之所以不匹配，因为加号是元字符，不代表自身。第二个正则表达式使用反斜杠对加号转义，就能匹配成功。
```
正则表达式中，需要反斜杠转义的，一共有12个字符：^、.、[、$、(、)、|、*、+、?、{和\
需要特别注意的是，如果使用RegExp方法生成正则对象，转义需要使用两个斜杠，因为字符串内部会先转义一次。
(new RegExp('1\+1')).test('1+1')
// false

(new RegExp('1\\+1')).test('1+1')
// true
```
+ 5.3 特殊字符
```
正则表达式对一些不能打印的特殊字符，提供了表达方法。

\cX 表示Ctrl-[X]，其中的X是A-Z之中任一个英文字母，用来匹配控制字符。
[\b] 匹配退格键(U+0008)，不要与\b混淆。
\n 匹配换行键。
\r 匹配回车键。
\t 匹配制表符 tab（U+0009）。
\v 匹配垂直制表符（U+000B）。
\f 匹配换页符（U+000C）。
\0 匹配null字符（U+0000）。
\xhh 匹配一个以两位十六进制数（\x00-\xFF）表示的字符。
\uhhhh 匹配一个以四位十六进制数（\u0000-\uFFFF）表示的 Unicode 字符。
```
+ 5.4 字符类 
+ 字符类（class）表示有一系列字符可供选择，只要匹配其中一个就可以了。所有可供选择的字符都放在方括号内，比如[xyz] 表示x、y、z之中任选一个匹配。
```
/[abc]/.test('hello world') // false
/[abc]/.test('apple') // true
```
+ 上面代码中，字符串hello world不包含a、b、c这三个字母中的任一个，所以返回false；字符串apple包含字母a，所以返回true。
+ （1）脱字符（^）
+ 如果方括号内的第一个字符是[^]，则表示除了字符类之中的字符，其他字符都可以匹配。比如，[^xyz]表示除了x、y、z之外都可以匹配。
```
/[^abc]/.test('bbc news') // true
/[^abc]/.test('bbc') // false
```
+ 如果方括号内没有其他字符，即只有[^]，就表示匹配一切字符，其中包括换行符。相比之下，点号作为元字符（.）是不包括换行符的。
```
var s = 'Please yes\nmake my day!';
s.match(/yes.*day/) // null
s.match(/yes[^]*day/) // [ 'yes\nmake my day']
```
+ 上面代码中，字符串s含有一个换行符，点号不包括换行符，所以第一个正则表达式匹配失败；第二个正则表达式[^]包含一切字符，所以匹配成功。
+ 注意，脱字符只有在字符类的第一个位置才有特殊含义，否则就是字面含义。
+ （2）连字符（-）
+ 某些情况下，对于连续序列的字符，连字符（-）用来提供简写形式，表示字符的连续范围。比如，[abc]可以写成[a-c]，[0123456789]可以写成[0-9]，同理[A-Z]表示26个大写字母。
```
/a-z/.test('b') // false
/[a-z]/.test('b') // true
```
+ 上面代码中，当连字号（dash）不出现在方括号之中，就不具备简写的作用，只代表字面的含义，所以不匹配字符b。只有当连字号用在方括号之中，才表示连续的字符序列。
+ 以下都是合法的字符类简写形式。
```
[0-9.,]
[0-9a-fA-F]
[a-zA-Z0-9-]
[1-31]
```
+ 上面代码中最后一个字符类[1-31]，不代表1到31，只代表1到3。
+ 连字符还可以用来指定 Unicode 字符的范围。]
```
var str = "\u0130\u0131\u0132";
/[\u0128-\uFFFF]/.test(str)
// true
```
+ 另外，不要过分使用连字符，设定一个很大的范围，否则很可能选中意料之外的字符。最典型的例子就是[A-z]，表面上它是选中从大写的A到小写的z之间52个字母，但是由于在 ASCII 编码之中，大写字母与小写字母之间还有其他字符，结果就会出现意料之外的结果。
```
/[A-z]/.test('\\') // true
```
+ 上面代码中，由于反斜杠（'\'）的ASCII码在大写字母与小写字母之间，结果会被选中。
+ 5.5 预定义模式
+ 预定义模式指的是某些常见模式的简写方式。
+ \d 匹配0-9之间的任一数字，相当于[0-9]。
+ \D 匹配所有0-9以外的字符，相当于[^0-9]。
+ \w 匹配任意的字母、数字和下划线，相当于[A-Za-z0-9_]。
+ \W 除所有字母、数字和下划线以外的字符，相当于[^A-Za-z0-9_]。
+ \s 匹配空格（包括换行符、制表符、空格符等），相等于[ \t\r\n\v\f]。
+ \S 匹配非空格的字符，相当于[^ \t\r\n\v\f]。
+ \b 匹配词的边界。
+ \B 匹配非词边界，即在词的内部。
```
// \s 的例子
/\s\w*/.exec('hello world') // [" world"]

// \b 的例子
/\bworld/.test('hello world') // true
/\bworld/.test('hello-world') // true
/\bworld/.test('helloworld') // false

// \B 的例子
/\Bworld/.test('hello-world') // false
/\Bworld/.test('helloworld') // true
```
+ 上面代码中，\s表示空格，所以匹配结果会包括空格。\b表示词的边界，所以world的词首必须独立（词尾是否独立未指定），才会匹配。同理，\B表示非词的边界，只有world的词首不独立，才会匹配。
+ 通常，正则表达式遇到换行符（\n）就会停止匹配。
```
var html = "<b>Hello</b>\n<i>world!</i>";
/.*/.exec(html)[0]
// "<b>Hello</b>"
```
+ 上面代码中，字符串html包含一个换行符，结果点字符（.）不匹配换行符，导致匹配结果可能不符合原意。这时使用\s字符类，就能包括换行符。
```
var html = "<b>Hello</b>\n<i>world!</i>";
/[\S\s]*/.exec(html)[0]
// "<b>Hello</b>\n<i>world!</i>"
```
+ 上面代码中，[\S\s]指代一切字符。
+ 5.6 重复类 
+ 模式的精确匹配次数，使用大括号（{}）表示。{n}表示恰好重复n次，{n,}表示至少重复n次，{n,m}表示重复不少于n次，不多于m次。
```
+ 上面代码中，第一个模式指定o连续出现2次，第二个模式指定o连续出现2次到5次之间。
/lo{2}k/.test('look') // true
/lo{2,5}k/.test('looook') // true
```
+ 5.7 量词符
+ 量词符用来设定某个模式出现的次数。
+ ? 问号表示某个模式出现0次或1次，等同于{0, 1}。
+ * 星号表示某个模式出现0次或多次，等同于{0,}。
+ 加号表示某个模式出现1次或多次，等同于{1,}。
```
// t 出现0次或1次
/t?est/.test('test') // true
/t?est/.test('est') // true

// t 出现1次或多次
/t+est/.test('test') // true
/t+est/.test('ttest') // true
/t+est/.test('est') // false

// t 出现0次或多次
/t*est/.test('test') // true
/t*est/.test('ttest') // true
/t*est/.test('tttest') // true
/t*est/.test('est') // true
```
+ 5.8 贪婪模式
+ 上一小节的三个量词符，默认情况下都是最大可能匹配，即匹配到下一个字符不满足匹配规则为止。这被称为贪婪模式。
```
var s = 'aaa';
s.match(/a+/) // ["aaa"]
```
+ 上面代码中，模式是/a+/，表示匹配1个a或多个a，那么到底会匹配几个a呢？因为默认是贪婪模式，会一直匹配到字符a不出现为止，所以匹配结果是3个a。
+ 除了贪婪模式，还有非贪婪模式，即最小可能匹配。只要一发现匹配，就返回结果，不要往下检查。如果想将贪婪模式改为非贪婪模式，可以在量词符后面加一个问号。
```
var s = 'aaa';
s.match(/a+?/) // ["a"]
```
+ 上面例子中，模式结尾添加了一个问号/a+?/，这时就改为非贪婪模式，一旦条件满足，就不再往下匹配，+?表示只要发现一个a，就不再往下匹配了。
+ 除了非贪婪模式的加号（+?），还有非贪婪模式的星号（*?）和非贪婪模式的问号（??）。
```
除了非贪婪模式的加号（+?），还有非贪婪模式的星号（*?）和非贪婪模式的问号（??）。
+?：表示某个模式出现1次或多次，匹配时采用非贪婪模式。
*?：表示某个模式出现0次或多次，匹配时采用非贪婪模式。
??：表格某个模式出现0次或1次，匹配时采用非贪婪模式。

'abb'.match(/ab*/) // ["abb"]
'abb'.match(/ab*?/) // ["a"]
'abb'.match(/ab?/) // ["ab"]
'abb'.match(/ab??/) // ["a"]
```
+ 上面例子中，/ab*/表示如果a后面有多个b，那么匹配尽可能多的b；/ab*?/表示匹配尽可能少的b，也就是0个b。\
+ 5.9 修饰符
+ 修饰符（modifier）表示模式的附加规则，放在正则模式的最尾部，修饰符可以单个使用，也可以多个一起使用。
```
// 单个修饰符
var regex = /test/i;

// 多个修饰符
var regex = /test/ig;
```
+ （1）g 修饰符
+ 默认情况下，第一次匹配成功后，正则对象就停止向下匹配了。g修饰符表示全局匹配（global），加上它以后，正则对象将匹配全部符合条件的结果，主要用于搜索和替换。
```
var regex = /b/;
var str = 'abba';
regex.test(str); // true
regex.test(str); // true
regex.test(str); // true
```
+ 上面代码中，正则模式不含g修饰符，每次都是从字符串头部开始匹配。所以，连续做了三次匹配，都返回true。
```
var regex = /b/g;
var str = 'abba';

regex.test(str); // true
regex.test(str); // true
regex.test(str); // false
```
+ 上面代码中，正则模式含有g修饰符，每次都是从上一次匹配成功处，开始向后匹配。因为字符串abba只有两个b，所以前两次匹配结果为true，第三次匹配结果为false。
+ （2）i 修饰符
+ 默认情况下，正则对象区分字母的大小写，加上i修饰符以后表示忽略大小写（ignoreCase）。
```
/abc/.test('ABC') // false
/abc/i.test('ABC') // true
```
+ 上面代码表示，加了i修饰符以后，不考虑大小写，所以模式abc匹配字符串ABC。
+ （3）m 修饰符
+ m修饰符表示多行模式（multiline），会修改^和$的行为。默认情况下（即不加m修饰符时），^和$匹配字符串的开始处和结尾处，加上m修饰符以后，^和$还会匹配行首和行尾，即^和$会识别换行符（\n）。
```
/world$/.test('hello world\n') // false
/world$/m.test('hello world\n') // true
```
+ 上面的代码中，字符串结尾处有一个换行符。如果不加m修饰符，匹配不成功，因为字符串的结尾不是world；加上以后，$可以匹配行尾。
```
/^b/m.test('a\nb') // true
```
+ 上面代码要求匹配行首的b，如果不加m修饰符，就相当于b只能处在字符串的开始处。加上m修饰符以后，换行符\n也会被认为是一行的开始。
+ 5.10 组匹配
+ （1）概述
+ 正则表达式的括号表示分组匹配，括号中的模式可以用来匹配分组的内容。
```
/fred+/.test('fredd') // true
/(fred)+/.test('fredfred') // true
```
+ 上面代码中，第一个模式没有括号，结果+只表示重复字母d，第二个模式有括号，结果+就表示匹配fred这个词。
+ 下面是另外一个分组捕获的例子。
```
var m = 'abcabc'.match(/(.)b(.)/);
m
// ['abc', 'a', 'c']
```
+ 上面代码中，正则表达式/(.)b(.)/一共使用两个括号，第一个括号捕获a，第二个括号捕获c。
+ 注意，使用组匹配时，不宜同时使用g修饰符，否则match方法不会捕获分组的内容。
+ 正则表达式内部，还可以用\n引用括号匹配的内容，n是从1开始的自然数，表示对应顺序的括号。
```
/(.)b(.)\1b\2/.test("abcabc")
// true
```
+ 上面的代码中，\1表示第一个括号匹配的内容（即a），\2表示第二个括号匹配的内容（即c）。
+ （2）非捕获组
+ (?:x)称为非捕获组（Non-capturing group），表示不返回该组匹配的内容，即匹配的结果中不计入这个括号。
+ （3）先行断言
+ x(?=y)称为先行断言（Positive look-ahead），x只有在y前面才匹配，y不会被计入返回结果。比如，要匹配后面跟着百分号的数字，可以写成/\d+(?=%)/。
+ 先行断言”中，括号里的部分是不会返回的。
```
var m = 'abc'.match(/b(?=c)/);
m // ["b"]
```
+ （4）先行否定断言
+ (?!y)称为先行否定断言（Negative look-ahead），x只有不在y前面才匹配，y不会被计入返回结果。比如，要匹配后面跟的不是百分号的数字，就要写成/\d+(?!%)/。
```
/\d+(?!\.)/.exec('3.14')
// ["14"]
```
+ 上面代码中，正则表达式指定，只有不在小数点前面的数字才会被匹配，因此返回的结果就是14。
+ “先行否定断言”中，括号里的部分是不会返回的。
```
var m = 'abd'.match(/b(?!c)/);
m // ['b']
```
+ 上面的代码使用了先行否定断言，b不在c前面所以被匹配，而且括号对应的d不会被返回。

#### 十一、JSON 对象
##### 1、JSON 格式
JSON 格式（JavaScript Object Notation 的缩写）是一种用于数据交换的文本格式，2001年由 Douglas Crockford 提出，目的是取代繁琐笨重的 XML 格式。
+ JSON 对值的类型和格式有严格的规定。
```
复合类型的值只能是数组或对象，不能是函数、正则表达式对象、日期对象。
原始类型的值只有四种：字符串、数值（必须以十进制表示）、布尔值和null（不能使用NaN, Infinity, -Infinity和undefined）。
字符串必须使用双引号表示，不能使用单引号。
对象的键名必须放在双引号里面。
数组或对象最后一个成员的后面，不能加逗号。
```
+ 以下都是合法的 JSON。
```
["one", "two", "three"]
{ "one": 1, "two": 2, "three": 3 }
{"names": ["张三", "李四"] }
[ { "name": "张三"}, {"name": "李四"} ]
```
+ 以下都是不合法的 JSON。
```
{ name: "张三", 'age': 32 }  // 属性名必须使用双引号
[32, 64, 128, 0xFFF] // 不能使用十六进制值
{ "name": "张三", "age": undefined } // 不能使用 undefined
{ "name": "张三",
  "birthday": new Date('Fri, 26 Aug 2011 07:13:10 GMT'),
  "getName": function () {
      return this.name;
  }
} // 属性值不能使用函数和日期对象
```
##### 2、JSON 对象
JSON对象是 JavaScript 的原生对象，用来处理 JSON 格式数据。它有两个静态方法：JSON.stringify()和JSON.parse()。

##### 3、JSON.stringify()
+ 3.1 基本用法
+ JSON.stringify()方法用于将一个值转为 JSON 字符串。该字符串符合 JSON 格式，并且可以被JSON.parse()方法还原。
```
JSON.stringify('abc') // ""abc""
JSON.stringify(1) // "1"
JSON.stringify(false) // "false"
JSON.stringify([]) // "[]"
JSON.stringify({}) // "{}"

JSON.stringify([1, "false", false])
// '[1,"false",false]'

JSON.stringify({ name: "张三" })
// '{"name":"张三"}'
```
+ 注意，对于原始类型的字符串，转换结果会带双引号。
```
JSON.stringify('foo') === "foo" // false
JSON.stringify('foo') === "\"foo\"" // true

JSON.stringify(false) // "false"
JSON.stringify('false') // "\"false\""
```
+ JSON.stringify()方法会忽略对象的不可遍历的属性。'
+ 正则对象会被转成空对象。
```
JSON.stringify(/foo/) // "{}"
```
+ 3.2 第二个参数
+ JSON.stringify()方法还可以接受一个数组，作为第二个参数，指定参数对象的哪些属性需要转成字符串。
```
var obj = {
  'prop1': 'value1',
  'prop2': 'value2',
  'prop3': 'value3'
};

var selectedProperties = ['prop1', 'prop2'];

JSON.stringify(obj, selectedProperties)
// "{"prop1":"value1","prop2":"value2"}"
```
+ 这个类似白名单的数组，只对对象的属性有效，对数组无效。
```
JSON.stringify(['a', 'b'], ['0'])
// "["a","b"]"

JSON.stringify({0: 'a', 1: 'b'}, ['0'])
// "{"0":"a"}"
```
+ 第二个参数还可以是一个函数，用来更改JSON.stringify()的返回值。
```
function f(key, value) {
  if (typeof value === "number") {
    value = 2 * value;
  }
  return value;
}

JSON.stringify({ a: 1, b: 2 }, f)
// '{"a": 2,"b": 4}'
```
+ 3.3 第三个参数
+ JSON.stringify()还可以接受第三个参数，用于增加返回的 JSON 字符串的可读性。
+ 默认返回的是单行字符串，对于大型的 JSON 对象，可读性非常差。第三个参数使得每个属性单独占据一行，并且将每个属性前面添加指定的前缀（不超过10个字符）。
```
// 默认输出
JSON.stringify({ p1: 1, p2: 2 })
// '{"p1":1,"p2":2}'

// 分行输出
JSON.stringify({ p1: 1, p2: 2 }, null, '\t')
// {
// 	"p1": 1,
// 	"p2": 2
// }
```
+ 上面例子中，第三个属性\t在每个属性前面添加一个制表符，然后分行显示。
+ 第三个属性如果是一个数字，则表示每个属性前面添加的空格（最多不超过10个）。
```
JSON.stringify({ p1: 1, p2: 2 }, null, 2);
/*
"{
  "p1": 1,
  "p2": 2
}"
*/
```
+ 3.4 参数对象的toJSON()方法
+ 如果参数对象有自定义的toJSON()方法，那么JSON.stringify()会使用这个方法的返回值作为参数，而忽略原对象的其他属性。
+ 下面是一个普通的对象。
```
var user = {
  firstName: '三',
  lastName: '张',

  get fullName(){
    return this.lastName + this.firstName;
  }
};

JSON.stringify(user)
// "{"firstName":"三","lastName":"张","fullName":"张三"}"
```
+ 现在，为这个对象加上toJSON()方法。
```
var user = {
  firstName: '三',
  lastName: '张',

  get fullName(){
    return this.lastName + this.firstName;
  },

  toJSON: function () {
    return {
      name: this.lastName + this.firstName
    };
  }
};

JSON.stringify(user)
// "{"name":"张三"}"
```
+ 上面代码中，JSON.stringify()发现参数对象有toJSON()方法，就直接使用这个方法的返回值作为参数，而忽略原对象的其他参数。
+ Date对象就有一个自己的toJSON()方法。
```
var date = new Date('2015-01-01');
date.toJSON() // "2015-01-01T00:00:00.000Z"
JSON.stringify(date) // ""2015-01-01T00:00:00.000Z""
```
+ 上面代码中，JSON.stringify()发现处理的是Date对象实例，就会调用这个实例对象的toJSON()方法，将该方法的返回值作为参数。
+ toJSON()方法的一个应用是，将正则对象自动转为字符串。因为JSON.stringify()默认不能转换正则对象，但是设置了toJSON()方法以后，就可以转换正则对象了。
```
var obj = {
  reg: /foo/
};

// 不设置 toJSON 方法时
JSON.stringify(obj) // "{"reg":{}}"

// 设置 toJSON 方法时
RegExp.prototype.toJSON = RegExp.prototype.toString;
JSON.stringify(/foo/) // ""/foo/""
```
+ 上面代码在正则对象的原型上面部署了toJSON()方法，将其指向toString()方法，因此转换成 JSON 格式时，正则对象就先调用toJSON()方法转为字符串，然后再被JSON.stringify()方法处理。
##### 4、JSON.parse()
+ JSON.parse()方法用于将 JSON 字符串转换成对应的值。
```
JSON.parse('{}') // {}
JSON.parse('true') // true
JSON.parse('"foo"') // "foo"
JSON.parse('[1, 5, "false"]') // [1, 5, "false"]
JSON.parse('null') // null

var o = JSON.parse('{"name": "张三"}');
o.name // 张三
```
+ 如果传入的字符串不是有效的 JSON 格式，JSON.parse()方法将报错。
```
JSON.parse("'String'") // illegal single quotes
// SyntaxError: Unexpected token ILLEGAL
```
+ 上面代码中，双引号字符串中是一个单引号字符串，因为单引号字符串不符合 JSON 格式，所以报错。
+ 为了处理解析错误，可以将JSON.parse()方法放在try...catch代码块中。
```
try {
  JSON.parse("'String'");
} catch(e) {
  console.log('parsing error');
}
```
+ JSON.parse()方法可以接受一个处理函数，作为第二个参数，用法与JSON.stringify()方法类似。
```
function f(key, value) {
  if (key === 'a') {
    return value + 10;
  }
  return value;
}

JSON.parse('{"a": 1, "b": 2}', f)
// {a: 11, b: 2}
```
+ 上面代码中，JSON.parse()的第二个参数是一个函数，如果键名是a，该函数会将键值加上10。

### 六、面向对象编程
#### 1、 实例对象与 new 命令
+ 1、对象是什么
+ 面向对象编程（Object Oriented Programming，缩写为 OOP）是目前主流的编程范式。它将真实世界各种复杂的关系，抽象为一个个对象，然后由对象之间的分工与合作，完成对真实世界的模拟。
+ 每一个对象都是功能中心，具有明确分工，可以完成接受信息、处理数据、发出信息等任务。对象可以复用，通过继承机制还可以定制。因此，面向对象编程具有灵活、代码可复用、高度模块化等特点，容易维护和开发，比起由一系列函数或指令组成的传统的过程式编程（procedural programming），更适合多人合作的大型软件项目。
+ 那么，“对象”（object）到底是什么？我们从两个层次来理解。
+ （1）对象是单个实物的抽象。
+ 一本书、一辆汽车、一个人都可以是对象，一个数据库、一张网页、一个远程服务器连接也可以是对象。当实物被抽象成对象，实物之间的关系就变成了对象之间的关系，从而就可以模拟现实情况，针对对象进行编程。
+ （2）对象是一个容器，封装了属性（property）和方法（method）。
+ 属性是对象的状态，方法是对象的行为（完成某种任务）。比如，我们可以把动物抽象为animal对象，使用“属性”记录具体是哪一种动物，使用“方法”表示动物的某种行为（奔跑、捕猎、休息等等）。

+ 2、构造函数
+ 面向对象编程的第一步，就是要生成对象。前面说过，对象是单个实物的抽象。通常需要一个模板，表示某一类实物的共同特征，然后对象根据这个模板生成。
+ 典型的面向对象编程语言（比如 C++ 和 Java），都有“类”（class）这个概念。所谓“类”就是对象的模板，对象就是“类”的实例。但是，JavaScript 语言的对象体系，不是基于“类”的，而是基于构造函数（constructor）和原型链（prototype）。
+ JavaScript 语言使用构造函数（constructor）作为对象的模板。所谓”构造函数”，就是专门用来生成实例对象的函数。它就是对象的模板，描述实例对象的基本结构。一个构造函数，可以生成多个实例对象，这些实例对象都有相同的结构。
+ 构造函数就是一个普通的函数，但具有自己的特征和用法。
```
var Vehicle = function () {
  this.price = 1000;
};
```
+ 上面代码中，Vehicle就是构造函数。为了与普通函数区别，构造函数名字的第一个字母通常大写。
+ 构造函数的特点有两个:
+ （1）函数体内部使用了this关键字，代表了所要生成的对象实例。
+ （2）生成对象的时候，必须使用new命令。

+ 3、new 命令
+ 3.1 基本用法
+ new命令的作用，就是执行构造函数，返回一个实例对象。
```
var Vehicle = function () {
  this.price = 1000;
};

var v = new Vehicle();
v.price // 1000
```
+ 使用new命令时，根据需要，构造函数也可以接受参数。
```
var Vehicle = function (p) {
  this.price = p;
};

var v = new Vehicle(500);
```
+ new命令本身就可以执行构造函数，所以后面的构造函数可以带括号，也可以不带括号。下面两行代码是等价的，但是为了表示这里是函数调用，推荐使用括号。
```
// 推荐的写法
var v = new Vehicle();
// 不推荐的写法
var v = new Vehicle;
```
+ 一个很自然的问题是，如果忘了使用new命令，直接调用构造函数会发生什么事？
+ 这种情况下，构造函数就变成了普通函数，并不会生成实例对象。而且由于后面会说到的原因，this这时代表全局对象，将造成一些意想不到的结果。
```
var Vehicle = function (){
  this.price = 1000;
};

var v = Vehicle();
v // undefined
price // 1000
```
+ 上面代码中，调用Vehicle构造函数时，忘了加上new命令。结果，变量v变成了undefined，而price属性变成了全局变量。因此，应该非常小心，避免不使用new命令、直接调用构造函数
+ 为了保证构造函数必须与new命令一起使用，一个解决办法是，构造函数内部使用严格模式，即第一行加上use strict。这样的话，一旦忘了使用new命令，直接调用构造函数就会报错。
```
function Fubar(foo, bar){
  'use strict';
  this._foo = foo;
  this._bar = bar;
}
Fubar()
// TypeError: Cannot set property '_foo' of undefined
```
+ 3.2 new 命令的原理
+ 使用new命令时，它后面的函数依次执行下面的步骤。
```
1、创建一个空对象，作为将要返回的对象实例。
2、将这个空对象的原型，指向构造函数的prototype属性。
3、将这个空对象赋值给函数内部的this关键字。
4、开始执行构造函数内部的代码。
```
+ 也就是说，构造函数内部，this指的是一个新生成的空对象，所有针对this的操作，都会发生在这个空对象上。构造函数之所以叫“构造函数”，就是说这个函数的目的，就是操作一个空对象（即this对象），将其“构造”为需要的样子。
+ 如果构造函数内部有return语句，而且return后面跟着一个对象，new命令会返回return语句指定的对象；否则，就会不管return语句，返回this对象。
```
var Vehicle = function () {
  this.price = 1000;
  return 1000;
};

(new Vehicle()) === 1000
// false
```
+ 上面代码中，构造函数Vehicle的return语句返回一个数值。这时，new命令就会忽略这个return语句，返回“构造”后的this对象。
+ 但是，如果return语句返回的是一个跟this无关的新对象，new命令会返回这个新对象，而不是this对象。这一点需要特别引起注意。
```
var Vehicle = function (){
  this.price = 1000;
  return { price: 2000 };
};

(new Vehicle()).price
// 2000
```
+ 上面代码中，构造函数Vehicle的return语句，返回的是一个新对象。new命令会返回这个对象，而不是this对象。
+ 另一方面，如果对普通函数（内部没有this关键字的函数）使用new命令，则会返回一个空对象。
```
function getMessage() {
  return 'this is a message';
}

var msg = new getMessage();

msg // {}
typeof msg // "object"
```
+ 上面代码中，getMessage是一个普通函数，返回一个字符串。对它使用new命令，会得到一个空对象。这是因为new命令总是返回一个对象，要么是实例对象，要么是return语句指定的对象。本例中，return语句返回的是字符串，所以new命令就忽略了该语句。
+ new命令简化的内部流程，可以用下面的代码表示。
```
function _new(/* 构造函数 */ constructor, /* 构造函数参数 */ params) {
  // 将 arguments 对象转为数组
  var args = [].slice.call(arguments);
  // 取出构造函数
  var constructor = args.shift();
  // 创建一个空对象，继承构造函数的 prototype 属性
  var context = Object.create(constructor.prototype);
  // 执行构造函数
  var result = constructor.apply(context, args);
  // 如果返回结果是对象，就直接返回，否则返回 context 对象
  return (typeof result === 'object' && result != null) ? result : context;
}

// 实例
var actor = _new(Person, '张三', 28);
```
+ 3.3 new.target
+ 函数内部可以使用new.target属性。如果当前函数是new命令调用，new.target指向当前函数，否则为undefined。
```
function f() {
  console.log(new.target === f);
}

f() // false
new f() // true
```
+ 使用这个属性，可以判断函数调用的时候，是否使用new命令。
```
function f() {
  if (!new.target) {
    throw new Error('请使用 new 命令调用！');
  }
  // ...
}

f() // Uncaught Error: 请使用 new 命令调用！
```
+ 上面代码中，构造函数f调用时，没有使用new命令，就抛出一个错误。

+ 4、Object.create() 创建实例对象
+ 构造函数作为模板，可以生成实例对象。但是，有时拿不到构造函数，只能拿到一个现有的对象。我们希望以这个现有的对象作为模板，生成新的实例对象，这时就可以使用Object.create()方法。
```
var person1 = {
  name: '张三',
  age: 38,
  greeting: function() {
    console.log('Hi! I\'m ' + this.name + '.');
  }
};

var person2 = Object.create(person1);

person2.name // 张三
person2.greeting() // Hi! I'm 张三.
```
#### 2、 this 关键字
1、涵义
+ this关键字是一个非常重要的语法点。毫不夸张地说，不理解它的含义，大部分开发任务都无法完成。
+ this可以用在构造函数之中，表示实例对象。除此之外，this还可以用在别的场合。但不管是什么场合，this都有一个共同点：它总是返回一个对象。
+ 简单说，this就是属性或方法“当前”所在的对象。
+ 情况一：纯粹的函数调用
+ 这是函数的最通常用法，属于全局性调用，因此this就代表全局对象。请看下面这段代码，它的运行结果是1。
```
var x = 1;
function test() {
   console.log(this.x);
}
test();  // 1

```
+ 情况二：作为对象方法的调用
+ 函数还可以作为某个对象的方法调用，这时this就指这个上级对象。
```

function test() {
  console.log(this.x);
}
var obj = {};
obj.x = 1;
obj.m = test;
obj.m(); // 1
```
+ 情况三 作为构造函数调用
+ 所谓构造函数，就是通过这个函数，可以生成一个新对象。这时，this就指这个新对象。
```
function test() {
　this.x = 1;
}

var obj = new test();
obj.x // 1
```
+ 运行结果为1。为了表明这时this不是全局对象，我们对代码做一些改变：
```
var x = 2;
function test() {
  this.x = 1;
}

var obj = new test();
x  // 2
```
+ 运行结果为2，表明全局变量x的值根本没变。
+ 情况四 apply 调用
+ apply()是函数的一个方法，作用是改变函数的调用对象。它的第一个参数就表示改变后的调用这个函数的对象。因此，这时this指的就是这第一个参数。
```
var x = 0;
function test() {
　console.log(this.x);
}

var obj = {};
obj.x = 1;
obj.m = test;
obj.m.apply() // 0
```
+ apply()的参数为空时，默认调用全局对象。因此，这时的运行结果为0，证明this指的是全局对象。
+ 如果把最后一行代码修改为
```
obj.m.apply(obj); //1
```
+ 运行结果就变成了1，证明了这时this代表的是对象obj。

#### 3、 对象的继承
面向对象编程很重要的一个方面，就是对象的继承。A 对象通过继承 B 对象，就能直接拥有 B 对象的所有属性和方法。这对于代码的复用是非常有用的。大部分面向对象的编程语言，都是通过“类”（class）实现对象的继承。传统上，JavaScript 语言的继承不通过 class，而是通过“原型对象”（prototype）实现，本章介绍 JavaScript 的原型链继承。ES6 引入了 class 语法，基于 class 的继承不在这里介绍。

##### 1、原型对象概述
+ 1.1 构造函数的缺点
+ JavaScript 通过构造函数生成新对象，因此构造函数可以视为对象的模板。实例对象的属性和方法，可以定义在构造函数内部。
```
function Cat (name, color) {
  this.name = name;
  this.color = color;
}

var cat1 = new Cat('大毛', '白色');
cat1.name // '大毛'
cat1.color // '白色'
```
+ 上面代码中，Cat函数是一个构造函数，函数内部定义了name属性和color属性，所有实例对象（上例是cat1）都会生成这两个属性，即这两个属性会定义在实例对象上面。
+ 通过构造函数为实例对象定义属性，虽然很方便，但是有一个缺点。同一个构造函数的多个实例之间，无法共享属性，从而造成对系统资源的浪费。
```
function Cat(name, color) {
  this.name = name;
  this.color = color;
  this.meow = function () {
    console.log('喵喵');
  };
}
var cat1 = new Cat('大毛', '白色');
var cat2 = new Cat('二毛', '黑色');
cat1.meow === cat2.meow
// false
```
+ 上面代码中，cat1和cat2是同一个构造函数的两个实例，它们都具有meow方法。由于meow方法是生成在每个实例对象上面，所以两个实例就生成了两次。也就是说，每新建一个实例，就会新建一个meow方法。这既没有必要，又浪费系统资源，因为所有meow方法都是同样的行为，完全应该共享。
+ 这个问题的解决方法，就是 JavaScript 的原型对象（prototype）。
+ 1.2 prototype 属性的作用
+ JavaScript 继承机制的设计思想就是，原型对象的所有属性和方法，都能被实例对象共享。也就是说，如果属性和方法定义在原型上，那么所有实例对象就能共享，不仅节省了内存，还体现了实例对象之间的联系。
+ 下面，先看怎么为对象指定原型。JavaScript 规定，每个函数都有一个prototype属性，指向一个对象。
```
function f() {}
typeof f.prototype // "object"
```
+ 上面代码中，函数f默认具有prototype属性，指向一个对象。对于普通函数来说，该属性基本无用。但是，对于构造函数来说，生成实例的时候，该属性会自动成为实例对象的原型。
```
function Animal(name) {
  this.name = name;
}
Animal.prototype.color = 'white';

var cat1 = new Animal('大毛');
var cat2 = new Animal('二毛');

cat1.color // 'white'
cat2.color // 'white'
```
+ 上面代码中，构造函数Animal的prototype属性，就是实例对象cat1和cat2的原型对象。原型对象上添加一个color属性，结果，实例对象都共享了该属性。
+ 原型对象的属性不是实例对象自身的属性。只要修改原型对象，变动就立刻会体现在所有实例对象上。
```
Animal.prototype.color = 'yellow';

cat1.color // "yellow"
cat2.color // "yellow"
```
+ 上面代码中，原型对象的color属性的值变为yellow，两个实例对象的color属性立刻跟着变了。这是因为实例对象其实没有color属性，都是读取原型对象的color属性。也就是说，当实例对象本身没有某个属性或方法的时候，它会到原型对象去寻找该属性或方法。这就是原型对象的特殊之处。
+ 如果实例对象自身就有某个属性或方法，它就不会再去原型对象寻找这个属性或方法。
```
cat1.color = 'black';

cat1.color // 'black'
cat2.color // 'yellow'
Animal.prototype.color // 'yellow';
```
+ 上面代码中，实例对象cat1的color属性改为black，就使得它不再去原型对象读取color属性，后者的值依然为yellow。
+ 总结一下，原型对象的作用，就是定义所有实例对象共享的属性和方法。这也是它被称为原型对象的原因，而实例对象可以视作从原型对象衍生出来的子对象。
```
Animal.prototype.walk = function () {
  console.log(this.name + ' is walking');
};
```
+ 上面代码中，Animal.prototype对象上面定义了一个walk方法，这个方法将可以在所有Animal实例对象上面调用。
+ 1.3 原型链
+ JavaScript 规定，所有对象都有自己的原型对象（prototype）。一方面，任何一个对象，都可以充当其他对象的原型；另一方面，由于原型对象也是对象，所以它也有自己的原型。因此，就会形成一个“原型链”（prototype chain）：对象到原型，再到原型的原型……
+ 如果一层层地上溯，所有对象的原型最终都可以上溯到Object.prototype，即Object构造函数的prototype属性。也就是说，所有对象都继承了Object.prototype的属性。这就是所有对象都有valueOf和toString方法的原因，因为这是从Object.prototype继承的。
+ 那么，Object.prototype对象有没有它的原型呢？回答是Object.prototype的原型是null。null没有任何属性和方法，也没有自己的原型。因此，原型链的尽头就是null。
```
Object.getPrototypeOf(Object.prototype)
// null
```
+ 上面代码表示，Object.prototype对象的原型是null，由于null没有任何属性，所以原型链到此为止。Object.getPrototypeOf方法返回参数对象的原型，具体介绍请看后文。
+ 读取对象的某个属性时，JavaScript 引擎先寻找对象本身的属性，如果找不到，就到它的原型去找，如果还是找不到，就到原型的原型去找。如果直到最顶层的Object.prototype还是找不到，则返回undefined。如果对象自身和它的原型，都定义了一个同名属性，那么优先读取对象自身的属性，这叫做“覆盖”（overriding）。
+ 注意，一级级向上，在整个原型链上寻找某个属性，对性能是有影响的。所寻找的属性在越上层的原型对象，对性能的影响越大。如果寻找某个不存在的属性，将会遍历整个原型链。
+ 举例来说，如果让构造函数的prototype属性指向一个数组，就意味着实例对象可以调用数组方法。
```
var MyArray = function () {};

MyArray.prototype = new Array();
MyArray.prototype.constructor = MyArray;

var mine = new MyArray();
mine.push(1, 2, 3);
mine.length // 3
mine instanceof Array // true
```
+ 上面代码中，mine是构造函数MyArray的实例对象，由于MyArray.prototype指向一个数组实例，使得mine可以调用数组方法（这些方法定义在数组实例的prototype对象上面）。最后那行instanceof表达式，用来比较一个对象是否为某个构造函数的实例，结果就是证明mine为Array的实例，instanceof运算符的详细解释详见后文。
+ 上面代码还出现了原型对象的constructor属性，这个属性的含义下一节就来解释。
+ 1.4 constructor 属性
+ prototype对象有一个constructor属性，默认指向prototype对象所在的构造函数。
```
function P() {}
P.prototype.constructor === P // true
```
+ 由于constructor属性定义在prototype对象上面，意味着可以被所有实例对象继承。
```
function P() {}
var p = new P();

p.constructor === P // true
p.constructor === P.prototype.constructor // true
p.hasOwnProperty('constructor') // false
```
+ 上面代码中，p是构造函数P的实例对象，但是p自身没有constructor属性，该属性其实是读取原型链上面的P.prototype.constructor属性。
+ constructor属性的作用是，可以得知某个实例对象，到底是哪一个构造函数产生的。
```
function F() {};
var f = new F();

f.constructor === F // true
f.constructor === RegExp // false
```
+ 上面代码中，constructor属性确定了实例对象f的构造函数是F，而不是RegExp。
+ 另一方面，有了constructor属性，就可以从一个实例对象新建另一个实例。
```
function Constr() {}
var x = new Constr();

var y = new x.constructor();
y instanceof Constr // true
```
+ 上面代码中，x是构造函数Constr的实例，可以从x.constructor间接调用构造函数。这使得在实例方法中，调用自身的构造函数成为可能。
```
Constr.prototype.createCopy = function () {
  return new this.constructor();
};
```
+ 上面代码中，createCopy方法调用构造函数，新建另一个实例。
+ constructor属性表示原型对象与构造函数之间的关联关系，如果修改了原型对象，一般会同时修改constructor属性，防止引用的时候出错。
```
function Person(name) {
  this.name = name;
}

Person.prototype.constructor === Person // true

Person.prototype = {
  method: function () {}
};

Person.prototype.constructor === Person // false
Person.prototype.constructor === Object // true
```
+ 上面代码中，构造函数Person的原型对象改掉了，但是没有修改constructor属性，导致这个属性不再指向Person。由于Person的新原型是一个普通对象，而普通对象的constructor属性指向Object构造函数，导致Person.prototype.constructor变成了Object。
+ 所以，修改原型对象时，一般要同时修改constructor属性的指向。
```
// 坏的写法
C.prototype = {
  method1: function (...) { ... },
  // ...
};

// 好的写法
C.prototype = {
  constructor: C,
  method1: function (...) { ... },
  // ...
};

// 更好的写法
C.prototype.method1 = function (...) { ... };
```
+ 上面代码中，要么将constructor属性重新指向原来的构造函数，要么只在原型对象上添加方法，这样可以保证instanceof运算符不会失真。
+ 如果不能确定constructor属性是什么函数，还有一个办法：通过name属性，从实例得到构造函数的名称。
```
function Foo() {}
var f = new Foo();
f.constructor.name // "Foo"
```
##### 2、instanceof 运算符
+ instanceof运算符返回一个布尔值，表示对象是否为某个构造函数的实例。
```
var v = new Vehicle();
v instanceof Vehicle // true
```
+ 上面代码中，对象v是构造函数Vehicle的实例，所以返回true。
+ instanceof运算符的左边是实例对象，右边是构造函数。它会检查右边构造函数的原型对象（prototype），是否在左边对象的原型链上。因此，下面两种写法是等价的。
```
v instanceof Vehicle
// 等同于
Vehicle.prototype.isPrototypeOf(v)
```
+ 上面代码中，Vehicle是对象v的构造函数，它的原型对象是Vehicle.prototype，isPrototypeOf()方法是 JavaScript 提供的原生方法，用于检查某个对象是否为另一个对象的原型，详细解释见后文。
+ 由于instanceof检查整个原型链，因此同一个实例对象，可能会对多个构造函数都返回true。
```
var d = new Date();
d instanceof Date // true
d instanceof Object // true
```
+ 上面代码中，d同时是Date和Object的实例，因此对这两个构造函数都返回true。
+ 由于任意对象（除了null）都是Object的实例，所以instanceof运算符可以判断一个值是否为非null的对象。
```
var obj = { foo: 123 };
obj instanceof Object // true
null instanceof Object // false
```
+ 上面代码中，除了null，其他对象的instanceOf Object的运算结果都是true。
+ instanceof的原理是检查右边构造函数的prototype属性，是否在左边对象的原型链上。有一种特殊情况，就是左边对象的原型链上，只有null对象。这时，instanceof判断会失真。
```
var obj = Object.create(null);
typeof obj // "object"
obj instanceof Object // false
```
+ instanceof运算符的一个用处，是判断值的类型。
```
var x = [1, 2, 3];
var y = {};
x instanceof Array // true
y instanceof Object // true
```
+ 注意，instanceof运算符只能用于对象，不适用原始类型的值。
```
var s = 'hello';
s instanceof String // false
```
+ 上面代码中，字符串不是String对象的实例（因为字符串不是对象），所以返回false。
+ 此外，对于undefined和null，instanceof运算符总是返回false。
```
undefined instanceof Object // false
null instanceof Object // false
```
##### 3、构造函数的继承
+ 让一个构造函数继承另一个构造函数，是非常常见的需求。这可以分成两步实现。第一步是在子类的构造函数中，调用父类的构造函数。
```
function Sub(value) {
  Super.call(this);
  this.prop = value;
}
```
+ 上面代码中，Sub是子类的构造函数，this是子类的实例。在实例上调用父类的构造函数Super，就会让子类实例具有父类实例的属性。
+ 第二步，是让子类的原型指向父类的原型，这样子类就可以继承父类原型。
```
Sub.prototype = Object.create(Super.prototype);
Sub.prototype.constructor = Sub;
Sub.prototype.method = '...';
```
+ 上面代码中，Sub.prototype是子类的原型，要将它赋值为Object.create(Super.prototype)，而不是直接等于Super.prototype。否则后面两行对Sub.prototype的操作，会连父类的原型Super.prototype一起修改掉。
+ 另外一种写法是Sub.prototype等于一个父类实例。
```
Sub.prototype = new Super();
```
+ 上面这种写法也有继承的效果，但是子类会具有父类实例的方法。有时，这可能不是我们需要的，所以不推荐使用这种写法。
+ 举例来说，下面是一个Shape构造函数。
```
function Shape() {
  this.x = 0;
  this.y = 0;
}

Shape.prototype.move = function (x, y) {
  this.x += x;
  this.y += y;
  console.info('Shape moved.');
};
```
+ 我们需要让Rectangle构造函数继承Shape。
```
// 第一步，子类继承父类的实例
function Rectangle() {
  Shape.call(this); // 调用父类构造函数
}
// 另一种写法
function Rectangle() {
  this.base = Shape;
  this.base();
}

// 第二步，子类继承父类的原型
Rectangle.prototype = Object.create(Shape.prototype);
Rectangle.prototype.constructor = Rectangle;
```
+ 采用这样的写法以后，instanceof运算符会对子类和父类的构造函数，都返回true。
```
var rect = new Rectangle();
rect instanceof Rectangle  // true
rect instanceof Shape  // true
```
+ 上面代码中，子类是整体继承父类。有时只需要单个方法的继承，这时可以采用下面的写法。
```
ClassB.prototype.print = function() {
  ClassA.prototype.print.call(this);
  // some code
}
```
+ 上面代码中，子类B的print方法先调用父类A的print方法，再部署自己的代码。这就等于继承了父类A的print方法。

##### 4、多重继承 
+ JavaScript 不提供多重继承功能，即不允许一个对象同时继承多个对象。但是，可以通过变通方法，实现这个功能。
```
function M1() {
  this.hello = 'hello';
}

function M2() {
  this.world = 'world';
}

function S() {
  M1.call(this);
  M2.call(this);
}

// 继承 M1
S.prototype = Object.create(M1.prototype);
// 继承链上加入 M2
Object.assign(S.prototype, M2.prototype);

// 指定构造函数
S.prototype.constructor = S;

var s = new S();
s.hello // 'hello'
s.world // 'world'
```
+ 上面代码中，子类S同时继承了父类M1和M2。这种模式又称为 Mixin（混入）。

#### 4、 Object 对象的相关方法
JavaScript 在Object对象上面，提供了很多相关方法，处理面向对象编程的相关操作。下面介绍这些方法。
##### 1、Object.getPrototypeOf()
Object.getPrototypeOf方法返回参数对象的原型。这是获取原型对象的标准方法。
```
var F = function () {};
var f = new F();
Object.getPrototypeOf(f) === F.prototype // true
```
+ 上面代码中，实例对象f的原型是F.prototype。
+ 下面是几种特殊对象的原型。
```
// 空对象的原型是 Object.prototype
Object.getPrototypeOf({}) === Object.prototype // true

// Object.prototype 的原型是 null
Object.getPrototypeOf(Object.prototype) === null // true

// 函数的原型是 Function.prototype
function f() {}
Object.getPrototypeOf(f) === Function.prototype // true
```
##### 2、Object.setPrototypeOf()
Object.setPrototypeOf方法为参数对象设置原型，返回该参数对象。它接受两个参数，第一个是现有对象，第二个是原型对象。
```
var a = {};
var b = {x: 1};
Object.setPrototypeOf(a, b);

Object.getPrototypeOf(a) === b // true
a.x // 1
```
+ 上面代码中，Object.setPrototypeOf方法将对象a的原型，设置为对象b，因此a可以共享b的属性。
+ new命令可以使用Object.setPrototypeOf方法模拟。
```
var F = function () {
  this.foo = 'bar';
};
var f = new F();
// 等同于
var f = Object.setPrototypeOf({}, F.prototype);
F.call(f);
```
+ 上面代码中，new命令新建实例对象，其实可以分成两步。第一步，将一个空对象的原型设为构造函数的prototype属性（上例是F.prototype）；第二步，将构造函数内部的this绑定这个空对象，然后执行构造函数，使得定义在this上面的方法和属性（上例是this.foo），都转移到这个空对象上。
##### 3、Object.create()
生成实例对象的常用方法是，使用new命令让构造函数返回一个实例。但是很多时候，只能拿到一个实例对象，它可能根本不是由构建函数生成的，那么能不能从一个实例对象，生成另一个实例对象呢？
+ JavaScript 提供了Object.create()方法，用来满足这种需求。该方法接受一个对象作为参数，然后以它为原型，返回一个实例对象。该实例完全继承原型对象的属性。
```
// 原型对象
var A = {
  print: function () {
    console.log('hello');
  }
};

// 实例对象
var B = Object.create(A);

Object.getPrototypeOf(B) === A // true
B.print() // hello
B.print === A.print // true
```
+ 上面代码中，Object.create()方法以A对象为原型，生成了B对象。B继承了A的所有属性和方法。
+ 下面三种方式生成的新对象是等价的。
```
var obj1 = Object.create({});
var obj2 = Object.create(Object.prototype);
var obj3 = new Object();
```
+ 如果想要生成一个不继承任何属性（比如没有toString()和valueOf()方法）的对象，可以将Object.create()的参数设为null。
```
var obj = Object.create(null);
obj.valueOf()
// TypeError: Object [object Object] has no method 'valueOf'
```
+ 上面代码中，对象obj的原型是null，它就不具备一些定义在Object.prototype对象上面的属性，比如valueOf()方法。
+ 使用Object.create()方法的时候，必须提供对象原型，即参数不能为空，或者不是对象，否则会报错。
```
Object.create()
// TypeError: Object prototype may only be an Object or null
Object.create(123)
// TypeError: Object prototype may only be an Object or null
```
+ Object.create()方法生成的新对象，动态继承了原型。在原型上添加或修改任何方法，会立刻反映在新对象之上。
```
var obj1 = { p: 1 };
var obj2 = Object.create(obj1);

obj1.p = 2;
obj2.p // 2
```
+ 上面代码中，修改对象原型obj1会影响到实例对象obj2。
+ 除了对象的原型，Object.create()方法还可以接受第二个参数。该参数是一个属性描述对象，它所描述的对象属性，会添加到实例对象，作为该对象自身的属性。
```
var obj = Object.create({}, {
  p1: {
    value: 123,
    enumerable: true,
    configurable: true,
    writable: true,
  },
  p2: {
    value: 'abc',
    enumerable: true,
    configurable: true,
    writable: true,
  }
});

// 等同于
var obj = Object.create({});
obj.p1 = 123;
obj.p2 = 'abc';
```
+ Object.create()方法生成的对象，继承了它的原型对象的构造函数。
```
function A() {}
var a = new A();
var b = Object.create(a);
b.constructor === A // true
b instanceof A // true
```
+ 上面代码中，b对象的原型是a对象，因此继承了a对象的构造函数A。
##### 4、Object.prototype.isPrototypeOf()
实例对象的isPrototypeOf方法，用来判断该对象是否为参数对象的原型。
```
var o1 = {};
var o2 = Object.create(o1);
var o3 = Object.create(o2);

o2.isPrototypeOf(o3) // true
o1.isPrototypeOf(o3) // true
```
+ 上面代码中，o1和o2都是o3的原型。这表明只要实例对象处在参数对象的原型链上，isPrototypeOf方法都返回true。
```
Object.prototype.isPrototypeOf({}) // true
Object.prototype.isPrototypeOf([]) // true
Object.prototype.isPrototypeOf(/xyz/) // true
Object.prototype.isPrototypeOf(Object.create(null)) // false
```
+ 上面代码中，由于Object.prototype处于原型链的最顶端，所以对各种实例都返回true，只有直接继承自null的对象除外。
##### 5、Object.prototype.__proto__
实例对象的__proto__属性（前后各两个下划线），返回该对象的原型。该属性可读写。
```
var obj = {};
var p = {};
obj.__proto__ = p;
Object.getPrototypeOf(obj) === p // true
```
+ 上面代码通过__proto__属性，将p对象设为obj对象的原型。
##### 6、获取原型对象方法的比较
```
var obj = new Object();
obj.__proto__ === Object.prototype
// true
obj.__proto__ === obj.constructor.prototype
// true
```
+ 上面代码首先新建了一个对象obj，它的__proto__属性，指向构造函数（Object或obj.constructor）的prototype属性。
+ 因此，获取实例对象obj的原型对象，有三种方法。
```
obj.__proto__
obj.constructor.prototype
Object.getPrototypeOf(obj)
```
+ 上面三种方法之中，前两种都不是很可靠。__proto__属性只有浏览器才需要部署，其他环境可以不部署。而obj.constructor.prototype在手动改变原型对象时，可能会失效。
+ 因此，推荐使用第三种Object.getPrototypeOf方法，获取原型对象。
##### 7、Object.getOwnPropertyNames()
Object.getOwnPropertyNames方法返回一个数组，成员是参数对象本身的所有属性的键名，不包含继承的属性键名。
```
Object.getOwnPropertyNames(Date)
// ["parse", "arguments", "UTC", "caller", "name", "prototype", "now", "length"]
```
+ 上面代码中，Object.getOwnPropertyNames方法返回Date所有自身的属性名。
+ 对象本身的属性之中，有的是可以遍历的（enumerable），有的是不可以遍历的。Object.getOwnPropertyNames方法返回所有键名，不管是否可以遍历。只获取那些可以遍历的属性，使用Object.keys方法。
```
Object.keys(Date) // []
```
+ 上面代码表明，Date对象所有自身的属性，都是不可以遍历的。
##### 8、Object.prototype.hasOwnProperty()
对象实例的hasOwnProperty方法返回一个布尔值，用于判断某个属性定义在对象自身，还是定义在原型链上。
```
Date.hasOwnProperty('length') // true
Date.hasOwnProperty('toString') // false
```
+ 上面代码表明，Date.length（构造函数Date可以接受多少个参数）是Date自身的属性，Date.toString是继承的属性。
+ 另外，hasOwnProperty方法是 JavaScript 之中唯一一个处理对象属性时，不会遍历原型链的方法。
##### 9、in 运算符和 for...in 循环 
in运算符返回一个布尔值，表示一个对象是否具有某个属性。它不区分该属性是对象自身的属性，还是继承的属性。
```
'length' in Date // true
'toString' in Date // true
```
+ in运算符常用于检查一个属性是否存在。
+ 获得对象的所有可遍历属性（不管是自身的还是继承的），可以使用for...in循环。
```
var o1 = { p1: 123 };

var o2 = Object.create(o1, {
  p2: { value: "abc", enumerable: true }
});

for (p in o2) {
  console.info(p);
}
// p2
// p1
```
+ 上面代码中，对象o2的p2属性是自身的，p1属性是继承的。这两个属性都会被for...in循环遍历。
+ 为了在for...in循环中获得对象自身的属性，可以采用hasOwnProperty方法判断一下。
```
for ( var name in object ) {
  if ( object.hasOwnProperty(name) ) {
    /* loop code */
  }
}
```
+ 获得对象的所有属性（不管是自身的还是继承的，也不管是否可枚举），可以使用下面的函数。
```
function inheritedPropertyNames(obj) {
  var props = {};
  while(obj) {
    Object.getOwnPropertyNames(obj).forEach(function(p) {
      props[p] = true;
    });
    obj = Object.getPrototypeOf(obj);
  }
  return Object.getOwnPropertyNames(props);
}
```
+ 上面代码依次获取obj对象的每一级原型对象“自身”的属性，从而获取obj对象的“所有”属性，不管是否可遍历。
+ 下面是一个例子，列出Date对象的所有属性。
```
inheritedPropertyNames(Date)
// [
//  "caller",
//  "constructor",
//  "toString",
//  "UTC",
//  ...
// ]
```
##### 10、对象的拷贝
如果要拷贝一个对象，需要做到下面两件事情。
+ 1、确保拷贝后的对象，与原对象具有同样的原型。
+ 2、确保拷贝后的对象，与原对象具有同样的实例属性。
+ 下面就是根据上面两点，实现的对象拷贝函数。
```
function copyObject(orig) {
  var copy = Object.create(Object.getPrototypeOf(orig));
  copyOwnPropertiesFrom(copy, orig);
  return copy;
}

function copyOwnPropertiesFrom(target, source) {
  Object
    .getOwnPropertyNames(source)
    .forEach(function (propKey) {
      var desc = Object.getOwnPropertyDescriptor(source, propKey);
      Object.defineProperty(target, propKey, desc);
    });
  return target;
}
```
+ 另一种更简单的写法，是利用 ES2017 才引入标准的Object.getOwnPropertyDescriptors方法。
```
function copyObject(orig) {
  return Object.create(
    Object.getPrototypeOf(orig),
    Object.getOwnPropertyDescriptors(orig)
  );
}
```

#### 5、 严格模式
+ 除了正常的运行模式，JavaScript 还有第二种运行模式：严格模式（strict mode）。顾名思义，这种模式采用更加严格的 JavaScript 语法。
+ 同样的代码，在正常模式和严格模式中，可能会有不一样的运行结果。一些在正常模式下可以运行的语句，在严格模式下将不能运行。
##### 1、设计目的
+ 早期的 JavaScript 语言有很多设计不合理的地方，但是为了兼容以前的代码，又不能改变老的语法，只能不断添加新的语法，引导程序员使用新语法。
+ 严格模式是从 ES5 进入标准的，主要目的有以下几个。
+ 1、明确禁止一些不合理、不严谨的语法，减少 JavaScript 语言的一些怪异行为。
+ 2、增加更多报错的场合，消除代码运行的一些不安全之处，保证代码运行的安全。
+ 3、提高编译器效率，增加运行速度。
+ 4、为未来新版本的 JavaScript 语法做好铺垫。
+ 总之，严格模式体现了 JavaScript 更合理、更安全、更严谨的发展方向。
##### 2、启用方法
+ 进入严格模式的标志，是一行字符串use strict。
```
'use strict';
```
+ 老版本的引擎会把它当作一行普通字符串，加以忽略。新版本的引擎就会进入严格模式。
+ 严格模式可以用于整个脚本，也可以只用于单个函数。

### 七、异步操作
#### 1、异步操作概述
##### 1.1、单线程模型
+ 单线程模型指的是，JavaScript 只在一个线程上运行。也就是说，JavaScript 同时只能执行一个任务，其他任务都必须在后面排队等待。
+ 注意，JavaScript 只在一个线程上运行，不代表 JavaScript 引擎只有一个线程。事实上，JavaScript 引擎有多个线程，单个脚本只能在一个线程上运行（称为主线程），其他线程都是在后台配合。

##### 1.2、同步任务和异步任务
+ 程序里面所有的任务，可以分成两类：同步任务（synchronous）和异步任务（asynchronous）。
+ 同步任务是那些没有被引擎挂起、在主线程上排队执行的任务。只有前一个任务执行完毕，才能执行后一个任务。
+ 异步任务是那些被引擎放在一边，不进入主线程、而进入任务队列的任务。只有引擎认为某个异步任务可以执行了（比如 Ajax 操作从服务器得到了结果），该任务（采用回调函数的形式）才会进入主线程执行。排在异步任务后面的代码，不用等待异步任务结束会马上运行，也就是说，异步任务不具有“堵塞”效应。
+ 举例来说，Ajax 操作可以当作同步任务处理，也可以当作异步任务处理，由开发者决定。如果是同步任务，主线程就等着 Ajax 操作返回结果，再往下执行；如果是异步任务，主线程在发出 Ajax 请求以后，就直接往下执行，等到 Ajax 操作有了结果，主线程再执行对应的回调函数。

##### 1.3、任务队列和事件循环
+ JavaScript 运行时，除了一个正在运行的主线程，引擎还提供一个任务队列（task queue），里面是各种需要当前程序处理的异步任务。（实际上，根据异步任务的类型，存在多个任务队列。为了方便理解，这里假设只存在一个队列。）
+ 首先，主线程会去执行所有的同步任务。等到同步任务全部执行完，就会去看任务队列里面的异步任务。如果满足条件，那么异步任务就重新进入主线程开始执行，这时它就变成同步任务了。等到执行完，下一个异步任务再进入主线程开始执行。一旦任务队列清空，程序就结束执行。
+ 异步任务的写法通常是回调函数。一旦异步任务重新进入主线程，就会执行对应的回调函数。如果一个异步任务没有回调函数，就不会进入任务队列，也就是说，不会重新进入主线程，因为没有用回调函数指定下一步的操作。
+ JavaScript 引擎怎么知道异步任务有没有结果，能不能进入主线程呢？答案就是引擎在不停地检查，一遍又一遍，只要同步任务执行完了，引擎就会去检查那些挂起来的异步任务，是不是可以进入主线程了。这种循环检查的机制，就叫做事件循环（Event Loop）。

##### 1.4、异步操作的模式
+ 1、回调函数
+ 回调函数是异步操作最基本的方法。
```
function f1(callback) {
  // ...
  callback();
}

function f2() {
  // ...
}
f1(f2);
```
+ 回调函数的优点是简单、容易理解和实现，缺点是不利于代码的阅读和维护，各个部分之间高度耦合（coupling），使得程序结构混乱、流程难以追踪（尤其是多个回调函数嵌套的情况），而且每个任务只能指定一个回调函数。

+ 2、时间监听
+ 另一种思路是采用事件驱动模式。异步任务的执行不取决于代码的顺序，而取决于某个事件是否发生。
+ 还是以f1和f2为例。首先，为f1绑定一个事件（这里采用的 jQuery 的写法）。
```
f1.on('done', f2);
```
+ 上面这行代码的意思是，当f1发生done事件，就执行f2。然后，对f1进行改写：
```
function f1() {
  setTimeout(function () {
    // ...
    f1.trigger('done');
  }, 1000);
}
```
+ 上面代码中，f1.trigger('done')表示，执行完成后，立即触发done事件，从而开始执行f2。
+ 这种方法的优点是比较容易理解，可以绑定多个事件，每个事件可以指定多个回调函数，而且可以“去耦合”（decoupling），有利于实现模块化。缺点是整个程序都要变成事件驱动型，运行流程会变得很不清晰。阅读代码的时候，很难看出主流程。

+ 3、发布与订阅
+ 事件完全可以理解成“信号”，如果存在一个“信号中心”，某个任务执行完成，就向信号中心“发布”（publish）一个信号，其他任务可以向信号中心“订阅”（subscribe）这个信号，从而知道什么时候自己可以开始执行。这就叫做”发布/订阅模式”（publish-subscribe pattern），又称“观察者模式”（observer pattern）。

#### 2、定时器
##### 2.1、setTimeout() 
setTimeout函数用来指定某个函数或某段代码，在多少毫秒之后执行。它返回一个整数，表示定时器的编号，以后可以用来取消这个定时器。
```
var timerId = setTimeout(func|code, delay);
```
+ 上面代码中，setTimeout函数接受两个参数，第一个参数func|code是将要推迟执行的函数名或者一段代码，第二个参数delay是推迟执行的毫秒数。
```
console.log(1);
setTimeout('console.log(2)',1000);
console.log(3);
// 1
// 3
// 2
```
+ 上面代码会先输出1和3，然后等待1000毫秒再输出2。注意，console.log(2)必须以字符串的形式，作为setTimeout的参数。
+ 如果推迟执行的是函数，就直接将函数名，作为setTimeout的参数。
```
function f() {
  console.log(2);
}
setTimeout(f, 1000);
```
+ setTimeout的第二个参数如果省略，则默认为0。
```
setTimeout(f)
// 等同于
setTimeout(f, 0)
```
+ 除了前两个参数，setTimeout还允许更多的参数。它们将依次传入推迟执行的函数（回调函数）。
```
setTimeout(function (a,b) {
  console.log(a + b);
}, 1000, 1, 1);
```
+ 上面代码中，setTimeout共有4个参数。最后那两个参数，将在1000毫秒之后回调函数执行时，作为回调函数的参数。
+ 还有一个需要注意的地方，如果回调函数是对象的方法，那么setTimeout使得方法内部的this关键字指向全局环境，而不是定义时所在的那个对象。
```
var x = 1;
var obj = {
  x: 2,
  y: function () {
    console.log(this.x);
  }
};
setTimeout(obj.y, 1000) // 1
```
+ 上面代码输出的是1，而不是2。因为当obj.y在1000毫秒后运行时，this所指向的已经不是obj了，而是全局环境。
+ 为了防止出现这个问题，一种解决方法是将obj.y放入一个函数。
```
var x = 1;
var obj = {
  x: 2,
  y: function () {
    console.log(this.x);
  }
};
setTimeout(function () {
  obj.y();
}, 1000);
// 2
```
+ 上面代码中，obj.y放在一个匿名函数之中，这使得obj.y在obj的作用域执行，而不是在全局作用域内执行，所以能够显示正确的值。
+ 另一种解决方法是，使用bind方法，将obj.y这个方法绑定在obj上面。
```
var x = 1;
var obj = {
  x: 2,
  y: function () {
    console.log(this.x);
  }
};
setTimeout(obj.y.bind(obj), 1000)
// 2
```
##### 2.2、setInterval()
setInterval函数的用法与setTimeout完全一致，区别仅仅在于setInterval指定某个任务每隔一段时间就执行一次，也就是无限次的定时执行。
```
var i = 1
var timer = setInterval(function() {
  console.log(2);
}, 1000)
```
+ 上面代码中，每隔1000毫秒就输出一个2，会无限运行下去，直到关闭当前窗口。
+ 与setTimeout一样，除了前两个参数，setInterval方法还可以接受更多的参数，它们会传入回调函数。
+ 下面是一个通过setInterval方法实现网页动画的例子。
```
var div = document.getElementById('someDiv');
var opacity = 1;
var fader = setInterval(function() {
  opacity -= 0.1;
  if (opacity >= 0) {
    div.style.opacity = opacity;
  } else {
    clearInterval(fader);
  }
}, 100);
```
+ 上面代码每隔100毫秒，设置一次div元素的透明度，直至其完全透明为止。
+ 为了确保两次执行之间有固定的间隔，可以不用setInterval，而是每次执行结束后，使用setTimeout指定下一次执行的具体时间。
```
var i = 1;
var timer = setTimeout(function f() {
  // ...
  timer = setTimeout(f, 2000);
}, 2000);
```
+ 上面代码可以确保，下一次执行总是在本次执行结束之后的2000毫秒开始。

##### 2.3、clearTimeout()，clearInterval()
setTimeout和setInterval函数，都返回一个整数值，表示计数器编号。将该整数传入clearTimeout和clearInterval函数，就可以取消对应的定时器。
```
var id1 = setTimeout(f, 1000);
var id2 = setInterval(f, 1000);
clearTimeout(id1);
clearInterval(id2);
```
+ 上面代码中，回调函数f不会再执行了，因为两个定时器都被取消了。
+ setTimeout和setInterval返回的整数值是连续的，也就是说，第二个setTimeout方法返回的整数值，将比第一个的整数值大1。
```
function f() {}
setTimeout(f, 1000) // 10
setTimeout(f, 1000) // 11
setTimeout(f, 1000) // 12
```
+ 上面代码中，连续调用三次setTimeout，返回值都比上一次大了1。
+ 利用这一点，可以写一个函数，取消当前所有的setTimeout定时器。
```
(function() {
  // 每轮事件循环检查一次
  var gid = setInterval(clearAllTimeouts, 0);
  function clearAllTimeouts() {
    var id = setTimeout(function() {}, 0);
    while (id > 0) {
      if (id !== gid) {
        clearTimeout(id);
      }
      id--;
    }
  }
})();
```
+ 上面代码中，先调用setTimeout，得到一个计算器编号，然后把编号比它小的计数器全部取消。

##### 2.4、debounce 函数
有时，我们不希望回调函数被频繁调用。比如，用户填入网页输入框的内容，希望通过 Ajax 方法传回服务器，jQuery 的写法如下：
```
$('textarea').on('keydown', ajaxAction);
```
+ 这样写有一个很大的缺点，就是如果用户连续击键，就会连续触发keydown事件，造成大量的 Ajax 通信。这是不必要的，而且很可能产生性能问题。正确的做法应该是，设置一个门槛值，表示两次 Ajax 通信的最小间隔时间。如果在间隔时间内，发生新的keydown事件，则不触发 Ajax 通信，并且重新开始计时。如果过了指定时间，没有发生新的keydown事件，再将数据发送出去。
+ 这种做法叫做 debounce（防抖动）。假定两次 Ajax 通信的间隔不得小于2500毫秒，上面的代码可以改写成下面这样。
```
$('textarea').on('keydown', debounce(ajaxAction, 2500));
function debounce(fn, delay){
  var timer = null; // 声明计时器
  return function() {
    var context = this;
    var args = arguments;
    clearTimeout(timer);
    timer = setTimeout(function () {
      fn.apply(context, args);
    }, delay);
  };
}
```
+ 上面代码中，只要在2500毫秒之内，用户再次击键，就会取消上一次的定时器，然后再新建一个定时器。这样就保证了回调函数之间的调用间隔，至少是2500毫秒。

##### 2.5、运行机制
setTimeout和setInterval的运行机制，是将指定的代码移出本轮事件循环，等到下一轮事件循环，再检查是否到了指定时间。如果到了，就执行对应的代码；如果不到，就继续等待。
+ 这意味着，setTimeout和setInterval指定的回调函数，必须等到本轮事件循环的所有同步任务都执行完，才会开始执行。由于前面的任务到底需要多少时间执行完，是不确定的，所以没有办法保证，setTimeout和setInterval指定的任务，一定会按照预定时间执行。
```
setTimeout(someTask, 100);
veryLongTask();
```
+ 上面代码的setTimeout，指定100毫秒以后运行一个任务。但是，如果后面的veryLongTask函数（同步任务）运行时间非常长，过了100毫秒还无法结束，那么被推迟运行的someTask就只有等着，等到veryLongTask运行结束，才轮到它执行。

#### 3、Promise对象
##### 3.1、概述
Promise 对象是 JavaScript 的异步操作解决方案，为异步操作提供统一接口。它起到代理作用（proxy），充当异步操作与回调函数之间的中介，使得异步操作具备同步操作的接口。Promise 可以让异步操作写起来，就像在写同步操作的流程，而不必一层层地嵌套回调函数。
+ 注意，本章只是 Promise 对象的简单介绍。为了避免与后续教程的重复，更完整的介绍请看《ES6 标准入门》的《Promise 对象》一章。
+ 首先，Promise 是一个对象，也是一个构造函数。
```
function f1(resolve, reject) {
  // 异步代码...
}
var p1 = new Promise(f1);
```
+ 上面代码中，Promise构造函数接受一个回调函数f1作为参数，f1里面是异步操作的代码。然后，返回的p1就是一个 Promise 实例。
+ Promise 的设计思想是，所有异步任务都返回一个 Promise 实例。Promise 实例有一个then方法，用来指定下一步的回调函数。
```
var p1 = new Promise(f1);
p1.then(f2);
```
+ 上面代码中，f1的异步操作执行完成，就会执行f2。
+ 传统的写法可能需要把f2作为回调函数传入f1，比如写成f1(f2)，异步操作完成后，在f1内部调用f2。Promise 使得f1和f2变成了链式写法。不仅改善了可读性，而且对于多层嵌套的回调函数尤其方便。
```
// 传统写法
step1(function (value1) {
  step2(value1, function(value2) {
    step3(value2, function(value3) {
      step4(value3, function(value4) {
        // ...
      });
    });
  });
});

// Promise 的写法
(new Promise(step1))
  .then(step2)
  .then(step3)
  .then(step4);
```
+ 从上面代码可以看到，采用 Promises 以后，程序流程变得非常清楚，十分易读。注意，为了便于理解，上面代码的Promise实例的生成格式，做了简化，真正的语法请参照下文。
+ 总的来说，传统的回调函数写法使得代码混成一团，变得横向发展而不是向下发展。Promise 就是解决这个问题，使得异步流程可以写成同步流程。
+ Promise 原本只是社区提出的一个构想，一些函数库率先实现了这个功能。ECMAScript 6 将其写入语言标准，目前 JavaScript 原生支持 Promise 对象。

##### 3.2、Promise 对象的状态
Promise 对象通过自身的状态，来控制异步操作。Promise 实例具有三种状态。
+ 1、异步操作未完成（pending）
+ 2、异步操作成功（fulfilled）
+ 3、异步操作失败（rejected）
+ 上面三种状态里面，fulfilled和rejected合在一起称为resolved（已定型）。
+ 这三种的状态的变化途径只有两种。
+ 1、从“未完成”到“成功”
+ 2、从“未完成”到“失败”
+ 一旦状态发生变化，就凝固了，不会再有新的状态变化。这也是 Promise 这个名字的由来，它的英语意思是“承诺”，一旦承诺成效，就不得再改变了。这也意味着，Promise 实例的状态变化只可能发生一次。
+ 因此，Promise 的最终结果只有两种。
+ 1、异步操作成功，Promise 实例传回一个值（value），状态变为fulfilled。
+ 2、异步操作失败，Promise 实例抛出一个错误（error），状态变为rejected。

##### 3.3、Promise 构造函数
JavaScript 提供原生的Promise构造函数，用来生成 Promise 实例。
```
var promise = new Promise(function (resolve, reject) {
  // ...

  if (/* 异步操作成功 */){
    resolve(value);
  } else { /* 异步操作失败 */
    reject(new Error());
  }
});
```
+ 上面代码中，Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject。它们是两个函数，由 JavaScript 引擎提供，不用自己实现。
+ resolve函数的作用是，将Promise实例的状态从“未完成”变为“成功”（即从pending变为fulfilled），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去。reject函数的作用是，将Promise实例的状态从“未完成”变为“失败”（即从pending变为rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。
+ 下面是一个例子。
```
function timeout(ms) {
  return new Promise((resolve, reject) => {
    setTimeout(resolve, ms, 'done');
  });
}
timeout(100)
```
+ 上面代码中，timeout(100)返回一个 Promise 实例。100毫秒以后，该实例的状态会变为fulfilled。

##### 3.4、Promise.prototype.then()
Promise 实例的then方法，用来添加回调函数。
+ then方法可以接受两个回调函数，第一个是异步操作成功时（变为fulfilled状态）的回调函数，第二个是异步操作失败（变为rejected）时的回调函数（该参数可以省略）。一旦状态改变，就调用相应的回调函数。
```
var p1 = new Promise(function (resolve, reject) {
  resolve('成功');
});
p1.then(console.log, console.error);
// "成功"

var p2 = new Promise(function (resolve, reject) {
  reject(new Error('失败'));
});
p2.then(console.log, console.error);
// Error: 失败
```
+ 上面代码中，p1和p2都是Promise 实例，它们的then方法绑定两个回调函数：成功时的回调函数console.log，失败时的回调函数console.error（可以省略）。p1的状态变为成功，p2的状态变为失败，对应的回调函数会收到异步操作传回的值，然后在控制台输出。
+ then方法可以链式使用。
```
p1
  .then(step1)
  .then(step2)
  .then(step3)
  .then(
    console.log,
    console.error
  );
```
+ 上面代码中，p1后面有四个then，意味依次有四个回调函数。只要前一步的状态变为fulfilled，就会依次执行紧跟在后面的回调函数。
+ 最后一个then方法，回调函数是console.log和console.error，用法上有一点重要的区别。console.log只显示step3的返回值，而console.error可以显示p1、step1、step2、step3之中任意一个发生的错误。举例来说，如果step1的状态变为rejected，那么step2和step3都不会执行了（因为它们是resolved的回调函数）。Promise 开始寻找，接下来第一个为rejected的回调函数，在上面代码中是console.error。这就是说，Promise 对象的报错具有传递性。

##### 3.5、then() 用法辨析
Promise 的用法，简单说就是一句话：使用then方法添加回调函数。但是，不同的写法有一些细微的差别，请看下面四种写法，它们的差别在哪里？
```
// 写法一
f1().then(function () {
  return f2();
});

// 写法二
f1().then(function () {
  f2();
});

// 写法三
f1().then(f2());

// 写法四
f1().then(f2);
```
+ 为了便于讲解，下面这四种写法都再用then方法接一个回调函数f3。写法一的f3回调函数的参数，是f2函数的运行结果。
```
f1().then(function () {
  return f2();
}).then(f3);
```
+ 写法二的f3回调函数的参数是undefined。
```
f1().then(function () {
  f2();
  return;
}).then(f3);
```
+ 写法三的f3回调函数的参数，是f2函数返回的函数的运行结果。
```
f1().then(f2())
  .then(f3);
```
+ 写法四与写法一只有一个差别，那就是f2会接收到f1()返回的结果。
```
f1().then(f2)
  .then(f3);
```

##### 3.6、小结
Promise 的优点在于，让回调函数变成了规范的链式写法，程序流程可以看得很清楚。它有一整套接口，可以实现许多强大的功能，比如同时执行多个异步操作，等到它们的状态都改变以后，再执行一个回调函数；再比如，为多个回调函数中抛出的错误，统一指定处理方法等等。

而且，Promise 还有一个传统写法没有的好处：它的状态一旦改变，无论何时查询，都能得到这个状态。这意味着，无论何时为 Promise 实例添加回调函数，该函数都能正确执行。所以，你不用担心是否错过了某个事件或信号。如果是传统写法，通过监听事件来执行回调函数，一旦错过了事件，再添加回调函数是不会执行的。

Promise 的缺点是，编写的难度比传统写法高，而且阅读代码也不是一眼可以看懂。你只会看到一堆then，必须自己在then的回调函数里面理清逻辑。

##### 3.7、微任务
Promise 的回调函数属于异步任务，会在同步任务之后执行。
```
new Promise(function (resolve, reject) {
  resolve(1);
}).then(console.log);

console.log(2);
// 2
// 1
```
+ 上面代码会先输出2，再输出1。因为console.log(2)是同步任务，而then的回调函数属于异步任务，一定晚于同步任务执行。
+ 但是，Promise 的回调函数不是正常的异步任务，而是微任务（microtask）。它们的区别在于，正常任务追加到下一轮事件循环，微任务追加到本轮事件循环。这意味着，微任务的执行时间一定早于正常任务。
```
setTimeout(function() {
  console.log(1);
}, 0);

new Promise(function (resolve, reject) {
  resolve(2);
}).then(console.log);

console.log(3);
// 3
// 2
// 1
```
+ 上面代码的输出结果是321。这说明then的回调函数的执行时间，早于setTimeout(fn, 0)。因为then是本轮事件循环执行，setTimeout(fn, 0)在下一轮事件循环开始时执行。

### 八、DOM

#### 1、概述
##### 1.1、DOM
DOM 是 JavaScript 操作网页的接口，全称为“文档对象模型”（Document Object Model）。它的作用是将网页转为一个 JavaScript 对象，从而可以用脚本进行各种操作（比如增删内容）。
+ 浏览器会根据 DOM 模型，将结构化文档（比如 HTML 和 XML）解析成一系列的节点，再由这些节点组成一个树状结构（DOM Tree）。所有的节点和最终的树状结构，都有规范的对外接口。
+ DOM 只是一个接口规范，可以用各种语言实现。所以严格地说，DOM 不是 JavaScript 语法的一部分，但是 DOM 操作是 JavaScript 最常见的任务，离开了 DOM，JavaScript 就无法控制网页。另一方面，JavaScript 也是最常用于 DOM 操作的语言。后面介绍的就是 JavaScript 对 DOM 标准的实现和用法。

##### 1.2、节点
DOM 的最小组成单位叫做节点（node）。文档的树形结构（DOM 树），就是由各种不同类型的节点组成。每个节点可以看作是文档树的一片叶子。
+ 节点的类型有七种：
+ 1、Document：整个文档树的顶层节点
+ 2、DocumentType：doctype标签（比如<!DOCTYPE html>）
+ 3、Element：网页的各种HTML标签（比如<body>、<a>等）
+ 4、Attr：网页元素的属性（比如class="right"）
+ 5、Text：标签之间或标签包含的文本
+ 6、Comment：注释
+ 7、DocumentFragment：文档的片段
+ 浏览器提供一个原生的节点对象Node，上面这七种节点都继承了Node，因此具有一些共同的属性和方法。

##### 1.3、节点树
一个文档的所有节点，按照所在的层级，可以抽象成一种树状结构。这种树状结构就是 DOM 树。它有一个顶层节点，下一层都是顶层节点的子节点，然后子节点又有自己的子节点，就这样层层衍生出一个金字塔结构，又像一棵树。
+ 浏览器原生提供document节点，代表整个文档。
```
document
// 整个文档树
```
+ 文档的第一层有两个节点，第一个是文档类型节点（<!doctype html>），第二个是 HTML 网页的顶层容器标签<html>。后者构成了树结构的根节点（root node），其他 HTML 标签节点都是它的下级节点。
+ 除了根节点，其他节点都有三种层级关系。
+ 1、父节点关系（parentNode）：直接的那个上级节点
+ 2、子节点关系（childNodes）：直接的下级节点
+ 3、同级节点关系（sibling）：拥有同一个父节点的节点
+ DOM 提供操作接口，用来获取这三种关系的节点。比如，子节点接口包括firstChild（第一个子节点）和lastChild（最后一个子节点）等属性，同级节点接口包括nextSibling（紧邻在后的那个同级节点）和previousSibling（紧邻在前的那个同级节点）属性。

#### 2、Node 接口
##### 2.1、属性
+ 1、Node.prototype.nodeType
+ nodeType属性返回一个整数值，表示节点的类型。
```
document.nodeType // 9
```
+ 上面代码中，文档节点的类型值为9。
+ Node 对象定义了几个常量，对应这些类型值。
```
document.nodeType === Node.DOCUMENT_NODE // true
```
+ 上面代码中，文档节点的nodeType属性等于常量Node.DOCUMENT_NODE。
+ 不同节点的nodeType属性值和对应的常量如下。
+ 1、文档节点（document）：9，对应常量Node.DOCUMENT_NODE
+ 2、元素节点（element）：1，对应常量Node.ELEMENT_NODE
+ 3、属性节点（attr）：2，对应常量Node.ATTRIBUTE_NODE
+ 4、文本节点（text）：3，对应常量Node.TEXT_NODE
+ 5、文档片断节点（DocumentFragment）：11，对应常量Node.DOCUMENT_FRAGMENT_NODE
+ 6、文档类型节点（DocumentType）：10，对应常量Node.DOCUMENT_TYPE_NODE
+ 7、注释节点（Comment）：8，对应常量Node.COMMENT_NODE
+ 确定节点类型时，使用nodeType属性是常用方法。
```
var node = document.documentElement.firstChild;
if (node.nodeType === Node.ELEMENT_NODE) {
  console.log('该节点是元素节点');
}
```
+ 2、Node.prototype.nodeName
+ nodeName属性返回节点的名称。
```
// HTML 代码如下
// <div id="d1">hello world</div>
var div = document.getElementById('d1');
div.nodeName // "DIV"
```
+ 上面代码中，元素节点<div>的nodeName属性就是大写的标签名DIV。
+ 不同节点的nodeName属性值如下。
+ 文档节点（document）：#document
+ 元素节点（element）：大写的标签名
+ 属性节点（attr）：属性的名称
+ 文本节点（text）：#text
+ 文档片断节点（DocumentFragment）：#document-fragment
+ 文档类型节点（DocumentType）：文档的类型
+ 注释节点（Comment）：#comment

+ 3、Node.prototype.nodeValue
+ nodeValue属性返回一个字符串，表示当前节点本身的文本值，该属性可读写。
+ 只有文本节点（text）、注释节点（comment）和属性节点（attr）有文本值，因此这三类节点的nodeValue可以返回结果，其他类型的节点一律返回null。同样的，也只有这三类节点可以设置nodeValue属性的值，其他类型的节点设置无效。
```
// HTML 代码如下
// <div id="d1">hello world</div>
var div = document.getElementById('d1');
div.nodeValue // null
div.firstChild.nodeValue // "hello world"
```
+ 上面代码中，div是元素节点，nodeValue属性返回null。div.firstChild是文本节点，所以可以返回文本值。

+ 4、Node.prototype.textContent
+ textContent属性返回当前节点和它的所有后代节点的文本内容。
```
// HTML 代码为
// <div id="divA">This is <span>some</span> text</div>

document.getElementById('divA').textContent
// This is some text
```
+ textContent属性自动忽略当前节点内部的 HTML 标签，返回所有文本内容。
+ 该属性是可读写的，设置该属性的值，会用一个新的文本节点，替换所有原来的子节点。它还有一个好处，就是自动对 HTML 标签转义。这很适合用于用户提供的内容。
```
document.getElementById('foo').textContent = '<p>GoodBye!</p>';
```
+ 上面代码在插入文本时，会将<p>标签解释为文本，而不会当作标签处理。
+ 文档节点（document）和文档类型节点（doctype）的textContent属性为null。如果要读取整个文档的内容，可以使用document.documentElement.textContent。

+ 5、Node.prototype.baseURI
+ baseURI属性返回一个字符串，表示当前网页的绝对路径。浏览器根据这个属性，计算网页上的相对路径的 URL。该属性为只读。
```
// 当前网页的网址为
// http://www.example.com/index.html
document.baseURI
// "http://www.example.com/index.html"
```
+ 如果无法读到网页的 URL，baseURI属性返回null。
+ 该属性的值一般由当前网址的 URL（即window.location属性）决定，但是可以使用 HTML 的<base>标签，改变该属性的值。
```
<base href="http://www.example.com/page.html">
```
+ 设置了以后，baseURI属性就返回<base>标签设置的值。

+ 6、Node.prototype.ownerDocument
+ Node.ownerDocument属性返回当前节点所在的顶层文档对象，即document对象。
```
var d = p.ownerDocument;
d === document // true
```
+ document对象本身的ownerDocument属性，返回null。

+ 7、Node.prototype.nextSibling
+ Node.nextSibling属性返回紧跟在当前节点后面的第一个同级节点。如果当前节点后面没有同级节点，则返回null。
```
// HTML 代码如下
// <div id="d1">hello</div><div id="d2">world</div>
var d1 = document.getElementById('d1');
var d2 = document.getElementById('d2');
d1.nextSibling === d2 // true
```
+ 上面代码中，d1.nextSibling就是紧跟在d1后面的同级节点d2。
+ 注意，该属性还包括文本节点和注释节点（<!-- comment -->）。因此如果当前节点后面有空格，该属性会返回一个文本节点，内容为空格。
+ nextSibling属性可以用来遍历所有子节点。
```
var el = document.getElementById('div1').firstChild;

while (el !== null) {
  console.log(el.nodeName);
  el = el.nextSibling;
}
```
+ 上面代码遍历div1节点的所有子节点。

+ 8、Node.prototype.previousSibling
+ previousSibling属性返回当前节点前面的、距离最近的一个同级节点。如果当前节点前面没有同级节点，则返回null。
```
// HTML 代码如下
// <div id="d1">hello</div><div id="d2">world</div>
var d1 = document.getElementById('d1');
var d2 = document.getElementById('d2');
d2.previousSibling === d1 // true
```
+ 上面代码中，d2.previousSibling就是d2前面的同级节点d1。
+ 注意，该属性还包括文本节点和注释节点。因此如果当前节点前面有空格，该属性会返回一个文本节点，内容为空格。

+ 9、Node.prototype.parentNode
+ parentNode属性返回当前节点的父节点。对于一个节点来说，它的父节点只可能是三种类型：元素节点（element）、文档节点（document）和文档片段节点（documentfragment）。
```
if (node.parentNode) {
  node.parentNode.removeChild(node);
}
```
+ 上面代码中，通过node.parentNode属性将node节点从文档里面移除。
+ 文档节点（document）和文档片段节点（documentfragment）的父节点都是null。另外，对于那些生成后还没插入 DOM 树的节点，父节点也是null。

10、Node.prototype.parentElement 
+ parentElement属性返回当前节点的父元素节点。如果当前节点没有父节点，或者父节点类型不是元素节点，则返回null。
```
if (node.parentElement) {
  node.parentElement.style.color = 'red';
}
```
+ 上面代码中，父元素节点的样式设定了红色。
+ 由于父节点只可能是三种类型：元素节点、文档节点（document）和文档片段节点（documentfragment）。parentElement属性相当于把后两种父节点都排除了。

11、Node.prototype.firstChild，Node.prototype.lastChild
+ firstChild属性返回当前节点的第一个子节点，如果当前节点没有子节点，则返回null。
```
// HTML 代码如下
// <p id="p1"><span>First span</span></p>
var p1 = document.getElementById('p1');
p1.firstChild.nodeName // "SPAN"
```
+ 上面代码中，p元素的第一个子节点是span元素。
+ 注意，firstChild返回的除了元素节点，还可能是文本节点或注释节点。
```
// HTML 代码如下
// <p id="p1">
//   <span>First span</span>
//  </p>
var p1 = document.getElementById('p1');
p1.firstChild.nodeName // "#text"
```
+ 上面代码中，p元素与span元素之间有空白字符，这导致firstChild返回的是文本节点。
+ lastChild属性返回当前节点的最后一个子节点，如果当前节点没有子节点，则返回null。用法与firstChild属性相同。

12、Node.prototype.childNodes
+ childNodes属性返回一个类似数组的对象（NodeList集合），成员包括当前节点的所有子节点。
```
var children = document.querySelector('ul').childNodes;
```
+ 上面代码中，children就是ul元素的所有子节点。
+ 使用该属性，可以遍历某个节点的所有子节点。
```
var div = document.getElementById('div1');
var children = div.childNodes;
for (var i = 0; i < children.length; i++) {
  // ...
}
```
+ 文档节点（document）就有两个子节点：文档类型节点（docType）和 HTML 根元素节点。
```
var children = document.childNodes;
for (var i = 0; i < children.length; i++) {
  console.log(children[i].nodeType);
}
// 10
// 1
```
+ 上面代码中，文档节点的第一个子节点的类型是10（即文档类型节点），第二个子节点的类型是1（即元素节点）。
+ 注意，除了元素节点，childNodes属性的返回值还包括文本节点和注释节点。如果当前节点不包括任何子节点，则返回一个空的NodeList集合。由于NodeList对象是一个动态集合，一旦子节点发生变化，立刻会反映在返回结果之中。

13、Node.prototype.isConnected
+ isConnected属性返回一个布尔值，表示当前节点是否在文档之中。
```
var test = document.createElement('p');
test.isConnected // false

document.body.appendChild(test);
test.isConnected // true
```
+ 上面代码中，test节点是脚本生成的节点，没有插入文档之前，isConnected属性返回false，插入之后返回true。

##### 2.2、方法
1、 Node.prototype.appendChild()
+ appendChild()方法接受一个节点对象作为参数，将其作为最后一个子节点，插入当前节点。该方法的返回值就是插入文档的子节点。
```
var p = document.createElement('p');
document.body.appendChild(p);
```
+ 上面代码新建一个<p>节点，将其插入document.body的尾部。
+ 如果参数节点是 DOM 已经存在的节点，appendChild()方法会将其从原来的位置，移动到新位置。
```
var div = document.getElementById('myDiv');
document.body.appendChild(div);
```
+ 上面代码中，插入的是一个已经存在的节点myDiv，结果就是该节点会从原来的位置，移动到document.body的尾部。
+ 如果appendChild()方法的参数是DocumentFragment节点，那么插入的是DocumentFragment的所有子节点，而不是DocumentFragment节点本身。返回值是一个空的DocumentFragment节点。

2、Node.prototype.hasChildNodes()
+ hasChildNodes方法返回一个布尔值，表示当前节点是否有子节点。
```
var foo = document.getElementById('foo');
if (foo.hasChildNodes()) {
  foo.removeChild(foo.childNodes[0]);
}
```
+ 上面代码表示，如果foo节点有子节点，就移除第一个子节点。
+ 注意，子节点包括所有类型的节点，并不仅仅是元素节点。哪怕节点只包含一个空格，hasChildNodes方法也会返回true。
+ 判断一个节点有没有子节点，有许多种方法，下面是其中的三种。
+ 1、node.hasChildNodes()
+ 2、node.firstChild !== null
+ 3、node.childNodes && node.childNodes.length > 0
+ hasChildNodes方法结合firstChild属性和nextSibling属性，可以遍历当前节点的所有后代节点。
```
function DOMComb(parent, callback) {
  if (parent.hasChildNodes()) {
    for (var node = parent.firstChild; node; node = node.nextSibling) {
      DOMComb(node, callback);
    }
  }
  callback(parent);
}

// 用法
DOMComb(document.body, console.log)
```
+ 上面代码中，DOMComb函数的第一个参数是某个指定的节点，第二个参数是回调函数。这个回调函数会依次作用于指定节点，以及指定节点的所有后代节点。

3、Node.prototype.cloneNode()
+ cloneNode方法用于克隆一个节点。它接受一个布尔值作为参数，表示是否同时克隆子节点。它的返回值是一个克隆出来的新节点。
```
var cloneUL = document.querySelector('ul').cloneNode(true);
```
+ 该方法有一些使用注意点：
+ （1）克隆一个节点，会拷贝该节点的所有属性，但是会丧失addEventListener方法和on-属性（即node.onclick = fn），添加在这个节点上的事件回调函数。
+ （2）该方法返回的节点不在文档之中，即没有任何父节点，必须使用诸如Node.appendChild这样的方法添加到文档之中。
+ （3）克隆一个节点之后，DOM 有可能出现两个有相同id属性（即id="xxx"）的网页元素，这时应该修改其中一个元素的id属性。如果原节点有name属性，可能也需要修改。

4、Node.prototype.insertBefore()
+ insertBefore方法用于将某个节点插入父节点内部的指定位置。
```
var insertedNode = parentNode.insertBefore(newNode, referenceNode);
```
+ insertBefore方法接受两个参数，第一个参数是所要插入的节点newNode，第二个参数是父节点parentNode内部的一个子节点referenceNode。newNode将插在referenceNode这个子节点的前面。返回值是插入的新节点newNode。
```
var p = document.createElement('p');
document.body.insertBefore(p, document.body.firstChild);
```
+ 上面代码中，新建一个<p>节点，插在document.body.firstChild的前面，也就是成为document.body的第一个子节点。
+ 如果insertBefore方法的第二个参数为null，则新节点将插在当前节点内部的最后位置，即变成最后一个子节点。
```
var p = document.createElement('p');
document.body.insertBefore(p, null);
```
+ 注意，如果所要插入的节点是当前 DOM 现有的节点，则该节点将从原有的位置移除，插入新的位置。
+ 由于不存在insertAfter方法，如果新节点要插在父节点的某个子节点后面，可以用insertBefore方法结合nextSibling属性模拟。
```
parent.insertBefore(s1, s2.nextSibling);
```
+ 上面代码中，parent是父节点，s1是一个全新的节点，s2是可以将s1节点，插在s2节点的后面。如果s2是当前节点的最后一个子节点，则s2.nextSibling返回null，这时s1节点会插在当前节点的最后，变成当前节点的最后一个子节点，等于紧跟在s2的后面。
+ 如果要插入的节点是DocumentFragment类型，那么插入的将是DocumentFragment的所有子节点，而不是DocumentFragment节点本身。返回值将是一个空的DocumentFragment节点。

5、Node.prototype.removeChild()
+ removeChild方法接受一个子节点作为参数，用于从当前节点移除该子节点。返回值是移除的子节点。
```
var divA = document.getElementById('A');
divA.parentNode.removeChild(divA);
```
+ 上面代码移除了divA节点。注意，这个方法是在divA的父节点上调用的，不是在divA上调用的。
+ 下面是如何移除当前节点的所有子节点。
```
var element = document.getElementById('top');
while (element.firstChild) {
  element.removeChild(element.firstChild);
}
```
+ 被移除的节点依然存在于内存之中，但不再是 DOM 的一部分。所以，一个节点移除以后，依然可以使用它，比如插入到另一个节点下面。
+ 如果参数节点不是当前节点的子节点，removeChild方法将报错。

6、Node.prototype.replaceChild()
+ replaceChild方法用于将一个新的节点，替换当前节点的某一个子节点。
```
var replacedNode = parentNode.replaceChild(newChild, oldChild);
```
+ 上面代码中，replaceChild方法接受两个参数，第一个参数newChild是用来替换的新节点，第二个参数oldChild是将要替换走的子节点。返回值是替换走的那个节点oldChild。
```
var divA = document.getElementById('divA');
var newSpan = document.createElement('span');
newSpan.textContent = 'Hello World!';
divA.parentNode.replaceChild(newSpan, divA);
```
+ 上面代码是如何将指定节点divA替换走。

7、Node.prototype.contains()
+ contains方法返回一个布尔值，表示参数节点是否满足以下三个条件之一。
+ 1、参数节点为当前节点。
+ 2、参数节点为当前节点的子节点。
+ 3、参数节点为当前节点的后代节点。
```
document.body.contains(node)
```
+ 上面代码检查参数节点node，是否包含在当前文档之中。
+ 注意，当前节点传入contains方法，返回true。
```
nodeA.contains(nodeA) // true
```

8、Node.prototype.compareDocumentPosition()
+ compareDocumentPosition方法的用法，与contains方法完全一致，返回一个六个比特位的二进制值，表示参数节点与当前节点的关系。

9、Node.prototype.isEqualNode()，Node.prototype.isSameNode()
+ isEqualNode方法返回一个布尔值，用于检查两个节点是否相等。所谓相等的节点，指的是两个节点的类型相同、属性相同、子节点相同。
```
var p1 = document.createElement('p');
var p2 = document.createElement('p');
p1.isEqualNode(p2) // true
```
+ isSameNode方法返回一个布尔值，表示两个节点是否为同一个节点。
```
var p1 = document.createElement('p');
var p2 = document.createElement('p');
p1.isSameNode(p2) // false
p1.isSameNode(p1) // true
```

10、Node.prototype.normalize()
+ normalize方法用于清理当前节点内部的所有文本节点（text）。它会去除空的文本节点，并且将毗邻的文本节点合并成一个，也就是说不存在空的文本节点，以及毗邻的文本节点。
```
var wrapper = document.createElement('div');
wrapper.appendChild(document.createTextNode('Part 1 '));
wrapper.appendChild(document.createTextNode('Part 2 '));
wrapper.childNodes.length // 2
wrapper.normalize();
wrapper.childNodes.length // 1
```
+ 上面代码使用normalize方法之前，wrapper节点有两个毗邻的文本子节点。使用normalize方法之后，两个文本子节点被合并成一个。

11、Node.prototype.getRootNode()
+ getRootNode()方法返回当前节点所在文档的根节点document，与ownerDocument属性的作用相同。
```
document.body.firstChild.getRootNode() === document
// true
document.body.firstChild.getRootNode() === document.body.firstChild.ownerDocument
// true
```
+ 该方法可用于document节点自身，这一点与document.ownerDocument不同。
```
document.getRootNode() // document
document.ownerDocument // null
```

#### 3、NodeList 接口，HTMLCollection 接口
##### 3.1、NodeList 接口
+ 1、概述
