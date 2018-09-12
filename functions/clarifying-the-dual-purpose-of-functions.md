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

创建notAPerson时，不适用new调用Person\(\)，notAPerson的是undefined。在非严格模式下，在全局对象上set了一个name属性。

