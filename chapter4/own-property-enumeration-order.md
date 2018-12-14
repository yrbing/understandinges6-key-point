## Own Property Enumeration Order

ES5没有定义对象属性的枚举顺序，而是留给了JS engine vendors来做这件事。

ES6严格地定义了对象属性的枚举顺序。这会影响我们在使用`Object.getOwnPropertyNames()`和`Reflect.ownkeys`时属性的返回。也会影响`Object.assign()`处理属性的顺序。

own property enumeration 的基本顺序是:

* All numeric keys in ascending order
* All string keys in the order in which they were added to the object
* All symbol keys (covered in Chapter 6) in the order in which they were added to the object

```js
var obj = {
    a: 1,
    0: 1,
    c: 1,
    2: 1,
    b: 1,
    1: 1
};

obj.d = 1;

console.log(Object.getOwnPropertyNames(obj).join(""));     // "012acbd"
```

> `for-in`循环仍然有一个未指定的枚举顺序，因为并非所有JavaScript引擎都以相同的方式实现它。 `Object.keys()`方法和`JSON.stringify()`都被指定使用与`for-in`相同（未指定）的枚举顺序。