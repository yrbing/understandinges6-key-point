## Template Literals

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

第一个参数是一个包括经JS解释（interpreted）的字面量字符串的数组。每一个随后的参数都是一个substitution的解释值。

