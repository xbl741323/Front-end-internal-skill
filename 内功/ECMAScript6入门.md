### 一、ECMAScript 6 简介
+ ECMAScript 6.0（以下简称 ES6）是 JavaScript 语言的下一代标准，已经在 2015 年 6 月正式发布了。它的目标，是使得 JavaScript 语言可以用来编写复杂的大型应用程序，成为企业级开发语言。

#### 1、ECMAScript 和 JavaScript 的关系？
+ ECMAScript 和 JavaScript 的关系是，前者是后者的规格（标准），后者是前者的一种实现（另外的 ECMAScript 方言还有 JScript 和 ActionScript）。日常场合，这两个词是可以互换的。
+ 要讲清楚这个问题，需要回顾历史。1996 年 11 月，JavaScript 的创造者 Netscape 公司，决定将 JavaScript 提交给标准化组织 ECMA，希望这种语言能够成为国际标准。次年，ECMA 发布 262 号标准文件（ECMA-262）的第一版，规定了浏览器脚本语言的标准，并将这种语言称为 ECMAScript，这个版本就是 1.0 版。该标准从一开始就是针对 JavaScript 语言制定的，但是之所以不叫 JavaScript，有两个原因。一是商标，Java 是 Sun 公司的商标，根据授权协议，只有 Netscape 公司可以合法地使用 JavaScript 这个名字，且 JavaScript 本身也已经被 Netscape 公司注册为商标。二是想体现这门语言的制定者是 ECMA，不是 Netscape，这样有利于保证这门语言的开放性和中立性。

#### 2、ES6 与 ECMAScript 2015 的关系？
+ ES6 既是一个历史名词，也是一个泛指，含义是 5.1 版以后的 JavaScript 的下一代标准，涵盖了 ES2015、ES2016、ES2017 等等，而 ECMAScript 2015（简称 ES2015） 则是正式名称，特指该年发布的正式版本的语言标准。本文中提到 ES6 的地方，一般是指 ES2015 标准，但有时也是泛指“下一代 JavaScript 语言”。

#### 3、Babel 转码器 
+ Babel 是一个广泛使用的 ES6 转码器，可以将 ES6 代码转为 ES5 代码，从而在老版本的浏览器执行。这意味着，你可以用 ES6 的方式编写程序，又不用担心现有环境是否支持。下面是一个例子。
```
// 转码前
input.map(item => item + 1);

// 转码后
input.map(function (item) {
  return item + 1;
});
```
+ 上面的原始代码用了箭头函数，Babel 将其转为普通函数，就能在不支持箭头函数的 JavaScript 环境执行了，下面的命令在项目目录中，安装 Babel。
```
$ npm install --save-dev @babel/core
```
### 二、let 和 const 命令

#### 1、基本用法

+ ES6 新增了let命令，用来声明变量。它的用法类似于var，但是所声明的变量，只在let命令所在的代码块内有效。
```
{
  let a = 10;
  var b = 1;
}

a // ReferenceError: a is not defined.
b // 1
```
#### 2、不存在变量提升
+ var命令会发生“变量提升”现象，即变量可以在声明之前使用，值为undefined。这种现象多多少少是有些奇怪的，按照一般的逻辑，变量应该在声明语句之后才可以使用。为了纠正这种现象，let命令改变了语法行为，它所声明的变量一定要在声明后使用，否则报错。
```
// var 的情况
console.log(foo); // 输出undefined
var foo = 2;

// let 的情况
console.log(bar); // 报错ReferenceError
let bar = 2;
```
#### 3、暂时性死区
+ 在代码块内，使用let命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”（temporal dead zone，简称 TDZ）。

