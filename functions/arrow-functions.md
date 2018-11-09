## Arrow Functions

箭头函数和传统JS函数在行为上有一些重要的不同：

* **没有 this，super，arguments，new.target bindings**
  * this，super，arguments，new.target 的值是由最近的包裹箭头函数的 noarrow function 决定的。\(`super`is covered in Chapter 4.\)
* **不能使用new调用**
  * 箭头函数没有`[[Construct]]`方法
* **没有原型 No prototype**
  * 不能使用new，因此不需要prototype
* **不能改变this**
  * 函数内的this值不能被改变，在整个函数生命周期中保持一样。It remains the same throughout the entire lifecycle of the function.
* **没有arguments对象**
  * 箭头函数没有arguments binding，因此需要依赖 named parameters 和 rest parameters 来获取函数参数。
* 不允许重复名称的参数 **No duplicate named parameters**
  * strict or nostrict mode，noarrow gunction 只有在严格模式才不能用重复名字的参数

> 减少错误和歧义。First and foremost, `this`binding is a common source of error in JavaScript.
>
> 优化性能。Second，通过限制this的值为唯一的，JS引擎可以更加容易地**优化函数执行**。普通函数可能被用作 constructor，或者被修改。

箭头函数也有name属性。

### Arrow Function Syntax

只有一个参数，直接使用

```js
var reflect = value => value;

// effectively equivalent to:

var reflect = function(value) {
    return value;
};
```

超过一个参数，parentheses

```js
var sum = (num1, num2) => num1 + num2;

// effectively equivalent to:

var sum = function(num1, num2) {
    return num1 + num2;
};
```

没有参数，parentheses

```js
var getName = () => "Nicholas";

// effectively equivalent to:

var getName = function() {
    return "Nicholas";
};
```

传统函数体，用braces包裹，同时清晰的定义返回值。

```js
var sum = (num1, num2) => {
    return num1 + num2;
};

// effectively equivalent to:

var sum = function(num1, num2) {
    return num1 + num2;
};
```

一个啥也不干的函数

```js
var doNothing = () => {};

// effectively equivalent to:

var doNothing = function() {};
```

返回一个对象字面量，又不想用传统函数体

```js
var getTempItem = id => ({ id: id, name: "Temp" });

// effectively equivalent to:

var getTempItem = function(id) {

    return {
        id: id,
        name: "Temp"
    };
};
```

### Creating Immediately-Invoked Function Expressions

JS中函数最popular的用法就是创建一个IIEFs。IIEFs可以让你定义一个匿名函数，并且马上调用它，而且不需要saving a reference。

当你想要创建一个scope，shielded from  the rest of a program。

```js
let person = function(name) {

    return {
        getName: function() {
            return name;
        }
    };

}("Nicholas");

console.log(person.getName());      // "Nicholas"
```

IIEF非常有效的让name变成了返回对象的私有成员。

把箭头函数用parentheses包裹：

```js
let person = ((name) => {

    return {
        getName: function() {
            return name;
        }
    };

})("Nicholas");

console.log(person.getName());      // "Nicholas"
```

注意：括号只包裹箭头函数的定义，不包括传参。和formal函数不同，括号包裹传参或者函数定义都可以。

### No this Binding

  


