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

二者的一个不同之处在于，concise methods可以使用`super`\(discussed later in the “Easy Prototype Access with Super References” section\)，nonconcise methods则不可用。

> concise 方法 的 name 属性 的值是括号前面的 name。

### Computed Property Names

ES5及之前，我们可以在object instances上计算属性名，使用square brackets将属性括起来，而不是使用dot notation。

square brackets可以让我们用**variables**和**string literals**\(可能包含了不能使用在identifier中的字符串\)来指定属性名。

```js
var person = {},
    lastName = "last name";

person["first name"] = "Nicholas";
person[lastName] = "Zakas";

console.log(person["first name"]);      // "Nicholas"
console.log(person[lastName]);          // "Zakas"
```

另外，还可以在object literals中直接使用string literals作为属性名：

```js
var person = {
    "first name": "Nicholas"
};

console.log(person["first name"]);      // "Nicholas"
```

这种模式需要我们提前知道属性名，并且属性名可以用字符串字面量来表示。

但如果属性名“first name”是变量的值或者需要计算获得，在ES5中，则无法在object literals中使用它来定义属性。

在ES6中，computed property names是对象字面量语法的一部分，同样使用中括号：

```js
var lastName = "last name";

var person = {
    "first name": "Nicholas",
    [lastName]: "Zakas"
};

console.log(person["first name"]);      // "Nicholas"
console.log(person[lastName]);          // "Zakas"
```

对象字面量中的中括号说明属性名需要进行计算

```js
var suffix = " name";

var person = {
    ["first" + suffix]: "Nicholas",
    ["last" + suffix]: "Zakas"
};

console.log(person["first name"]);      // "Nicholas"
console.log(person["last name"]);       // "Zakas"
```



