## New Methods

从ES5开始，ECMAScript的设计目标之一就是，避免增加新的全局函数，以及增加`Object.prototype`的方法。As a result, the

`Object`global has received an increasing number of methods when no other objects are more appropriate.

ES6在`Object`全局上引入了一些新方法。

### The Object.is\(\) Method

比较JS中的两个值：

* equals operator\(==\)：类型转换
* identically equals operator \(`===`\)：
  * +0 和 -0 被认为是相等的，但在JS引擎中它们是不同的
  * `NaN === Nan` 返回 `false`，因此必须使用`isNaN()`来正确的检测 `NaN`

ES6引入了 `Object.is()`方法，弥补了全等操作符的不足之处。两个值如果是 same type, same value则被认为是相等的。

```js
console.log(+0 == -0);              // true
console.log(+0 === -0);             // true
console.log(Object.is(+0, -0));     // false

console.log(NaN == NaN);            // false
console.log(NaN === NaN);           // false
console.log(Object.is(NaN, NaN));   // true

console.log(5 == 5);                // true
console.log(5 == "5");              // true
console.log(5 === 5);               // true
console.log(5 === "5");             // false
console.log(Object.is(5, 5));       // true
console.log(Object.is(5, "5"));     // false
```

大多数情况下，Object.is\(\) 和 === 操作符是一致的。唯一的不同在于 +0 和 -0，NaN。

### The Object.assign\(\) Method

_Mixins_是JavaScript中最常用的对象组合\(object composition\)模式。在一个mixin中，一个对象接收另一个对象的属性和方法。很多JS库都有一个类似的mixin方法：

```js
function mixin(receiver, supplier) {
    Object.keys(supplier).forEach(function(key) {
        receiver[key] = supplier[key];
    });

    return receiver;
}
```

mixin\(\)方法遍历supplier的自由属性，并将其copu到receiver上（**shallow copy**）。

```js
function EventTarget() { /*...*/ }
EventTarget.prototype = {
    constructor: EventTarget,
    emit: function() { /*...*/ },
    on: function() { /*...*/ }
};

var myObject = {};
mixin(myObject, EventTarget.prototype);

myObject.emit("somethingChanged");
```

ES6增加了Object.assign\(\)方法。之所以用assign而不是mixin，是因为assign反应了实际上发生的操作，mixin\(\)方法使用了assignment operator\(=\)，因此无法将寄存器属性\(accessor properties\)复制到receiver上仍作为寄存器属性。