#### 4、不允许重复声明 
+ let不允许在相同作用域内，重复声明同一个变量。
```
// 报错
function func() {
  let a = 10;
  var a = 1;
}

// 报错
function func() {
  let a = 10;
  let a = 1;
}
```
#### 5、const 命令
+ const声明一个只读的常量。一旦声明，常量的值就不能改变，就必须立即初始化，不能留到以后赋值。
+ const命令声明的常量也是不提升，同样存在暂时性死区，只能在声明的位置后面使用。
```
if (true) {
  console.log(MAX); // ReferenceError
  const MAX = 5;
}
```
+ const声明的常量，也与let一样不可重复声明。
```
var message = "Hello!";
let age = 25;

// 以下两行都会报错
const message = "Goodbye!";
const age = 30;
```
#### 6、块级作用域
+ 为什么需要块级作用域？
+ ES5 只有全局作用域和函数作用域，没有块级作用域，这带来很多不合理的场景。
+ 第一种场景，内层变量可能会覆盖外层变量。
```
var tmp = new Date();
function f() {
  console.log(tmp);
  if (false) {
    var tmp = 'hello world';
  }
}
f(); // undefined
```
+ 第二种场景，用来计数的循环变量泄露为全局变量。
```
var s = 'hello';
for (var i = 0; i < s.length; i++) {
  console.log(s[i]);
}
console.log(i); // 5
```
#### 7、ES6 的块级作用域 
+ let实际上为 JavaScript 新增了块级作用域。
```
function f1() {
  let n = 5;
  if (true) {
    let n = 10;
  }
  console.log(n); // 5
}

function f2() {
  var n = 5;
  if (true) {
    var n = 10;
  }
  console.log(n); // 10
}
```
+ 上面的函数有两个代码块，都声明了变量n，运行后输出 5。这表示外层代码块不受内层代码块的影响。如果两次都使用var定义变量n，最后输出的值才是 10。
+ 块级作用域的出现，实际上使得获得广泛应用的匿名立即执行函数表达式（匿名 IIFE）不再必要了。
```
// IIFE 写法
(function () {
  var tmp = ...;
  ...
}());

// 块级作用域写法
{
  let tmp = ...;
  ...
}
```
#### 8、块级作用域与函数声明 
函数能不能在块级作用域之中声明？这是一个相当令人混淆的问题。
+ ES5 规定，函数只能在顶层作用域和函数作用域之中声明，不能在块级作用域声明。
+ ES6 引入了块级作用域，明确允许在块级作用域之中声明函数。ES6 规定，块级作用域之中，函数声明语句的行为类似于let，在块级作用域之外不可引用。
+ 另外，还有一个需要注意的地方。ES6 的块级作用域必须有大括号，如果没有大括号，JavaScript 引擎就认为不存在块级作用域。
```
// 第一种写法，报错
if (true) let x = 1;

// 第二种写法，不报错
if (true) {
  let x = 1;
}
```
#### 9、ES6 声明变量的六种方法 
ES5 只有两种声明变量的方法：var命令和function命令。ES6 除了添加let和const命令，后面章节还会提到，另外两种声明变量的方法：import命令和class命令。所以，ES6 一共有 6 种声明变量的方法。

#### 10、顶层对象的属性
顶层对象，在浏览器环境指的是window对象，在 Node 指的是global对象。ES5 之中，顶层对象的属性与全局变量是等价的。
+ 顶层对象的属性与全局变量挂钩，被认为是 JavaScript 语言最大的设计败笔之一。这样的设计带来了几个很大的问题，首先是没法在编译时就报出变量未声明的错误，只有运行时才能知道（因为全局变量可能是顶层对象的属性创造的，而属性的创造是动态的）；其次，程序员很容易不知不觉地就创建了全局变量（比如打字出错）；最后，顶层对象的属性是到处可以读写的，这非常不利于模块化编程。另一方面，window对象有实体含义，指的是浏览器的窗口对象，顶层对象是一个有实体含义的对象，也是不合适的。
+ ES6 为了改变这一点，一方面规定，为了保持兼容性，var命令和function命令声明的全局变量，依旧是顶层对象的属性；另一方面规定，let命令、const命令、class命令声明的全局变量，不属于顶层对象的属性。也就是说，从 ES6 开始，全局变量将逐步与顶层对象的属性脱钩。
```
var a = 1;
// 如果在 Node 的 REPL 环境，可以写成 global.a
// 或者采用通用方法，写成 this.a
window.a // 1

let b = 1;
window.b // undefined
```
+ 上面代码中，全局变量a由var命令声明，所以它是顶层对象的属性；全局变量b由let命令声明，所以它不是顶层对象的属性，返回undefined。

