## Retrieving Symbol Properties

`Object.keys()`和`Object.getOwnPropertyNames()`方法可用来检索一个对象的属性名。`Object.keys()`方法会返回一个由给定对象的自身可枚举属性组成的数组，Object.getOwnPropertyNames()方法返回一个由指定对象的所有自身属性的属性名（包括不可枚举属性但不包括Symbol值作为名称的属性）组成的数组。两种方法都不会返回Symbol值作为名称的属性名, 以保留其ECMAScript 5功能。

ES6增加了`Object.getOwnPropertySymbols()`方法，用来从对象中检索Symbols属性。

`Object.getOwnPropertySymbols()`的返回值是一个包含own property symbols的数组。

```js
let uid = Symbol.for("uid");
let object = {
    [uid]: "12345"
};

let symbols = Object.getOwnPropertySymbols(object);

console.log(symbols.length);        // 1
console.log(symbols[0]);            // "Symbol(uid)"
console.log(object[symbols[0]]);    // "12345"
```