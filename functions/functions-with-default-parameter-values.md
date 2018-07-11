## Functions with Default Parameter Values

JS中的函数比较特别，因为它允许传入任意个数的参数，而不用理会函数定义时声明的参数个数。

### Simulating Default Parameter Values in ECMAScript 5

```js
function makeRequest(url, timeout, callback) {

    timeout = timeout || 2000;
    callback = callback || function() {};

    // the rest of the function

}
```

没有明确提供的函数参数将被设定为`undefined`，因此使用逻辑或（logical OR operator）可以为缺失的参数提供默认值。

这个方法的缺陷在于，如果函数的有效参数可能为0，也仍然会被替换。

更安全的替代方法使用typeof判断参数类型：

```js
function makeRequest(url, timeout, callback) {

    timeout = (typeof timeout !== "undefined") ? timeout : 2000;
    callback = (typeof callback !== "undefined") ? callback : function() {};

    // the rest of the function

}
```

### Default Parameter Values in ECMAScript 6

ES6通过初始化给参数提供默认值，如果参数没有被正式的传递过来。

```js
function makeRequest(url, timeout = 2000, callback = function() {}) {

    // the rest of the function

}
```

如果三个参数都传递了，defaults不会被使用。

```js
// uses default timeout and callback
makeRequest("/foo");

// uses default callback
makeRequest("/foo", 500);

// doesn't use defaults
makeRequest("/foo", 500, function(body) {
    doSomething(body);
});
```

url是必需的，其他两个参数是可选的。

可以给任意参数提供默认值。

```js
function makeRequest(url, timeout = 2000, callback) {

    // the rest of the function

}
```

timeout默认值只有在以下情况被用到：1、没有第二个参数传入；2、第二个参数明确的传入`undefined`。

```js
// uses default timeout
makeRequest("/foo", undefined, function(body) {
    doSomething(body);
});

// uses default timeout
makeRequest("/foo");

// doesn't use default timeout
makeRequest("/foo", null, function(body) {
    doSomething(body);
});
```

**null被认为是合法的（valid），因此在第三个例子里，不会用到默认值。**

### How Default Parameter Values Affect the arguments Object

ES5 nostrict mode，`arguments`对象反应了命名参数的变化。

```js
function mixArgs(first, second) {
    console.log(first === arguments[0]);
    console.log(second === arguments[1]);
    first = "c";
    second = "d";
    console.log(first === arguments[0]);
    console.log(second === arguments[1]);
}

mixArgs("a", "b");
```

输出：

```js
true
true
true
true
```

ES5严格模式

```js
function mixArgs(first, second) {
    "use strict";

    console.log(first === arguments[0]);
    console.log(second === arguments[1]);
    first = "c";
    second = "d"
    console.log(first === arguments[0]);
    console.log(second === arguments[1]);
}

mixArgs("a", "b");
```

输出：

```js
true
true
false
false
```

`arguments`对象在应用ES6默认参数的函数中，和ES5严格模式的表现是一样的，无论这个函数是否在严格模式运行。

**由于默认参数值的出现，导致**`arguments`**对象和函数的命名参数保持分离。（如果没有默认参数值，在非严格模式下，就走ES5 nostrict那一套了。）**

```js
// not in strict mode
function mixArgs(first, second = "b") {
    console.log(arguments.length);
    console.log(first === arguments[0]);
    console.log(second === arguments[1]);
    first = "c";
    second = "d"
    console.log(first === arguments[0]);
    console.log(second === arguments[1]);
}

mixArgs("a");
```

输出：

```js
1
true
false
false
false
```

`arguments[1]`的值是`undefined`。

改变参数的值不会影响到arguments，在严格模式和非严格模式都是如此，因此`arguments`总是反映着初始的调用状态。

### Default Parameter Expressions

默认参数值，需要是一个原始值（primitive value）。

可以通过执行一个函数获取这个默认参数值。

```js
function getValue() {
    return 5;
}

function add(first, second = getValue()) {
    return first + second;
}

console.log(add(1, 1));     // 2
console.log(add(1));        // 6
```

getValue\(\)只有在add\(\)被调用时没有第二个参数时才会执行。

```js
let value = 5;

function getValue() {
    return value++;
}

function add(first, second = getValue()) {
    return first + second;
}

console.log(add(1, 1));     // 2
console.log(add(1));        // 6
console.log(add(1));        // 7
```

> 注意使用函数时的括号。如果写的是second = getValue，传入的是一个引用而不是函数执行的值。

可以使用前面的参数作为后面参数的默认值。

```js
function add(first, second = first) {
    return first + second;
}

console.log(add(1, 1));     // 2
console.log(add(1));        // 2
```

再进一步，可以把前一个参数传入一个函数中，来获取后面的参数的值。

```js
function getValue(value) {
    return value + 5;
}

function add(first, second = getValue(first)) {
    return first + second;
}

console.log(add(1, 1));     // 2
console.log(add(1));        // 7
```



