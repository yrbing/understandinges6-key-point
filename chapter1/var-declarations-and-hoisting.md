## Var Declarations and Hoisting

_hoisting（作用域提升）：_

用var声明的变量，被提升到了函数的顶部（或者global scope，如果是在函数外声明），不论它实际是在哪里声明的。



```js
function getValue(condition) {

    if (condition) {
        var value = "blue";

        // other code

        return value;
    } else {

        // value exists here with a value of undefined

        return null;
    }

    // value exists here with a value of undefined
}
```

事实上，无论condition是否为true，变量value都被创建了。

