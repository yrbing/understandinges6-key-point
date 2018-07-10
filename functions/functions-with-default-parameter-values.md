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



