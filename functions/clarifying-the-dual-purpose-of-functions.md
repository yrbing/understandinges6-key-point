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

`Person`的首字母大写**只是一个指示器**，表示这个函数应该使用`new`调用。在JS程序中普遍这样使用。

函数的双重角色令人困惑，因此在ES6中做了一些改变。

JS函数有两个不同的仅内部可用的方法：`[[Call]]`and`[[Construct]]`。当一个函数被调用时没有使用 `new`，则`[[Call]]`方法被执行，执行函数body中的代码（which executes the body of the function as it appears in the code）。当一个函数被调用时使用了 `new`，则`[[Construct]]`方法被执行。`[[Construct]]`方法负责创建一个新对象，叫做 new target，然后执行这个函数body，并且将`this`设置为这个new target。（ The`[[Construct]]`method is responsible for creating a new object, called the n_ew target_, and then executing the function body with`this`set to the new target.）

