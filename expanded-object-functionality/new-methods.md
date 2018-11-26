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

