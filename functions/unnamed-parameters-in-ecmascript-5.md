## Working with Unnamed Parameters

JS函数没有限制传入参数的个数，可以比函数定义时的命名参数更少或者更多。默认参数值使得传入更少的参数的情况更加清晰，同时ES6也在寻求更好的处理传入参数比定义时更多的方法。

### Unnamed Parameters in ECMAScript 5

早期的JS提供了`arguments`对象，但使用`arguments`可能会非常笨重。

```js
function pick(object) {
    let result = Object.create(null);

    // start at the second parameter
    for (let i = 1, len = arguments.length; i < len; i++) {
        result[arguments[i]] = object[arguments[i]];
    }

    return result;
}

let book = {
    title: "Understanding ECMAScript 6",
    author: "Nicholas C. Zakas",
    year: 2015
};

let bookData = pick(book, "author", "year");

console.log(bookData.author);   // "Nicholas C. Zakas"
console.log(bookData.year);     // 2015
```

这个函数模拟了_Underscore.js_库的`pick()`方法。返回一个对象的属性的指定子集的拷贝。第一，看不出pick可以接收更多参数；第二，arguments包括了所有传递给方法的参数。所以遍历要从index=1开始。

ECMAScript 6 引入了 rest parameters 帮助解决这些问题。

### Rest Parameters

_rest parameter _一个命名参数前门加上三个点\(...\)。这个命名参数会成为一个包括余下所有传递给函数的参数的数组。仍然是`pick()`方法。

```js
function pick(object, ...keys) {
    let result = Object.create(null);

    for (let i = 0, len = keys.length; i < len; i++) {
        result[keys[i]] = object[keys[i]];
    }

    return result;
}
```

> Rest parameters do not affect a function’s`length`property, which indicates the number of named parameters for the function. The value of`length`for`pick()`in this example is 1 because only`object`counts towards this value.

#### Rest Parameter Restrictions

只能有一个rest parameter，而且必须是最后一个参数。

