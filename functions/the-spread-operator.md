## The Spread Operator

和 rest parameters 紧密相关的是 the spread operator。

rest parameters 允许你指定多个独立的参数合并为一个数组，the spread operator 允许你指定一个数组，对其进行拆分并且将每一个item当做单独的参数传入函数。

`Math.max() `方法：

```js
let value1 = 25,
    value2 = 50;

console.log(Math.max(value1, value2));      // 50
```



