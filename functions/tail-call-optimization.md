## Tail Call Optimization

ES6对于函数的engine optimization。

tail call是指当一个函数是另一个函数体内的最后一个语句last statement。

```js
function doSomething() {
    return doSomethingElse();   // tail call
}
```

在ES5引擎中，tail calls的实现方式和其他函数调用一样：一个新的**堆栈帧 stack frame **被创建，并且push到当前的调用堆栈 call stack** **中。这意味着每一个之前的堆栈帧都被存储在memory中，当调用对战很大时，可能会导致问题。

### What’s Different?



