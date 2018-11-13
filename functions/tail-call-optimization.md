## Tail Call Optimization

ES6对于函数的engine optimization。

tail call是指当一个函数是另一个函数体内的最后一个语句last statement。

```js
function doSomething() {
    return doSomethingElse();   // tail call
}
```



