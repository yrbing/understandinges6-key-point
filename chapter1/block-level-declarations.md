## Block-Level Declarations

Block scopes, also called lexical scopes（词法作用域）：

1. 在function内部

2. 在一个block内部（被“{”和“}”包含）

### Let Declarations

1. 块级作用域

2. no declaration hoisting 不会声明提升

3. no redeclaration 不能重复声明

**No Redeclaration**

如果一个标识符（identifier）已经被定义在某个scope，在这个scope种用 let 声明这个标识符会抛出error：

```js
var count = 30;

// Syntax error
let count = 40;
```

但如果在子scope中，则不会报错：

在if块中，新的变量覆盖了global的count变量。

```js
var count = 30;

// Does not throw an error
if(condition) {
    let count = 40;
    // more code
}
```

### Constant Declarations

用const声明的变量被认为是constants, 一旦被定义则无法修改它们的值。

因此，每个const变量，都必须在声明的时候被初始化：

```js
// Valid constant
const maxItems = 30;

// Syntax error: missing initialization
const name;
```

### Constants vs Let Declarations

相同点

1. 块级作用域

2. no declaration hoisting 不会声明提升

3. no redeclaration 不能重复声明

```js
var message = "Hello!";
let age = 25;

// Each of these would throw an error.
const message = "Goodbye!";
const age = 30;
```

不同点

1. const 不能重复赋值（objects有其特殊性）

```javascript
const maxItems = 5;
maxItems = 6; // throws error
```

像其他语言的const一样，maxItems变量不能被赋予一个新值。但和其他语言不同的是，如果const存储的是一个对象，它的值是可能可以改变的。

**Declaring Objects with Const**

`const` 阻止对binding的修改，但并不阻止对bound value的修改。

```js
const person = {
    name: "Nicholas"
};

// work
person.name = "Greg";

// throws an error
person = {
    name:"Greg"
};
```

### The Temporal Dead Zone \(TDZ\)

TDZ: 描述为什么 let 和 const 变量在声明之前不能获取。

**任何尝试在TDZ中获取变量的操作都会导致runtime error。**

使用`let`或`const`声明的变量直到声明之后才能被获取。

```javascript
if (condition) {
    console.log(typeof value);  // ReferenceError!
    let value = "blue";
}
```

上面的 typeof 语句执行时，value 在 TDZ 中是存在的。

That variable is only removed from the TDZ, and therefore safe to use, once execution flows to the variable declaration.

即使是使用 `typeof` 这个一般情况下比较safe的运算符时也是如此。但是，如果你是在变量声明的block外面：

```javascript
console.log(typeof value);  // "undefined"
if (condition) {
    let value = "blue";
}
```

`typeof`运算符执行时，变量`value`不在TDZ 。这说明这里没有 value binding，typeof 简单返回 ”undefined“。

TDZ是block bindings的一个特别的地方，另一个特别的部分是在loops中应用它们。

###  {#leanpub-auto-block-binding-in-loops}