### 三、变量的解构赋值

#### 1、数组的解构赋值
ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。以前，为变量赋值，只能直接指定值。
```
let a = 1;
let b = 2;
let c = 3;
```
ES6 允许写成下面这样。
```
let [a, b, c] = [1, 2, 3];
```
+ 解构赋值允许指定默认值。
```
let [x, y = 'b'] = ['a']; // x='a', y='b'
```
#### 2、对象的解构赋值
解构不仅可以用于数组，还可以用于对象。
```
let { foo, bar } = { foo: 'aaa', bar: 'bbb' };
foo // "aaa"
bar // "bbb"
```
+ 对象的解构与数组有一个重要的不同。数组的元素是按次序排列的，变量的取值由它的位置决定；而对象的属性没有次序，变量必须与属性同名，才能取到正确的值。
```
let { bar, foo } = { foo: 'aaa', bar: 'bbb' };
foo // "aaa"
bar // "bbb"

let { baz } = { foo: 'aaa', bar: 'bbb' };
baz // undefined
```
+ 如果解构失败，变量的值等于undefined。
+ 对象的解构赋值，可以很方便地将现有对象的方法，赋值到某个变量。
```
// 例一
let { log, sin, cos } = Math;

// 例二
const { log } = console; // console是个对象类型
log('hello') // hello
```
+ 对象的解构也可以指定默认值。
```
var {x = 3} = {};
x // 3

var {x, y = 5} = {x: 1};
x // 1
y // 5

var {x: y = 3} = {};
y // 3

var {x: y = 3} = {x: 5};
y // 5

var { message: msg = 'Something went wrong' } = {};
msg // "Something went wrong"
```
#### 3、字符串的解构赋值
字符串也可以解构赋值。这是因为此时，字符串被转换成了一个类似数组的对象。
```
const [a, b, c, d, e] = 'hello';
a // "h"
b // "e"
c // "l"
d // "l"
e // "o"
```
+ 类似数组的对象都有一个length属性，因此还可以对这个属性解构赋值。
```
let {length : len} = 'hello';
len // 5
```
+ 上面代码中，数值和布尔值的包装对象都有toString属性，因此变量s都能取到值。
+ 解构赋值的规则是，只要等号右边的值不是对象或数组，就先将其转为对象。由于undefined和null无法转为对象，所以对它们进行解构赋值，都会报错。
```
let { prop: x } = undefined; // TypeError
let { prop: y } = null; // TypeError
```

#### 4、数值和布尔值的解构赋值
解构赋值时，如果等号右边是数值和布尔值，则会先转为对象。
```
let {toString: s} = 123;
s === Number.prototype.toString // true

let {toString: s} = true;
s === Boolean.prototype.toString // true
```

#### 5、函数参数的解构赋值
函数的参数也可以使用解构赋值。
```
function add([x, y]){
  return x + y;
}
add([1, 2]); // 3
```
```
[[1, 2], [3, 4]].map(([a, b]) => a + b);
// [ 3, 7 ]
```
+ 函数参数的解构也可以使用默认值。
```
function move({x = 0, y = 0} = {}) {
  return [x, y];
}

move({x: 3, y: 8}); // [3, 8]
move({x: 3}); // [3, 0]
move({}); // [0, 0]
move(); // [0, 0]
```

#### 6、圆括号问题
解构赋值虽然很方便，但是解析起来并不容易。对于编译器来说，一个式子到底是模式，还是表达式，没有办法从一开始就知道，必须解析到（或解析不到）等号才能知道。
+ 由此带来的问题是，如果模式中出现圆括号怎么处理。ES6 的规则是，只要有可能导致解构的歧义，就不得使用圆括号。
+ 但是，这条规则实际上不那么容易辨别，处理起来相当麻烦。因此，建议只要有可能，就不要在模式中放置圆括号。

