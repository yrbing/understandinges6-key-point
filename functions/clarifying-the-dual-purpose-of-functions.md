## Clarifying the Dual Purpose of Functions

In ECMAScript 5 and earlier, functions serve the dual purpose of being callable with or without`new`.

当使用`new`时，函数内部的`this`是一个新的对象，并且会返回这个新对象。

```js
function Person(name) {
    this.name = name;
}

var person = new Person("Nicholas");
var notAPerson = Person("Nicholas");

console.log(person);        // "[Object object]"
console.log(notAPerson);    // "undefined"
```

创建`notAPerson`时，不使用`new`调用`Person()`，`notAPerson`的值是`undefined`。（在非严格模式下，在全局对象上set了一个`name`属性。）

`Person`的首字母大写只是一个指示器，表示这个函数应该使用`new`调用。在JS程序中普遍这样使用。

函数的双重角色令人困惑，因此在ES6中做了一些改变。

