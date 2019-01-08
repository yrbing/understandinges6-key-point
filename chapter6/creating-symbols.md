## Creating Symbols

symbols和其他JS原始类型不同的一点是，symbols没有字面量形式(literal form)，比如布尔值的`true`或者数字的`42`。可以使用全局的`Symbol`函数来创建一个symbol：

```js
let firstName = Symbol();
let person = {};

person[firstName] = "Nicholas";
console.log(person[firstName]);     // "Nicholas"
```

这里创建了symbol`firstName`，并且将其作为`person`对象的一个属性。每次想要获取这个属性的时候都必需使用这个symbol。

> 由于symbols是primitive values, 调用`new Symbol()`会报错。You can create an instance of `Symbol` via `new Object(yourSymbol)` as well, but it’s unclear when this capability would be useful.

`Symbol`方法也可以接收一个可选的参数，作为这个symbol的说明(description)。这个描述本身并不能用来获取属性property，但可以用来debug。

```js
let firstName = Symbol("first name");
let person = {};

person[firstName] = "Nicholas";

console.log("first name" in person);        // false
console.log(person[firstName]);             // "Nicholas"
console.log(firstName);                     // "Symbol(first name)"
```

symbol的描述(description)存储在内部的[[Description]]属性中。当symbol的`toString()`方法被显式或隐含的调用时，会读取这个属性。没有其他的方法可以直接在代码中获取[[Description]]属性值。

建议总是为symbol提供一个description，to make both reading and debugging symbols easier.

---

### Identifying Symbols

因为symbols是原始值，可以使用`typeof`操作符判断一个变量是否是symbol。ECMAScript6扩展了`typeof`操作符，当用于symbol时，会返回`"symbol"`。

```js
let symbol = Symbol("test symbol");
console.log(typeof symbol);         // "symbol"
```

除非之外，也有其他一些不直接的方法来判断一个变量是否是symbol，`typeof`操作符是最为准确和推荐的。

---