#### 7、用途
变量的解构赋值用途很多。
+ （1）交换变量的值
```
let x = 1;
let y = 2;
[x, y] = [y, x];
```
上面代码交换变量x和y的值，这样的写法不仅简洁，而且易读，语义非常清晰。

+ （2）从函数返回多个值
函数只能返回一个值，如果要返回多个值，只能将它们放在数组或对象里返回。有了解构赋值，取出这些值就非常方便。
```
// 返回一个数组

function example() {
  return [1, 2, 3];
}
let [a, b, c] = example();

// 返回一个对象

function example() {
  return {
    foo: 1,
    bar: 2
  };
}
let { foo, bar } = example();
```
+ （3）函数参数的定义
解构赋值可以方便地将一组参数与变量名对应起来。
```
// 参数是一组有次序的值
function f([x, y, z]) { ... }
f([1, 2, 3]);

// 参数是一组无次序的值
function f({x, y, z}) { ... }
f({z: 3, y: 2, x: 1});
```
+ （4）提取 JSON 数据
解构赋值对提取 JSON 对象中的数据，尤其有用。
```
let jsonData = {
  id: 42,
  status: "OK",
  data: [867, 5309]
};

let { id, status, data: number } = jsonData;

console.log(id, status, number);
// 42, "OK", [867, 5309]
```
上面代码可以快速提取 JSON 数据的值。

+ （5）遍历 Map 结构
任何部署了 Iterator 接口的对象，都可以用for...of循环遍历。Map 结构原生支持 Iterator 接口，配合变量的解构赋值，获取键名和键值就非常方便。
```
const map = new Map();
map.set('first', 'hello');
map.set('second', 'world');

for (let [key, value] of map) {
  console.log(key + " is " + value);
}
// first is hello
// second is world
```
如果只想获取键名，或者只想获取键值，可以写成下面这样。
```
// 获取键名
for (let [key] of map) {
  // ...
}

// 获取键值
for (let [,value] of map) {
  // ...
}
```
+ （6）输入模块的指定方法
加载模块时，往往需要指定输入哪些方法。解构赋值使得输入语句非常清晰。
```
const { SourceMapConsumer, SourceNode } = require("source-map");
```

### 四、字符串的扩展

#### 1、模板字符串
模板字符串（template string）是增强版的字符串，用反引号（`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。
```
// 普通字符串
`In JavaScript '\n' is a line-feed.`

// 多行字符串
`In JavaScript this is
 not legal.`

console.log(`string text line 1
string text line 2`);

// 字符串中嵌入变量
let name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`
```
+ 大括号内部可以放入任意的 JavaScript 表达式，可以进行运算，以及引用对象属性。
```
let x = 1;
let y = 2;

`${x} + ${y} = ${x + y}`
// "1 + 2 = 3"

`${x} + ${y * 2} = ${x + y * 2}`
// "1 + 4 = 5"

let obj = {x: 1, y: 2};
`${obj.x + obj.y}`
// "3"
```
+ 模板字符串之中还能调用函数。
```
function fn() {
  return "Hello World";
}

`foo ${fn()} bar`
// foo Hello World bar
```
### 五、字符串的新增方法

#### 1、实例方法：includes(), startsWith(), endsWith()
传统上，JavaScript 只有indexOf方法，可以用来确定一个字符串是否包含在另一个字符串中。ES6 又提供了三种新方法。
+ includes()：返回布尔值，表示是否找到了参数字符串。
+ startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部。
+ endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部。
```
let s = 'Hello world!';
s.startsWith('Hello') // true
s.endsWith('!') // true
s.includes('o') // true
```
+ 这三个方法都支持第二个参数，表示开始搜索的位置。
```
let s = 'Hello world!';
s.startsWith('world', 6) // true
s.endsWith('Hello', 5) // true
s.includes('Hello', 6) // false
```
+ 上面代码表示，使用第二个参数n时，endsWith的行为与其他两个方法有所不同。它针对前n个字符，而其他两个方法针对从第n个位置直到字符串结束。

