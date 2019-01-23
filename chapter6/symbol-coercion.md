## Symbol Coercion

类型强制转换(type coercion)是JavaScript语言重要的一部分, 强制转换数据类型使得语言有很大的灵活性。Symbols, however, are quite inflexible when it comes to coercion because other types lack a logical equivalent to a symbol. 

Specifically, symbols cannot be coerced into strings or numbers so that they cannot accidentally be used as properties that would otherwise be expected to behave as symbols.

本章中使用`console.log()`来指示symbols的output，这样做之所以有效是因为`console.log()`在symbols上调用了`String()`方法。你也可以直接使用`String()`方法得到相同的结果。

```js
let uid = Symbol.for("uid"),
    desc = String(uid);

console.log(desc);              // "Symbol(uid)"
```

`String()`方法调用`uid.toString()`，返回了symbol的string description。如果你想要concatenate the symbol directly with a string, 抱歉，是不行的，报错：

```js
let uid = Symbol.for("uid"),
    desc = uid + "";            // error!
```

Concatenating `uid` with an empty string requires that `uid` first be coerced into a string. An error is thrown when the coercion is detected, preventing its use in this manner.

同样，你也不能将symbol强制转换为number。所有的数学运算符在应用于symbol时，都会导致错误。

```js
let uid = Symbol.for("uid"),
    sum = uid / 1;            // error!
```

此示例尝试将symbol除以1，这会导致错误。无论使用何种数学运算符，都会抛出错误。

逻辑运算符不会抛出错误，因为所有symbol都被认为等同于`true`，就像JavaScript中的任何其他非空值(non-empty value)一样。