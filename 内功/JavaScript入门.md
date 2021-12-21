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
点字符（.）匹配除回车（\r）、换行(\n) 、行分隔符（\u2028）和段分隔符（\u2029）以外的所有字符。注意，对于码点大于0xFFFF字符，点字符不能正确匹配，会认为这是两个字符。
```
/c.t/.test('cat'); // true
/c.a/.test('c-a'); // true
/c.t/.test('coot'); // false
```
+ 上面代码中，c.t匹配c和t之间包含任意一个字符的情况，只要这三个字符在同一行，比如cat、c2t、c-t等等，但是不匹配coot。
+ （2）位置字符
位置字符用来提示字符所处的位置，主要有两个字符。
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
竖线符号（|）在正则表达式中表示“或关系”（OR），即cat|dog表示匹配cat或dog。
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
#### 十一、JSON 对象
