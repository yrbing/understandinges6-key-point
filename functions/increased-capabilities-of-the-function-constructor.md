## Increased Capabilities of the Function Constructor

Function构造函数是JS中很少用到的功能，它可以动态的创建一个新函数。

传入构造函数的参数\(arguments\)是函数的参数\(parameters\)和函数体，都是字符串。

```js
var add = new Function("first", "second", "return first + second");

console.log(add(1, 1));     // 2
```

ES6增加了函数构造函数使用default parameters和rest parameters的能力。

```js
var add = new Function("first", "second = first",
        "return first + second");

console.log(add(1, 1));     // 2
console.log(add(1));        // 2
```

```js
var pickFirst = new Function("...args", "return args[0]");

console.log(pickFirst(1, 2));   // 1
```

增加default parameters和rest parameters**确保了Function构造函数和通过声明形式创建函数有同样的能力。**