#### 2、实例方法：repeat() 
repeat方法返回一个新字符串，表示将原字符串重复n次。
```
'x'.repeat(3) // "xxx"
'hello'.repeat(2) // "hellohello"
'na'.repeat(0) // ""
```
+ 参数如果是小数，会被取整。
```
'na'.repeat(2.9) // "nana"
```
+ 如果repeat的参数是负数或者Infinity，会报错
```
'na'.repeat(Infinity)
// RangeError
'na'.repeat(-1)
// RangeError
```
+ 但是，如果参数是 0 到-1 之间的小数，则等同于 0，这是因为会先进行取整运算。0 到-1 之间的小数，取整以后等于-0，repeat视同为 0。
```
'na'.repeat(-0.9) // ""
```
+ 参数NaN等同于 0。
```
'na'.repeat(NaN) // ""
```
+ 如果repeat的参数是字符串，则会先转换成数字。
```
'na'.repeat('na') // ""
'na'.repeat('3') // "nanana"
```
#### 3、实例方法：replaceAll()
历史上，字符串的实例方法replace()只能替换第一个匹配。
```
'aabbcc'.replace('b', '_')
// 'aa_bcc'
```
+ 如果要替换所有的匹配，不得不使用正则表达式的g修饰符。
```
'aabbcc'.replace(/b/g, '_')
// 'aa__cc'
```
+ 正则表达式毕竟不是那么方便和直观，ES2021 引入了replaceAll()方法，可以一次性替换所有匹配。
+ 它的用法与replace()相同，返回一个新字符串，不会改变原字符串。
+ replaceAll()的第二个参数replacement除了为字符串，也可以是一个函数，该函数的返回值将替换掉第一个参数searchValue匹配的文本。
```
'aabbcc'.replaceAll('b', () => '_')
// 'aa__cc'
```
+ replaceAll()的第二个参数replacement是一个字符串，表示替换的文本，其中可以使用一些特殊字符串。
```
$&：匹配的字符串。
$`：匹配结果前面的文本。
$'：匹配结果后面的文本。
$n：匹配成功的第n组内容，n是从1开始的自然数。这个参数生效的前提是，第一个参数必须是正则表达式。
$$：指代美元符号$。
```
+ 下面是一些例子。
```
// $& 表示匹配的字符串，即`b`本身
// 所以返回结果与原字符串一致
'abbc'.replaceAll('b', '$&')
// 'abbc'

// $` 表示匹配结果之前的字符串
// 对于第一个`b`，$` 指代`a`
// 对于第二个`b`，$` 指代`ab`
'abbc'.replaceAll('b', '$`')
// 'aaabc'

// $' 表示匹配结果之后的字符串
// 对于第一个`b`，$' 指代`bc`
// 对于第二个`b`，$' 指代`c`
'abbc'.replaceAll('b', `$'`)
// 'abccc'

// $1 表示正则表达式的第一个组匹配，指代`ab`
// $2 表示正则表达式的第二个组匹配，指代`bc`
'abbc'.replaceAll(/(ab)(bc)/g, '$2$1')
// 'bcab'

