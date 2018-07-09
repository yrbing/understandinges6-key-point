* ## Template Literals

ECMAScript 6 的 _template literals _提供了创建 domain-specific languages\(DSLs\)的句法，处理内容比ECMAScript 5更加安全。

> A DSL is a programming language designed for a specific, narrow purpose, as opposed to general-purpose languages like JavaScript.

事实上，ECMAScript 6的  template literals，解决了ES5一直缺少的如下features：

* **Multiline strings **多行字符串的正式概念
* **Basic string formatting **用变量的值替换部分string
* **HTML escaping **转换string使其能够安全插入HTML

ES6没有试图给JS已有的字符串添加更多功能，而是采用了template literals这个全新的方法去解决这些问题。

### Basic Syntax

template literals使用倒引号backtick。

```js
let message = `Hello world!`;

console.log(message);               // "Hello world!"
console.log(typeof message);        // "string"
console.log(message.length);        // 12
```

如果想在字符串中使用backtick，用反斜线backslash转义escape它。

```js
let message = `\`Hello\` world!`;

console.log(message);               // "`Hello` world!"
console.log(typeof message);        // "string"
console.log(message.length);        // 14
```

在template literals中使用double或者single quotes，无须转义escape。

### Multiline Strings

#### Pre-ECMAScript 6 Workarounds

由于一直存在的句法bug，JS有一种创建多行string的变通办法。

```js
var message = "Multiline \
string";

console.log(message);       // "Multiline string"
```

```js
var message = "Multiline \n\
string";

console.log(message);       // "Multiline
                            //  string"
```

虽然在主要的JS引擎中，这样做都可以达到目的，但是这个行为被定义为一个bug，很多开发者不推荐这么做。\(反斜线\)

其他的pre-ECMAScript 6创建多行字符串的方式基本基于array或者字符串连接string concatenation。

```js
var message = [
    "Multiline ",
    "string"
].join("\n");

let message = "Multiline \n" +
    "string";
```

#### Multiline Strings the Easy Way

ES6的template literals：

```js
let message = `Multiline
string`;

console.log(message);           // "Multiline
                                //  string"
console.log(message.length);    // 16
```

倒引号backticks中的所有空格都会成为string的一部分，因此小心使用缩进indentation。

```js
let message = `Multiline
               string`;

console.log(message);           // "Multiline
                                //                 string"
console.log(message.length);    // 31
```

### Making Substitutions

Substitutions允许在template literal中嵌入任何合法的JS表达式。

> A template literal can access any variable accessible in the scope in which it is defined. Attempting to use an undeclared variable in a template literal throws an error in both strict and non-strict modes.
>
> 变量可以是undefined，但不能是未声明的。（所以一个已声明对象的未声明属性是可以的）

可以嵌入计算，函数调用等等。

```js
let count = 10,
    price = 0.25,
    message = `${count} items cost $${(count * price).toFixed(2)}.`;

console.log(message);       // "10 items cost $2.50."
```

template literal也是JS表达式，因此可以在template literal中嵌入template literal。

```js
let name = "Nicholas",
    message = `Hello, ${
        `my name is ${ name }`
    }.`;

console.log(message);        // "Hello, my name is Nicholas."
```

### Tagged Templates

template literals可以不使用concatenation，达到创建多行string，或者在string中嵌入value的目的。但其真正的能力来自于tagged templates。

template tag对template literal进行转化，返回最终的字符串值。tag在template的开头指定。

```js
let message = tag`Hello world`;
```

#### Defining Tags

tag是一个用处理后的template literal数据调用的函数。将有关模板文字的数据作为单独的块pieces接收，合并这些块创建出result。

第一个参数是一个包括经JS解释\(interpreted\)的字面量字符串的数组。每一个随后的参数都是一个substitution的解释\(interpreted\)值。

tag函数很适合使用rest arguments，处理数据更加方便：

```js
function tag(literals, ...substitutions) {
    // return a string
}
```

具体接收参数可以看这个例子：

```js
let count = 10,
    price = 0.25,
    message = passthru`${count} items cost $${(count * price).toFixed(2)}.`;
```

passthru\(\)函数接收三个参数。

1. literals数组。包含元素：

   * 第一个substitution之前的空字符串`“”`
   * 第一个第二个substitution之间的字符串`“ items cost $”`
   * 第二个substitution之后的字符串`“.”`

2. `count`变量的interpreted value`10`，substitutions数组的第一个元素。

3. `(count * price).toFixed(2)`的interpreted值`"2.50"`，substitutions数组的第二个元素。

可以看出literals\[0\]总是字符串的开头，literals\[literals.length-1\]总是字符串的结尾。因此`substitutions.length === literals.length - 1`is always true。

因此，可以使用模板tag模拟template literal的默认行为：

```js
function passthru(literals, ...substitutions) {
    let result = "";

    // run the loop only for the substitution count
    for (let i = 0; i < substitutions.length; i++) {
        result += literals[i];
        result += substitutions[i];
    }

    // add the last literal
    result += literals[literals.length - 1];

    return result;
}

let count = 10,
    price = 0.25,
    message = passthru`${count} items cost $${(count * price).toFixed(2)}.`;

console.log(message);       // "10 items cost $2.50."
```

> substitutions中的值并不一定是string，如果一个表达式的结果是一个number，传入substitution的就是一个numeric value。决定这个值如何被输出是tag的工作。

#### Using Raw Values in Template Literals

template tags也可以获取raw string信息，主要是指获取character escapes转换成character equivalents之前的值。可以使用内置的`String.raw()`标签。

```js
let message1 = `Multiline\nstring`,
    message2 = String.raw`Multiline\nstring`;

console.log(message1);          // "Multiline
                                //  string"
console.log(message2);          // "Multiline\\nstring"
```

第一个参数是一个数组，数组有一个额外的属性叫做`raw`。因此，`literals[0]`有一个对应的值`literals.raw[0]`，是它的raw string information.

`String.raw()`是一个模板字符串的标签函数，它的作用类似于 Python 中的字符串前缀`r`和 C\# 中的字符串前缀`@`，是用来获取一个模板字符串的原始字面量值的。

`String.raw()`是唯一一个内置的模板字符串标签函数，因为它太常用了。不过它并没有什么特殊能力，你自己也可以实现一个和它功能一模一样的标签函数。

