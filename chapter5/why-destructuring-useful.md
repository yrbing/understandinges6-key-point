## Why is Destructuring Useful?

ES5及之前，从对象和数组中获取信息需要很多重复的代码。

```js
let options = {
        repeat: true,
        save: false
    };

// extract data from the object
let repeat = options.repeat,
    save = options.save;
```

ES6增加了对象和数组的解构。并且使用了熟悉的语法：对象和数组字面量的语法。