// $$ 指代 $
'abc'.replaceAll('b', '$$')
// 'a$c'
```
+ 下面例子中，正则表达式有三个组匹配，所以replacer()函数的第一个参数match是捕捉到的匹配内容（即字符串123abc456），后面三个参数p1、p2、p3则依次为三个组匹配。
```
const str = '123abc456';
const regex = /(\d+)([a-z]+)(\d+)/g;
function replacer(match, p1, p2, p3, offset, string) {
  return [p1, p2, p3].join(' - ');
}
str.replaceAll(regex, replacer)
// 123 - abc - 456
```
#### 4、实例方法：at()
at()方法接受一个整数作为参数，返回参数指定位置的字符，支持负索引（即倒数的位置）。
```
const str = 'hello';
str.at(1) // "e"
str.at(-1) // "o"
```
### 五、正则的扩展（暂不记录）

### 六、数值的扩展
#### 1、二进制和八进制表示法
ES6 提供了二进制和八进制数值的新的写法，分别用前缀0b（或0B）和0o（或0O）表示。
```
0b111110111 === 503 // true
0o767 === 503 // true
```
+ 如果要将0b和0o前缀的字符串数值转为十进制，要使用Number方法。
```
Number('0b111')  // 7
Number('0o10')  // 8
```
#### 2、Number.isFinite(), Number.isNaN() 
ES6 在Number对象上，新提供了Number.isFinite()和Number.isNaN()两个方法。
+ Number.isFinite()用来检查一个数值是否为有限的（finite），即不是Infinity。
```
Number.isFinite(15); // true
Number.isFinite(0.8); // true
Number.isFinite(NaN); // false
Number.isFinite(Infinity); // false
Number.isFinite(-Infinity); // false
Number.isFinite('foo'); // false
Number.isFinite('15'); // false
Number.isFinite(true); // false
```
+ 注意，如果参数类型不是数值，Number.isFinite一律返回false。
+ Number.isNaN()用来检查一个值是否为NaN。
```
Number.isNaN(NaN) // true
Number.isNaN(15) // false
Number.isNaN('15') // false
Number.isNaN(true) // false
Number.isNaN(9/NaN) // true
Number.isNaN('true' / 0) // true
Number.isNaN('true' / 'true') // true
```
+ 如果参数类型不是NaN，Number.isNaN一律返回false。
+ 它们与传统的全局方法isFinite()和isNaN()的区别在于，传统方法先调用Number()将非数值的值转为数值，再进行判断，而这两个新方法只对数值有效，Number.isFinite()对于非数值一律返回false, Number.isNaN()只有对于NaN才返回true，非NaN一律返回false。
```
isFinite(25) // true
isFinite("25") // true
Number.isFinite(25) // true
Number.isFinite("25") // false

isNaN(NaN) // true
isNaN("NaN") // true
Number.isNaN(NaN) // true
Number.isNaN("NaN") // false
Number.isNaN(1) // false
```
#### 3、Number.parseInt(), Number.parseFloat() 
ES6 将全局方法parseInt()和parseFloat()，移植到Number对象上面，行为完全保持不变。
```
// ES5的写法
parseInt('12.34') // 12
parseFloat('123.45#') // 123.45

// ES6的写法
Number.parseInt('12.34') // 12
Number.parseFloat('123.45#') // 123.45
```
这样做的目的，是逐步减少全局性方法，使得语言逐步模块化。
```
Number.parseInt === parseInt // true
Number.parseFloat === parseFloat // true
```
#### 4、Number.isInteger() 
Number.isInteger()用来判断一个数值是否为整数。
```
Number.isInteger(25) // true
Number.isInteger(25.1) // false
```
+ JavaScript 内部，整数和浮点数采用的是同样的储存方法，所以 25 和 25.0 被视为同一个值。
```
Number.isInteger(25) // true
Number.isInteger(25.0) // true
```
+ 如果参数不是数值，Number.isInteger返回false。
```
Number.isInteger() // false
Number.isInteger(null) // false
Number.isInteger('15') // false
Number.isInteger(true) // false
```
+ 注意，由于 JavaScript 采用 IEEE 754 标准，数值存储为64位双精度格式，数值精度最多可以达到 53 个二进制位（1 个隐藏位与 52 个有效位）。如果数值的精度超过这个限度，第54位及后面的位就会被丢弃，这种情况下，Number.isInteger可能会误判。
```
Number.isInteger(3.0000000000000002) // true
```
+ 上面代码中，Number.isInteger的参数明明不是整数，但是会返回true。原因就是这个小数的精度达到了小数点后16个十进制位，转成二进制位超过了53个二进制位，导致最后的那个2被丢弃了。
+ 类似的情况还有，如果一个数值的绝对值小于Number.MIN_VALUE（5E-324），即小于 JavaScript 能够分辨的最小值，会被自动转为 0。这时，Number.isInteger也会误判。
```
Number.isInteger(5E-324) // false
Number.isInteger(5E-325) // true
```
+ 上面代码中，5E-325由于值太小，会被自动转为0，因此返回true。总之，如果对数据精度的要求较高，不建议使用Number.isInteger()判断一个数值是否为整数。

#### 5、Number.EPSILON
ES6 在Number对象上面，新增一个极小的常量Number.EPSILON。根据规格，它表示 1 与大于 1 的最小浮点数之间的差。
```
Number.EPSILON === Math.pow(2, -52)
// true
Number.EPSILON
// 2.220446049250313e-16
Number.EPSILON.toFixed(20)
// "0.00000000000000022204"
```
+ Number.EPSILON实际上是 JavaScript 能够表示的最小精度。误差如果小于这个值，就可以认为已经没有意义了，即不存在误差了。
+ 引入一个这么小的量的目的，在于为浮点数计算，设置一个误差范围。我们知道浮点数计算是不精确的。
```
0.1 + 0.2
// 0.30000000000000004

