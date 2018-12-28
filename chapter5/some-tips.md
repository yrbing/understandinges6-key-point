# 使用解构的几个小技巧

*本文内容来自Nicholas C. Zakas的《Understanding ECMAScript 6》。*

ES6简化了从对象和数组中获取数据的方法，解构可以把一个数据结构拆分成任意小的部分。我们在开发中经常使用对象和数组的解构来简化代码，以下几个很有用但经常被忽略的用法。

## Value Swapping

value swapping在排序算法中经常出现，在ES5中，我们需要第三个临时变量来完成两个数值的交换：

```js
// Swapping variables in ECMAScript 5
let a = 1,
    b = 2,
    tmp;

tmp = a;
a = b;
b = tmp;

console.log(a);     // 2
console.log(b);     // 1
```

in ECMAScript 6，数组解构赋值可以用来交换两个变量的值。

```js
// Swapping variables in ECMAScript 6
let a = 1,
    b = 2;

[ a, b ] = [ b, a ];

console.log(a);     // 2
console.log(b);     // 1
```

赋值运算符左边是解构模式语法，右边是临时创建的数组字面量。使用解构可以很大程度上简化代码，增加代码的可读性，同时也省去了创建新变量的开销。

## Use Rest Items to Create a Clone

在ES5中，我们经常使用`concat()`作为克隆数组的简便方法。`concat()`方法原意是用来连接两个数组。当无参数调用时，它会返回当前这个数组的克隆版本。

```js
// cloning an array in ECMAScript 5
var colors = [ "red", "green", "blue" ];
var clonedColors = colors.concat();

console.log(clonedColors);      //"[red,green,blue]"
```

在ES6中，可以使用rest items完成这个需求。

```js
// cloning an array in ECMAScript 6
let colors = [ "red", "green", "blue" ];
let [ ...clonedColors ] = colors;

console.log(clonedColors);      //"[red,green,blue]"
```

与concat()方法相比，使用解构能够更加清晰的表达开发者的意图，增加代码的易读性。

> Rest items 必须是解构数组的最后一个入口（the last entry），后面跟comma会报错。

## Destructured Parameters

解构还有一个非常有用的case，就是用在函数参数上。

我们有时候会面对这样的情景：一个JS函数除了接受几个固定参数外，还会接受一些可选参数。通常我们可能会使用一个`option`对象，将可选参数作为这个对象的属性。

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

这种方法是可用的，但是你并不能从函数定义上看出来这个函数期待的输入参数是什么，你需要去阅读函数体。

解构提供了一种新的思路，你可以使用数组解构或对象解构模式来代替这个`option`命名参数。

```js
function setCookie(name, value, { secure, path, domain, expires }) {

    // code to set the cookie
}

setCookie("type", "js", {
    secure: true,
    expires: 60000
});
```

解构模式里的函数参数也像普通参数一样，如果没有传入具体值，则置为`undefined`。

解构参数拥有所有解构的能力。你可以使用默认值（default values），混合对象和数组的模式（mix object and array patterns），以及不同于对象属性的变量名（use variable names that differ from the properties you’re reading from）。

### Destructured Parameters are Required

使用解构参数需要注意一点：默认情况下，如果在函数定义中的解构参数的位置上，你没有传入任何值，会发生报错。

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

在解构赋值中，如果赋值运算符右侧表达式的值是`null`或者`undefined`则会报错，因为你无法从`null`或者`undefined`中读取属性。

因此`setCookie()`函数在调用时，没有传入第三个参数会报错。

如果代码中，这个解构参数是必需的，这样做没有问题。如果希望解构参数是可选的，你可以给解构参数本身提供默认值。

```js
function setCookie(name, value, { secure, path, domain, expires } = {}) {

    // ...
}
```

### Default Values for Destructured Parameters

像解构赋值一样，可以给解构模式的参数提供默认值。

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

这样你就可以不必去check传入的解构参数有没有包含特定的属性，然后再给它正确的值。同时，因为整个解构参数本身也有默认值，因此这个函数参数是可选的。

建议在函数声明时，使用解构参数来替代你的“option”对象。一方面可以清晰表达函数需要的参数，同时还能够以较为简便的方式为可选参数提供默认值。