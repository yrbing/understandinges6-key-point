## Object Destructuring

对象解构，在赋值操作符的左边使用对象字面量语法。

```js
let node = {
        type: "Identifier",
        name: "foo"
    };

let { type, name } = node;

console.log(type);      // "Identifier"
console.log(name);      // "foo"
```

这里的语法和对象字面量属性初始化的简写语法一样，标识符`type`和`name`既是local variables的声明，也是读取的`node`对象的属性。

---
Don’t Forget the Initializer

用解构来声明变量，必须进行初始化。

```js
// syntax error!
var { type, name };

// syntax error!
let { type, name };

// syntax error!
const { type, name };
```

在这里需要关注的是，`const`总是需要初始化的，`let`和`var`只有在用解构声明时需要同时初始化。

---

### Destructuring Assignment

在赋值时使用解构。

```js
let node = {
        type: "Identifier",
        name: "foo"
    },
    type = "Literal",
    name = 5;

// assign different values using destructuring
({ type, name } = node);

console.log(type);      // "Identifier"
console.log(name);      // "foo"
```

** 必须使用括号，否则报错。Unexpected token `=` **

因为 an opening curly brace 总是预示着一个 black statement，而一个 block statement 不能出现在赋值操作的左边。parentheses预示着接下来的curly brace不是一个 block statement，而应该被解析为一个表达式expression。

解构赋值运行结果的值是表达式的右边部分，即`=`后面的部分。因此可以在任何需要一个value的地方使用解构赋值。比如给函数传入参数。

```js
let node = {
        type: "Identifier",
        name: "foo"
    },
    type = "Literal",
    name = 5;

function outputInfo(value) {
    console.log(value === node);        // true
}

outputInfo({ type, name } = node);

console.log(type);      // "Identifier"
console.log(name);      // "foo"
```

The `outputInfo()` function is called with a destructuring assignment expression. 
这个expression的值是`node`，即赋值运算符右边的值。`type` and `name`被正常赋值，同时`node`作为参数传入函数`outputInfo()`.

> 如果`=`右边执行的值是`null`或者`undefined`，结构赋值表达式会报错。因为获取`null`或者`undefined`的属性会导致 runtime error。

### Default Values

解构赋值语句中，如果指定的本地变量名，在object上没有对应的属性名，这个local variable会被赋值undefined。

```js
let node = {
        type: "Identifier",
        name: "foo"
    };

let { type, name, value } = node;

console.log(type);      // "Identifier"
console.log(name);      // "foo"
console.log(value);     // undefined
```

可以定义一个default value，当对应的属性不存在或者值是`undefined`时，会使用默认值。

```js
let node = {
        type: "Identifier",
        name: "foo"
    };

let { type, name, value = true } = node;

console.log(type);      // "Identifier"
console.log(name);      // "foo"
console.log(value);     // true
```

### Assigning to Different Local Variable Names

有没有可能不使用对象的属性名作为对应的local变量名？ES6提供了扩展语法，你可以用不同的local变量名，这语法看上去就像是非简写的对象字面量初始化语法。

```js
let node = {
        type: "Identifier",
        name: "foo"
    };

let { type: localType, name: localName } = node;

console.log(localType);     // "Identifier"
console.log(localName);     // "foo"
```

你还可以在这个基础上再加入default value。

```js
let node = {
        type: "Identifier"
    };

let { type: localType, name: localName = "bar" } = node;

console.log(localType);     // "Identifier"
console.log(localName);     // "bar"
```

以上的对象解构，对象属性都是原始值，对象解构也可以处理嵌套对象结构。

### Nested Object Destructuring

类似对象字面量的语法，进入嵌套对象结构的内部，仅仅获取需要的信息。

```js
let node = {
        type: "Identifier",
        name: "foo",
        loc: {
            start: {
                line: 1,
                column: 1
            },
            end: {
                line: 1,
                column: 4
            }
        }
    };

let { loc: { start }} = node;

console.log(start.line);        // 1
console.log(start.column);      // 1
```

在上一节中，解构中的冒号意味着，冒号colon前面的标识符indentifier是要去查询的位置，冒号右边是要去赋值的对象。当冒号右边是一个花括号时，说明目标嵌套在当前对象中。
* 因此这里并没有声明一个loc变量 *

在这里也可以使用和属性不同的名字：

```js
let node = {
        type: "Identifier",
        name: "foo",
        loc: {
            start: {
                line: 1,
                column: 1
            },
            end: {
                line: 1,
                column: 4
            }
        }
    };

// extract node.loc.start
let { loc: { start: localStart }} = node;

console.log(localStart.line);   // 1
console.log(localStart.column); // 1
```

解构模式可以嵌套到任意深度级别，每个级别都可以使用所有的能力。

---

Syntax Gotcha

Be careful when using nested destructuring because you can inadvertently create a statement that has no effect. Empty curly braces are legal in object destructuring, however, they don’t do anything. For example:

```js
// no variables declared!
let { loc: {} } = node;
```

There are no bindings declared in this statement. Due to the curly braces on the right, loc is used as a location to inspect rather than a binding to create. In such a case, it’s likely that the intent was to use = to define a default value rather than : to define a location. It’s possible that this syntax will be made illegal in the future, but for now, this is a gotcha to look out for.

