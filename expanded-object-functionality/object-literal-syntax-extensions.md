## Object Literal Syntax Extensions

Luckily for developers, ECMAScript 6 makes object literals more powerful and even more succinct by extending the syntax in several ways.

### Property Initializer Shorthand

在ES5和之前，对象字面量是简单的name-value pairs。属性值初始化时可能会有重复。

```js
function createPerson(name, age) {
    return {
        name: name,
        age: age
    };
}
```

ES6消除了这个冗余：

```js
function createPerson(name, age) {
    return {
        name,
        age
    };
}
```

当一个对象字面量的属性只有一个name，JS引擎查找包含的scope中同名的变量。并且赋值给对象字面量属性。

### Concise Methods

在ES5和之前，在对象中增加方法，必须指定一个name，以及完整的函数定义。

```js
var person = {
    name: "Nicholas",
    sayName: function() {
        console.log(this.name);
    }
};
```

ES6:

```js
var person = {
    name: "Nicholas",
    sayName() {
        console.log(this.name);
    }
};
```

二者的一个不同之处在于，concise methods需要使用super\(discussed later in the “Easy Prototype Access with Super References” section\)，nonconcise methods则不需要。

