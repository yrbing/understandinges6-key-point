## Other String Changes

ECMAScript 6 扩展了 JavaScript 处理 string 的能力。

### Methods for Identifying Substrings 定位子串

`includes()`

`startsWith()`

`endsWith()`

每一个方法都接收两个参数：搜索的文本和可选的index。

事实上，第二个参数缩小了string被搜索的范围。

对于`endsWith()`，index为字符串长度取值，结束的位置为index-1。

```js
var msg = "Hello world!";

console.log(msg.startsWith("Hello"));       // true
console.log(msg.endsWith("!"));             // true
console.log(msg.includes("o"));             // true

console.log(msg.startsWith("o"));           // false
console.log(msg.endsWith("world!"));        // true
console.log(msg.includes("x"));             // false

console.log(msg.startsWith("o", 4));        // true
console.log(msg.endsWith("o", 8));          // true
console.log(msg.includes("o", 8));          // false
```

这三个方法只返回boolean值，如果需要找到一个string在另一个中的actual position，使用`indexOf()`或者lastIndexOf\(\)方法。

> 如果传入一个regular expression而不是string作为参数，`includes()`，`startsWith()`和`endsWith()`都会throw an error。`indexOf()`和`lastIndexOf()`会把正则表达式转换成string（虽然和想象的方式不太一样）

### The repeat\(\) Method

```js
console.log("x".repeat(3));         // "xxx"
console.log("hello".repeat(2));     // "hellohello"
console.log("abc".repeat(4));       // "abcabcabcabc"
```



