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

>Similar to object destructuring, you must always provide an initializer when using array destructuring with var, let, or const.

### Destructuring Assignment

### Default Values

### Nested Destructuring

### Rest Items