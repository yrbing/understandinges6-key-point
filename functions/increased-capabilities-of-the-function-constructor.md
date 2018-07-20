## Increased Capabilities of the Function Constructor

Function构造函数是JS中很少用到的功能，它可以动态的创建一个新函数。

```js
var add = new Function("first", "second", "return first + second");

console.log(add(1, 1));     // 2
```