0.1 + 0.2 - 0.3
// 5.551115123125783e-17

5.551115123125783e-17.toFixed(20)
// '0.00000000000000005551'
```
+ 上面代码解释了，为什么比较0.1 + 0.2与0.3得到的结果是false。
```
0.1 + 0.2 === 0.3 // false
```
+ Number.EPSILON的实质是一个可以接受的最小误差范围。

#### 6、安全整数和 Number.isSafeInteger() 
JavaScript 能够准确表示的整数范围在-2^53到2^53之间（不含两个端点），超过这个范围，无法精确表示这个值。
```
Math.pow(2, 53) // 9007199254740992

9007199254740992  // 9007199254740992
9007199254740993  // 9007199254740992

Math.pow(2, 53) === Math.pow(2, 53) + 1
// true
```
+ ES6 引入了Number.MAX_SAFE_INTEGER和Number.MIN_SAFE_INTEGER这两个常量，用来表示这个范围的上下限。
```
Number.MAX_SAFE_INTEGER === Math.pow(2, 53) - 1
// true
Number.MAX_SAFE_INTEGER === 9007199254740991
// true

Number.MIN_SAFE_INTEGER === -Number.MAX_SAFE_INTEGER
// true
Number.MIN_SAFE_INTEGER === -9007199254740991
// true
```
+ Number.isSafeInteger()则是用来判断一个整数是否落在这个范围之内。
```
Number.isSafeInteger('a') // false
Number.isSafeInteger(null) // false
Number.isSafeInteger(NaN) // false
Number.isSafeInteger(Infinity) // false
Number.isSafeInteger(-Infinity) // false

Number.isSafeInteger(3) // true
Number.isSafeInteger(1.2) // false
Number.isSafeInteger(9007199254740990) // true
Number.isSafeInteger(9007199254740992) // false

Number.isSafeInteger(Number.MIN_SAFE_INTEGER - 1) // false
Number.isSafeInteger(Number.MIN_SAFE_INTEGER) // true
Number.isSafeInteger(Number.MAX_SAFE_INTEGER) // true
Number.isSafeInteger(Number.MAX_SAFE_INTEGER + 1) // false
```

#### 7、Math 对象的扩展
ES6 在 Math 对象上新增了 17 个与数学相关的方法。所有这些方法都是静态方法，只能在 Math 对象上调用。
+ 1、Math.trunc() 
+ Math.trunc方法用于去除一个数的小数部分，返回整数部分，对于非数值，Math.trunc内部使用Number方法将其先转为数值，对于空值和无法截取整数的值，返回NaN。
```
Math.trunc(4.1) // 4
Math.trunc(4.9) // 4
Math.trunc(-4.1) // -4
Math.trunc(-4.9) // -4
Math.trunc(-0.1234) // -0
```
+ 2、Math.sign()
+ Math.sign方法用来判断一个数到底是正数、负数、还是零，对于非数值，会先将其转换为数值。
+ 它会返回五种值。
```
//参数为正数，返回+1；
//参数为负数，返回-1；
//参数为 0，返回0；
//参数为-0，返回-0;
//其他值，返回NaN。

