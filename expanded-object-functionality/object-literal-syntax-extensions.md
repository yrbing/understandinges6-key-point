## Object Literal Syntax Extensions

The object literal is one of the most popular patterns in JavaScript. JSON is built upon its syntax, and it’s in nearly every JavaScript file on the Internet. The object literal is so popular because it’s a succinct syntax for creating objects that otherwise would take several lines of code. Luckily for developers, ECMAScript 6 makes object literals more powerful and even more succinct by extending the syntax in several ways.

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

  

