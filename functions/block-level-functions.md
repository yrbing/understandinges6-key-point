## 关键Block-Level Functions

在ES3及之前，出现在block中的函数声明是syntax error，但是所有的浏览器都支持这样做。但是每个浏览器都有些微的差别。因此最好的方式是避免在block中进行function declarations（最好的替代方法是使用function expression）。

为了尝试去抑制这种不兼容的行为，ES5严格模式引入了一个error。

```js
"use strict";

if (true) {

    // Throws a syntax error in ES5, not so in ES6
    function doSomething() {
        // ...
    }
}
```

在ES6中，函数被认为是block-level的声明，在same block中可以被access和called。

```js
"use strict";

if (true) {

    console.log(typeof doSomething);        // "function"

    function doSomething() {
        // ...
    }

    doSomething();
}

console.log(typeof doSomething);            // "undefined"
```

声明提升：块级函数会被提升到block的顶部，因此typeof返回function。

### Deciding When to Use Block-Level Functions

块级函数声明和使用let的函数表达式类似，当执行流到了block之外，函数定义都会被移除。关键的不同是声明提升，可以参考第一章let部分。

```js
"use strict";

if (true) {

    console.log(typeof doSomething);        // throws error

    let doSomething = function () {
        // ...
    }

    doSomething();
}

console.log(typeof doSomething);
```

代码会在执行到typeof时停止，因为let语句还没有被执行，所以doSomething\(\)在TDZ中。

因此，通过是否需要hoisting行为来决定使用block level functions或者let 表达式。

### Block-Level Functions in Nonstrict Mode

ES6同时也允许非严格模式的 block-level function，但行为略有不同。声明不是被提升到top of the block，而是被提升到function或者global environment。

```js
// ECMAScript 6 behavior
if (true) {

    console.log(typeof doSomething);        // "function"

    function doSomething() {
        // ...
    }

    doSomething();
}

console.log(typeof doSomething);            // "function"
```



