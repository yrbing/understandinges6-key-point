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
When you use a destructuring assignment statement, if you specify a local variable with a property name that doesn’t exist on the object, then that local variable is assigned a value of undefined. For example:

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

This code defines an additional local variable called value and attempts to assign it a value. However, there is no corresponding value property on the node object, so the variable is assigned the value of undefined as expected.

You can optionally define a default value to use when a specified property doesn’t exist. To do so, insert an equals sign (=) after the property name and specify the default value, like this:

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

In this example, the variable value is given true as a default value. The default value is only used if the property is missing on node or has a value of undefined. Since there is no node.value property, the variable value uses the default value. This works similarly to the default parameter values for functions, as discussed in Chapter 3.

### Assigning to Different Local Variable Names

Up to this point, each example destructuring assignment has used the object property name as the local variable name; for example, the value of node.type was stored in a type variable. That works well when you want to use the same name, but what if you don’t? ECMAScript 6 has an extended syntax that allows you to assign to a local variable with a different name, and that syntax looks like the object literal nonshorthand property initializer syntax. Here’s an example:

```js
let node = {
        type: "Identifier",
        name: "foo"
    };

let { type: localType, name: localName } = node;

console.log(localType);     // "Identifier"
console.log(localName);     // "foo"
```

This code uses destructuring assignment to declare the localType and localName variables, which contain the values from the node.type and node.name properties, respectively. The syntax type: localType says to read the property named type and store its value in the localType variable. This syntax is effectively the opposite of traditional object literal syntax, where the name is on the left of the colon and the value is on the right. In this case, the name is on the right of the colon and the location of the value to read is on the left.

You can add default values when using a different variable name, as well. The equals sign and default value are still placed after the local variable name. For example:

```js
let node = {
        type: "Identifier"
    };

let { type: localType, name: localName = "bar" } = node;

console.log(localType);     // "Identifier"
console.log(localName);     // "bar"
```

Here, the localName variable has a default value of "bar". The variable is assigned its default value because there’s no node.name property.

So far, you’ve seen how to deal with destructuring of an object whose properties are primitive values. Object destructuring can also be used to retrieve values in nested object structures.

### Nested Object Destructuring
By using a syntax similar to object literals, you can navigate into a nested object structure to retrieve just the information you want. Here’s an example:

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

The destructuring pattern in this example uses curly braces to indicate that the pattern should descend into the property named loc on node and look for the start property. Remember from the last section that whenever there’s a colon in a destructuring pattern, it means the identifier before the colon is giving a location to inspect, and the right side assigns a value. When there’s a curly brace after the colon, that indicates that the destination is nested another level into the object.

You can go one step further and use a different name for the local variable as well:

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

In this version of the code, `node.loc.start` is stored in a new local variable called `localStart`. Destructuring patterns can be nested to an arbitrary level of depth, with all capabilities available at each level.

Object destructuring is very powerful and has a lot of options, but array destructuring offers some unique capabilities that allow you to extract information from arrays.

Syntax Gotcha
Be careful when using nested destructuring because you can inadvertently create a statement that has no effect. Empty curly braces are legal in object destructuring, however, they don’t do anything. For example:

```js
// no variables declared!
let { loc: {} } = node;
```

There are no bindings declared in this statement. Due to the curly braces on the right, loc is used as a location to inspect rather than a binding to create. In such a case, it’s likely that the intent was to use = to define a default value rather than : to define a location. It’s possible that this syntax will be made illegal in the future, but for now, this is a gotcha to look out for.

