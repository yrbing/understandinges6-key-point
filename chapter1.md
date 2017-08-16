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

