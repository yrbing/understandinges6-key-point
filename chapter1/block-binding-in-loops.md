## Block Binding in Loops

#### Functions in Loops {#leanpub-auto-functions-in-loops}

```javascript
var funcs = [];

for (var i = 0; i < 10; i++) {
    funcs.push(function() { console.log(i); });
}

funcs.forEach(function(func) {
    func();  // outputs the number "10" ten times
});
```

To fix this problem, developers use **immediately-invoked function expressions \(IIFEs\) **inside of loops to force a new copy of the variable they want to iterate over to be created, as in this example:

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

上面这个例子在循环中用到了IIFE，块级绑定`let`和`const`可以简化这个循环。

#### Let Declarations in Loops {#leanpub-auto-let-declarations-in-loops}

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



