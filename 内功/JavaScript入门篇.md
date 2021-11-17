## 什么是JavaScript语言？
+ javaScript是一种轻量级的脚本语言，所谓脚本语言（script language），指的是它不具备开发操作系统的能力，而是只用来编写控制其他大型应用程序（比如浏览器的）脚本。
+ JavaScript 也是一种嵌入式（embedded）语言。本身不提供任何与 I/O（输入/输出）相关的 API，都要靠宿主环境（host）提供，所以 JavaScript 只合适嵌入更大型的应用程序环境，去调用宿主环境提供的底层 API。目前，已经嵌入 JavaScript 的宿主环境有多种，最常见的环境就是浏览器，另外还有服务器环境，也就是 Node 项目。
+ 从语法角度看，JavaScript 语言是一种“对象模型”语言。但是，JavaScript 并不是纯粹的“面向对象语言”，还支持其他编程范式（比如函数式编程）。这导致几乎任何一个问题，JavaScript 都有多种解决方法。
+ JavaScript 的核心语法部分相当精简，只包括两个部分：基本的语法构造（比如操作符、控制结构、语句）和标准库（就是一系列具有各种功能的对象比如Array、Date、Math等）。除此之外，各种宿主环境提供额外的 API（即只能在该环境使用的接口），以便 JavaScript 调用。以浏览器为例，它提供的额外 API 可以分成三大类。1、浏览器控制类：操作浏览器；2、DOM 类：操作网页的各种元素；3、Web 类：实现互联网的各种功能；如果宿主环境是服务器，则会提供各种操作系统的 API，比如文件操作 API、网络通信 API等等。

### 基本语法
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

### 数据类型
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
