## Global Block Bindings

let， const 和 var 不同的另一个地方就是：在 global scope 中的行为。

**var 在 global scope：**创建一个全局变量 global variable，并且是全局对象 global object \( `window` in browsers\) 的一个属性。因此你可能会不小心覆盖了一个已经存在的全局变量。

```js
// in a browser
var RegExp = "Hello!";
console.log(window.RegExp);     // "Hello!"

var ncz = "Hi!";
console.log(window.ncz);        // "Hi!"
```

**let 或者 const 在 global scope：**在 global scope 中创建了一个新的 binding，但没有给全局对象添加任何属性。因此不能用 let 或 const **overwrite** 一个 全局变量，只能 **shadow** it。

