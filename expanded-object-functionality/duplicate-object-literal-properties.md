## Duplicate Object Literal Properties

ES5严格模式下，对象字面量属性如果发生重复，会报错。

```js
"use strict";

var person = {
    name: "Nicholas",
    name: "Greg"        // syntax error in ES5 strict mode
};
```

在ES6中，重复属性的检测被移除了，无论是严格模式还是非严格模式。

```js
"use strict";

var person = {
    name: "Nicholas",
    name: "Greg"        // no error in ES6 strict mode
};

console.log(person.name);       // "Greg"
```



