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

**null被认为是合法的valid，因此在第三个例子里，不会用到默认值。**

### How Default Parameter Values Affect the arguments Object

  


