# Block Bindings

#### Let Declarations {#leanpub-auto-let-declarations}

除了是块级作用域之外，也不会 declaration hoisting。或者就是因为hoisting才导致var不是块级作用域

#### No Redeclaration {#leanpub-auto-no-redeclaration}

If an identifier has already been defined in a scope, then using the identifier in a`let`declaration inside that scope causes an error to be thrown. For example:

`var count = 30;`

`// Syntax error`

`let count = 40;`

---

`var count = 30;`

`// Does not throw an error`

`if(condition) {`

`let count = 40;`

`// more code`

`}`

#### Constant Declarations {#leanpub-auto-constant-declarations}

every `const`variable must be initialized on declaration

`// Syntax error: missing initialization`

`const name;`

##### Constants vs Let Declarations {#leanpub-auto-constants-vs-let-declarations}

Constants, like `let`declarations, are block-level declarations.

In another similarity to`let`, a`const`declaration throws an error when made with an identifier for an already-defined variable in the same scope. It doesn’t matter if that variable was declared using`var`\(for global or function scope\) or`let`\(for block scope\). For example, consider this code:

`var message = "Hello!";`

`let age = 25;`

`// Each of these would throw an error.`

`const message = "Goodbye!";`

`const age = 30;`

##### Declaring Objects with Const {#leanpub-auto-declaring-objects-with-const}

`const maxItems = 5;`

`maxItems = 6; // throws error`

Much like constants in other languages, the`maxItems`variable can’t be assigned a new value later on.However, unlike constants in other languages, the value a constant holds may be modified if it is an object.

A`const`declaration prevents modification of the binding and not of the value itself. That means`const`declarations for objects do not prevent modification of those objects. For example:

`const person = {`

`name: "Nicholas"`

`};`

`// work`

`person.name = "Greg";`

`// throws an error`

`person = {`

`name:"Greg"`

`};`

`const` 阻止对binding的修改，但并不阻止对bound balue的修改。

#### The Temporal Dead Zone \(TDZ\) {#leanpub-auto-the-temporal-dead-zone}

使用`let`或`const`声明的变量 cannot be accessed until after the declaration.

`if (condition) {`

`console.log(typeof value);  // ReferenceError!`

`let value = "blue";`

`}`

When a JavaScript engine looks through an upcoming block and finds a variable declaration, it either hoists the declaration to the top of the function or global scope \(for`var`\) or places the declaration in the TDZ \(for`let`and`const`\). Any attempt to access a variable in the TDZ results in a runtime error. That variable is only removed from the TDZ, and therefore safe to use, once execution flows to the variable declaration.

即使是使用 `typeof` 这个一般情况下比较safe的运算符时也是如此。但是，如果你是在变量声明的block外面：

