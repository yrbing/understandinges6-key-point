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

ES6增加了Object.assign\(\)方法。之所以用assign而不是mixin，是因为assign反应了实际上发生的操作，mixin\(\)方法使用了assignment operator\(`=`\)，因此无法将寄存器属性\(accessor properties\)复制到receiver上仍作为寄存器属性。

> Similar methods in various libraries may have other names for the same basic functionality; popular alternates include the`extend()`and`mix()`methods. There was also, briefly, an`Object.mixin()`method in ECMAScript 6 in addition to the`Object.assign()`method. The primary difference was that`Object.mixin()`also copied over accessor properties, but the method was removed due to concerns over the use of`super`\(discussed in the “Easy Prototype Access with Super References” section of this chapter\).

没明白，看到后面再说好了？！！！！！！！！！！

任何地方使用mixin\(\)方法的，都可以替换成Object.assign\(\)。

```js
function EventTarget() { /*...*/ }
EventTarget.prototype = {
    constructor: EventTarget,
    emit: function() { /*...*/ },
    on: function() { /*...*/ }
}

var myObject = {}
Object.assign(myObject, EventTarget.prototype);

myObject.emit("somethingChanged");
```

Object.assign\(\)方法接受多个suppliers，receiver按照传入顺序receive属性。因此后面的supplier可能会overwrite前面的supplier的提供的参数。

```js
var receiver = {};

Object.assign(receiver,
    {
        type: "js",
        name: "file.js"
    },
    {
        type: "css"
    }
);

console.log(receiver.type);     // "css"
console.log(receiver.name);     // "file.js"
```

Object.assign\(\)方法不是ECMAScript 6的重要补充，而是公共函数的标准化。

当supplier有存取器属性时，Object.assign\(\)会在receiver上增加一个数据属性\(data property\)。因为使用的是assignment operator。

```js
var receiver = {},
    supplier = {
        get name() {
            return "file.js"
        }
    };

Object.assign(receiver, supplier);

var descriptor = Object.getOwnPropertyDescriptor(receiver, "name");

console.log(descriptor.value);      // "file.js"
console.log(descriptor.get);        // undefined
```



