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
