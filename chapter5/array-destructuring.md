## Array Destructuring

数组解构使用数组字面量语法形式，相对于对象解构使用命名属性，数组解构使用数组元素的位置。

```js
let colors = [ "red", "green", "blue" ];

let [ firstColor, secondColor ] = colors;

console.log(firstColor);        // "red"
console.log(secondColor);       // "green"
```

你也可以在解构模式中忽略一些元素，只获取想要的元素。
 
```js
let colors = [ "red", "green", "blue" ];

let [ , , thirdColor ] = colors;

console.log(thirdColor);        // "blue"
```

`thirdColor`前面的逗号，是数组元素的占位符placeholders。

> Similar to object destructuring, you must always provide an initializer when using array destructuring with `var`, `let`, or `const`.

### Destructuring Assignment

可以使用array destructuring in the context of an assignment, *不需要用括号*。

```js
let colors = [ "red", "green", "blue" ],
    firstColor = "black",
    secondColor = "purple";

[ firstColor, secondColor ] = colors;

console.log(firstColor);        // "red"
console.log(secondColor);       // "green"
```

数组解构赋值在交换两个变量的值上，有非常神奇的用法。value swapping 是在排序算法中经常出现的，ES5的方法需要第三个临时变量来完成交换两个数的值：

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

in ECMAScript 6，数组解构赋值:

```js
// Swapping variables in ECMAScript 6
let a = 1,
    b = 2;

[ a, b ] = [ b, a ];

console.log(a);     // 2
console.log(b);     // 1
```

赋值运算符左边是解构模式，右边是临时创建的数组字面量。

> Like object destructuring assignment, an error is thrown when the right side of an array destructured assignment expression evaluates to `null` or `undefined`.

### Default Values

数组解构赋值，指定default value。当指定位置不存在属性，或者为`undefined`时，使用默认值。

```js
let colors = [ "red" ];

let [ firstColor, secondColor = "green" ] = colors;

console.log(firstColor);        // "red"
console.log(secondColor);       // "green"
```

### Nested Destructuring

```js
let colors = [ "red", [ "green", "lightgreen" ], "blue" ];

// later

let [ firstColor, [ secondColor ] ] = colors;

console.log(firstColor);        // "red"
console.log(secondColor);       // "green"
```

As with objects, you can nest arrays arbitrarily deep.

### Rest Items

Chapter3介绍了函数的 rest parameters，数组解构也有类似的概念叫做 rest items。 rest items使用 `...` 语法，将数组中剩余的元素赋值给一个特定的变量。

```js
let colors = [ "red", "green", "blue" ];

let [ firstColor, ...restColors ] = colors;

console.log(firstColor);        // "red"
console.log(restColors.length); // 2
console.log(restColors[0]);     // "green"
console.log(restColors[1]);     // "blue"
```

rest items 非常适合用来抽取数组的特定元素们，**可以替代一部分Array.prototype.slice()的工作，只传入一个参数的时候**

**rest items 还有一个非常有用而且经常被忽略的作用：create a clone。** 在ES5中，开发者频繁使用`concat()`作为克隆数组的简便方法（用`slice()`是不是也可以）：

```js
// cloning an array in ECMAScript 5
var colors = [ "red", "green", "blue" ];
var clonedColors = colors.concat();

console.log(clonedColors);      //"[red,green,blue]"
```

`concat()`方法原本是用来连接两个数组。当无参数调用时，它会返回a clone of the array。

在ES6中，可以使用 rest items。这比使用concat()方法更加清晰的表达了开发者的意图。

```js
// cloning an array in ECMAScript 6
let colors = [ "red", "green", "blue" ];
let [ ...clonedColors ] = colors;

console.log(clonedColors);      //"[red,green,blue]"
```

> Rest items 必须是解构数组的最后一个入口the last entry，后面跟comma会报错。