Math.sign(-5) // -1
Math.sign(5) // +1
Math.sign(0) // +0
Math.sign(-0) // -0
Math.sign(NaN) // NaN
```
+ 3、Math.cbrt()
+ Math.cbrt()方法用于计算一个数的立方根，对于非数值，Math.cbrt()方法内部也是先使用Number()方法将其转为数值。
```
Math.cbrt(-1) // -1
Math.cbrt(0)  // 0
Math.cbrt(1)  // 1
Math.cbrt(2)  // 1.2599210498948732
```
+ 4、Math.hypot()
+ Math.hypot方法返回所有参数的平方和的平方根。
```
Math.hypot(3, 4);        // 5
Math.hypot(3, 4, 5);     // 7.0710678118654755
Math.hypot();            // 0
Math.hypot(NaN);         // NaN
Math.hypot(3, 4, 'foo'); // NaN
Math.hypot(3, 4, '5');   // 7.0710678118654755
Math.hypot(-3);          // 3
```

### 七、函数的扩展
#### 1、函数参数的默认值
+ ES6 之前，不能直接为函数的参数指定默认值，只能采用变通的方法。
+ ES6 允许为函数的参数设置默认值，即直接写在参数定义的后面。
+ 参数变量是默认声明的，所以不能用let或const再次声明。
```
function foo(x = 5) {
  let x = 1; // error
  const x = 2; // error
}
```
+ 参数默认值可以与解构赋值的默认值，结合起来使用。
```
unction foo({x, y = 5}) {
  console.log(x, y);
}

foo({}) // undefined 5
foo({x: 1}) // 1 5
foo({x: 1, y: 2}) // 1 2
foo() // TypeError: Cannot read property 'x' of undefined
```

#### 2、rest 参数
ES6 引入 rest 参数（形式为...变量名），用于获取函数的多余参数，这样就不需要使用arguments对象了。rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中。
```
function add(...values) {
  let sum = 0;

  for (var val of values) {
    sum += val;
  }

  return sum;
}
add(2, 5, 3) // 10
```
+ 注意，rest 参数之后不能再有其他参数（即只能是最后一个参数），否则会报错。
```
// 报错
function f(a, ...b, c) {
  // ...
}
```

#### 3、严格模式
从 ES5 开始，函数内部可以设定为严格模式。
```
function doSomething(a, b) {
  'use strict';
  // code
}
```
+ ES2016 做了一点修改，规定只要函数参数使用了默认值、解构赋值、或者扩展运算符，那么函数内部就不能显式设定为严格模式，否则会报错。
```
// 报错
function doSomething(a, b = a) {
  'use strict';
  // code
}

// 报错
const doSomething = function ({a, b}) {
  'use strict';
  // code
};

// 报错
const doSomething = (...a) => {
  'use strict';
  // code
};

const obj = {
  // 报错
  doSomething({a, b}) {
    'use strict';
    // code
  }
};
```

#### 4、name 属性 
函数的name属性，返回该函数的函数名。
```
function foo() {}
foo.name // "foo"
```

#### 5、箭头函数
ES6 允许使用“箭头”（=>）定义函数。
```
var f = v => v;

// 等同于
var f = function (v) {
  return v;
};
```
+ 如果箭头函数不需要参数或需要多个参数，就使用一个圆括号代表参数部分。
```
var f = () => 5;
// 等同于
var f = function () { return 5 };

var sum = (num1, num2) => num1 + num2;
// 等同于
var sum = function(num1, num2) {
  return num1 + num2;
};
```
+ 如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回。
```
var sum = (num1, num2) => { return num1 + num2; }
```
#### 使用注意点
箭头函数有几个使用注意点。
+（1）箭头函数没有自己的this对象（详见下文）。
+（2）不可以当作构造函数，也就是说，不可以对箭头函数使用new命令，否则会抛出一个错误。
+（3）不可以使用arguments对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。
+（4）不可以使用yield命令，因此箭头函数不能用作 Generator 函数。
