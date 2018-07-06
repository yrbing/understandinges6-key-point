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

虽然在主要的JS引擎中，这样做都可以达到目的，但是这个行为被定义为一个bug，很多开发者不推荐这么做。

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

倒引号backticks中的所有空格都会成为string的一部分，因此小心使用indentation。

```js
let message = `Multiline
               string`;

console.log(message);           // "Multiline
                                //                 string"
console.log(message.length);    // 31
```

### Making Substitutions

### 

### Tagged Templates



