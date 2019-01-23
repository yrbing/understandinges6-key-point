## Sharing Symbols

你可能会需要在代码的不同部分使用the same symbols。比如，你的应用中有两个不同的对象类型，需要使用同样的symbol属性来表示一个独特的标识符(suppose you have two different object types in your application that should use the same symbol property to represent a unique identifier)。

在跨文件或者大的代码库中追踪一个symbols是很难的，并且容易出错。因此ES6提供了一个全局symbol注册机制(a global symbol registry)，你可以在任何需要时候使用它。

当你想要创建一个以共享(share)为目的的symbol时，可以使用`Symbol.for()`方法代替调用`Symbol()`方法。`Symbol.for()`方法接受一个字符串标识符(string identifier)作为唯一的参数，这个参数也是symbol的description。

```js
let uid = Symbol.for("uid");
let object = {};

object[uid] = "12345";

console.log(object[uid]);       // "12345"
console.log(uid);               // "Symbol(uid)"
```

`Symbol.for()`方法首先搜索全局的symbol注册机制(global symbol registry)，检查是否已有使用了key值为`"uid"`的symbol。如果存在，方法返回已经存在的symbol，如果不存在，则使用这个key创建一个新的symbol，并将这个symbol注册到全局symbol登记处中，并且返回这个新的symbol。


```js
let uid = Symbol.for("uid");
let object = {
    [uid]: "12345"
};

console.log(object[uid]);       // "12345"
console.log(uid);               // "Symbol(uid)"

let uid2 = Symbol.for("uid");

console.log(uid === uid2);      // true
console.log(object[uid2]);      // "12345"
console.log(uid2);              // "Symbol(uid)"
```

在上面这个例子里, `uid` and `uid2` contain the same symbol，可以交换使用。第一次调用`Symbol.for()` creates the symbol，第二次调用retrieves the symbol from the global symbol registry.

共享symbols(shared symbols)的另一个独特的应用是，你可以通过调用`Symbol.keyFor()`方法，获取一个在global symbol registry中注册的symbol关联的key值：

```js
let uid = Symbol.for("uid");
console.log(Symbol.keyFor(uid));    // "uid"

let uid2 = Symbol.for("uid");
console.log(Symbol.keyFor(uid2));   // "uid"

let uid3 = Symbol("uid");
console.log(Symbol.keyFor(uid3));   // undefined
```

Notice that both `uid` and `uid2` return the `"uid"` key. The symbol uid3 doesn’t exist in the global symbol registry, so it has no key associated with it and `Symbol.keyFor()` returns `undefined`.

>对symbol keys使用命名空间：The global symbol registry is a shared environment, just like the global scope. That means you can’t make assumptions about what is or is not already present in that environment. Use namespacing of symbol keys to reduce the likelihood of naming collisions when using third-party components. For example, jQuery code might use "jquery." to prefix all keys, for keys like `"jquery.element"` or similar.