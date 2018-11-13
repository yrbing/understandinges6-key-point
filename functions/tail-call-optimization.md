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

ES6 对特定的tail calls 缩减了call stack的大小，仅仅在严格模式下\(nonstrict mode tail calls are left untouched\)。不再创建一个新的堆栈帧，而是清空当前的堆栈帧，并且重用之。

前提是满足以下条件：

1. tail call 不需要获取current stack frame的变量（非闭包）
2. tail call 返回后，函数没有其他后续工作要做
3. tail call的结果被当做函数的值返回

以下为正反几个例子：

```js
"use strict";

function doSomething() {
    // optimized
    return doSomethingElse();
}
```

```js
"use strict";

function doSomething() {
    // not optimized - no return
    doSomethingElse();
}
```

tail call 返回之后还有操作：

```js
"use strict";

function doSomething() {
    // not optimized - must add after returning
    return 1 + doSomethingElse();
}
```

```js
"use strict";

function doSomething() {
    // not optimized - call isn't in tail position
    var result = doSomethingElse();
    return result;
}
```

闭包：

```js
"use strict";

function doSomething() {
    var num = 1,
        func = () => num;

    // not optimized - function is a closure
    return func();
}
```

### How to Harness Tail Call Optimization

实际上，因为tail call 优化发生在幕后，因此除非你想要优化函数的执行，否则不需要考虑它。

tail call optimization 最主要的应用场景是 递归函数 recursive functions，优化效果最好。

考虑如下阶乘函数：

```js
function factorial(n) {

    if (n <= 1) {
        return 1;
    } else {

        // not optimized - must multiply after returning
        return n * factorial(n - 1);
    }
}
```

函数无法被优化，因为乘法发生在factorial迭代调用之后。因此需要把乘法从return语句中拿出来。

```js
function factorial(n, p = 1) {

    if (n <= 1) {
        return 1 * p;
    } else {
        let result = n * p;

        // optimized
        return factorial(n - 1, result);
    }
}
```

当你写一个递归函数的时候，考虑一下tail call优化。会有非常显著的性能优化，尤其是在computationally-expensive function中。

