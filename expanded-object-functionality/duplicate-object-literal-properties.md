## Duplicate Object Literal Properties

ES5严格模式下，对象字面量属性如果发生重复，会报错。

```js
"use strict";

var person = {
    name: "Nicholas",
    name: "Greg"        // syntax error in ES5 strict mode
};
```



