## ECMAScript 6’s name Property

JS定义函数的方式非常多，因此identifying函数变得很困难。匿名函数的普遍使用使得debug变得有一些困难。因此，ES6给所有函数增加了`name`属性。

### Choosing Appropriate Names

ES6中所有函数都有`name`属性。

```js
function doSomething() {
    // ...
}

var doAnotherThing = function() {
    // ...
};

console.log(doSomething.name);          // "doSomething"
console.log(doAnotherThing.name);       // "doAnotherThing"
```



