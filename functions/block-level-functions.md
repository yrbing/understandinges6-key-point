## Block-Level Functions

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



