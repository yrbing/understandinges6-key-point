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

### Making Substitutions

### 

### Tagged Templates



