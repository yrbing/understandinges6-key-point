## Other String Changes

ECMAScript 6 扩展了 JavaScript 处理 string 的能力。

### Methods for Identifying Substrings

`includes()`

`startsWith()`

`endsWith()`

每一个方法都接收两个参数：搜索的文本和可选的index。对于`endsWith()`，index以为这结束的位置index-1。

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

这三个方法只返回boolean值，如果需要找到一个string在另一个中的actual position，

