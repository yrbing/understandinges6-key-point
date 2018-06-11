## Block-Level Declarations

Block scopes, also called lexical scopes（词法作用域）：

1. 在function内部
2. 在一个block内部（被“{”和“}”包含）

### Let Declarations

1. 块级作用域
2. no declaration hoisting 不会声明提升
3. no redeclaration 不能重复声明

#### No Redeclaration {#leanpub-auto-no-redeclaration}

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

every `const`variable must be initialized on declaration

```js
// Syntax error: missing initialization
const name;
```

##### Constants vs Let Declarations {#leanpub-auto-constants-vs-let-declarations}

Constants, like `let`declarations, are block-level declarations.

In another similarity to`let`, a`const`declaration throws an error when made with an identifier for an already-defined variable in the same scope. It doesn’t matter if that variable was declared using`var`\(for global or function scope\) or`let`\(for block scope\). For example, consider this code:

```js
var message = "Hello!";
let age = 25;

// Each of these would throw an error.
const message = "Goodbye!";
const age = 30;
```

##### Declaring Objects with Const {#leanpub-auto-declaring-objects-with-const}

```javascript
const maxItems = 5;
maxItems = 6; // throws error
```

Much like constants in other languages, the`maxItems`variable can’t be assigned a new value later on.However, unlike constants in other languages, the value a constant holds may be modified if it is an object.

A`const`declaration prevents modification of the binding and not of the value itself. That means`const`declarations for objects do not prevent modification of those objects. For example:

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

`const` 阻止对binding的修改，但并不阻止对bound balue的修改。

#### The Temporal Dead Zone \(TDZ\) {#leanpub-auto-the-temporal-dead-zone}

使用`let`或`const`声明的变量 cannot be accessed until after the declaration.

```javascript
if (condition) {
    console.log(typeof value);  // ReferenceError!
    let value = "blue";
}
```

When a JavaScript engine looks through an upcoming block and finds a variable declaration, it either hoists the declaration to the top of the function or global scope \(for`var`\) or places the declaration in the TDZ \(for`let`and`const`\). Any attempt to access a variable in the TDZ results in a runtime error. That variable is only removed from the TDZ, and therefore safe to use, once execution flows to the variable declaration.

即使是使用 `typeof` 这个一般情况下比较safe的运算符时也是如此。但是，如果你是在变量声明的block外面：

```javascript
console.log(typeof value);  // "undefined"
if (condition) {
    let value = "blue";
}
```

`typeof`运算符执行时，变量`value`不在TDZ 。because it occurs outside of the block in which`value`is declared. That means there is no`value`binding, and`typeof`simply returns`"undefined"`.

###  {#leanpub-auto-block-binding-in-loops}



