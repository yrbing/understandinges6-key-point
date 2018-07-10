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

  


