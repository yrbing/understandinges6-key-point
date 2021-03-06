## ECMAScript 6’s name Property

JS定义函数的方式非常多，因此identifying函数变得很困难。匿名函数的普遍使用使得debug变得有一些困难。因此，ES6给所有函数增加了`name`属性。

### Choosing Appropriate Names

ES6中所有函数都有`name`属性。

function declarations and function expressions——

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

### Special Cases of the name Property

Both getter and setter functions must be retrieved using`Object.getOwnPropertyDescriptor()`.

```js
var doSomething = function doSomethingElse() {
    // ...
};

var person = {
    get firstName() {
        return "Nicholas"
    },
    sayName: function() {
        console.log(this.name);
    }
}

console.log(doSomething.name);      // "doSomethingElse"
console.log(person.sayName.name);   // "sayName"

var descriptor = Object.getOwnPropertyDescriptor(person, "firstName");
console.log(descriptor.get.name); // "get firstName"
```

使用bind\(\)创建的函数和使用`Function`constructor创建的函数——

```js
var doSomething = function() {
    // ...
};

console.log(doSomething.bind().name);   // "bound doSomething"

console.log((new Function()).name);     // "anonymous"
```

**name属性只是用来获取信息的，并不refer to同名的变量。**Keep in mind that the value of`name`for any function does not necessarily refer to a variable of the same name. The`name`property is meant to be informative, to help with debugging, so there’s no way to use the value of`name`to get a reference to the function.



