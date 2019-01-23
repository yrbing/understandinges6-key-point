## Using Symbols

可以在任何使用计算属性名(computed property name)的地方使用symbols，比如计算对象字面量属性名(computed object literal property names)，也可以在`Object.defineProperty()`以及`Object.defineProperties()`调用中使用。

```js
let firstName = Symbol("first name");

// use a computed object literal property
let person = {
    [firstName]: "Nicholas"
};

// make the property read only
Object.defineProperty(person, firstName, { writable: false });

let lastName = Symbol("last name");

Object.defineProperties(person, {
    [lastName]: {
        value: "Zakas",
        writable: false
    }
});

console.log(person[firstName]);     // "Nicholas"
console.log(person[lastName]);      // "Zakas"
```

既然你可以在任何可以使用computed property names的地方使用symbols，那么你可能就需要一个symbol的共享系统，从而在不同的代码段里有效地使用它们。