## Destructured Parameters

解构还有一个非常有用的case，就是在函数参数上。当一个JS函数接收一堆可选参数时，通常我们会使用一个`option`对象，将它的属性作为这些可选参数放置的地方。

```js
// properties on options represent additional parameters
function setCookie(name, value, options) {

    options = options || {};

    let secure = options.secure,
        path = options.path,
        domain = options.domain,
        expires = options.expires;

    // code to set the cookie
}

// third argument maps to options
setCookie("type", "js", {
    secure: true,
    expires: 60000
});
```

这种方法可用，但是你并不能从函数定义function definition上看出来这个函数期待的输入参数是什么，你需要去读函数体function body。

解构提供了一种替代方案，你可以使用数组或对象解构模式替代一个命名参数。

```js
function setCookie(name, value, { secure, path, domain, expires }) {

    // code to set the cookie
}

setCookie("type", "js", {
    secure: true,
    expires: 60000
});
```

解构参数也像普通参数一样，如果没有传入，则置为undefined。

> Destructured parameters have all of the capabilities of destructuring that you’ve learned so far in this chapter. You can use default values, mix object and array patterns, and use variable names that differ from the properties you’re reading from.

### Destructured Parameters are Required

使用解构参数需要注意的是：默认情况下，如果你没有传入任何值，会报错。

```js
// Error!
setCookie("type", "js");
```

出错的原因是：解构参数实际上是解构声明的简写，实际上JS引擎会对上述代码做以下工作：

```js
function setCookie(name, value, options) {

    let { secure, path, domain, expires } = options;

    // code to set the cookie
}
```

已知，赋值运算符右侧表达式的值是`null`或者`undefined`会报错。因此没传入第三个参数会报错。

如果你希望解构参数to be required，这样做没问题。如果希望解构参数to be optional，你可以给解构参数本身提供默认值。

```js
function setCookie(name, value, { secure, path, domain, expires } = {}) {

    // ...
}
```

### Default Values for Destructured Parameters

像解构赋值一样，可以给解构参数提供default value。

```js
function setCookie(name, value,
    {
        secure = false,
        path = "/",
        domain = "example.com",
        expires = new Date(Date.now() + 360000000)
    } = {}
) {

    // ...
}
```

这样你就可以不必去check传入的解构参数有没有包含特定的属性，然后再给它正确的值。
同时，整个解构参数本身也有默认值，因此这个函数参数是可选的。