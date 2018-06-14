## 

## 

## Block Binding in Loops

我们最想要的是 throwaway counter variable 一次性使用的计算变量。

### Functions in Loops

```javascript
var funcs = [];

for (var i = 0; i < 10; i++) {
    funcs.push(function() { console.log(i); });
}

funcs.forEach(function(func) {
    func();  // outputs the number "10" ten times
});
```

这是因为 i 在循环的每个迭代中是** share **的**，**循环里面创建的函数都保存着一份对同一变量的** reference**。当循环结束时，变量 i 的值是 10。

（That’s because `i`is **shared** across each iteration of the loop, meaning the functions created inside the loop all hold a **reference** to the same variable.）

为了解决这个问题，在循环中使用 **immediately-invoked function expressions \(IIFEs\)  :**

```javascript
var funcs = [];
for (var i = 0; i < 10; i++) {
    funcs.push((function(value) {
        return function() {
            console.log(value);
        }
    }(i)));
}

funcs.forEach(function(func) {
    func();     // outputs 0, then 1, then 2, up to 9
});
```

上面这个例子在循环中用到了IIFE。

块级绑定`let`和`const`可以简化这个循环。

### Let Declarations in Loops

```js
var funcs = [];
for (let i = 0; i < 10; i++) {
    funcs.push(function() {
        console.log(i);
    });
}

funcs.forEach(function(func) {
    func();     // outputs 0, then 1, then 2, up to 9
})
```

每一次循环，let 声明创建了一个新的变量 i 。所以每一次循环创建的函数都得到了一份属于自己的 i 的拷贝。

对于`for-in`和 `for-of`来说也是一样的。

#### **It’s important to understand**

> **let 声明在 loops 中的行为是在标准中特别定义的（specially-defined behavior in the specification）。**
>
> **和 let 的 non-hoisting 特性并没有什么必然联系。**
>
> **事实上，早期的 let 并没有这个行为，是在发展过程中后来加上的。**

### Constant Declarations in Loops

ECMAScript 6 规范没有明确的不允许在 loops 中应用 const 声明。

然而，使用不同类型的loop，行为是不同的。

