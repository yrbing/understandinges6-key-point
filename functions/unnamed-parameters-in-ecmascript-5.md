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

ECMAScript 6 引入了 rest parameters 帮助解决这些问题。

### Rest Parameters

  


