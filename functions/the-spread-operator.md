## The Spread Operator

和 rest parameters 紧密相关的是 the spread operator。

rest parameters 允许你指定多个独立的参数合并为一个数组，the spread operator 允许你指定一个数组，对其进行拆分并且将每一个item当做单独的参数传入函数。

`Math.max()`方法，接受许多number参数，返回其中最大的一个：

```js
let value1 = 25,
    value2 = 50;

console.log(Math.max(value1, value2));      // 50
```

如果只有两个值，`Math.max()`使用起来很简单。但万一你碰到的是一个数组，`Math.max()`不允许传入数组，因此在ES5及之前，要么遍历这个数组，要么使用`apply()`方法：

```js
let values = [25, 50, 75, 100]

console.log(Math.max.apply(Math, values));  // 100
```



