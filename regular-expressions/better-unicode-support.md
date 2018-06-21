## Better Unicode Support

> _**code unit**_
>
> 在ECMAScript 6之前，JavaScript strings 使用 16-bit character encoding \(UTF-16\)。每一个 16-bit sequence 是一个 code unit，代表了一个 character。所有的string属性和方法，比如 `length` 属性，`charAt()` 方法，都是基于 16-bit code unit。

16-bit 过去是足够包括所有 character 的。但是由于 Unicode 带来了一个 扩展的字符集合，that’s no longer true。

### UTF-16 Code Points

> _**code points**_
>
> Unicode 希望能给世界上的每一个字符提供一个 globally unique identifier，限制 character 的长度为 16 bits 是无法实现这个愿望的。这些 globally unique identifiers，被称作 _code points，_是从 0 开始的简单数字。_code points _可以被认为是字符编码 character codes，既一个 number 代表 一个 character。character 的编码需要把 code points 编码成一致的 code units。对于 UTF-16, code points 可能是由多个 code units组成的。
>
> _**Basic Multilingual Plane \(BMP\)**_
>
> UTF-16中，最初的 2[^16] 个 code points 是 single 16-bit code units。这个范围叫做 _Basic Multilingual Plane \(BMP\)。_
>
> _**surrogate pairs**_
>
> 所有不在这个范围内的被认为是在一个 _supplementary planes _中，code points 不能被表示为 16-bits。UTF-16 通过引入 _surrogate pairs _来解决这个问题，即 一个 code point 表示为 两个 16-bits 的 code units。
>
> 这就意味着，string中的任何一个单个的 character，既有可能是一个 code unit（16 bits）for BMP character，也有可能是两个 code units（32 bits）for supplementary plane characters。

ECMAScript 5 中，所有的string操作都是工作在 16-bit code units 上的，当UTF-16编码字符串包括 surrogate pairs 时，可能会得到不符合预期的结果。

```js
var text = "𠮷";

console.log(text.length);           // 2
console.log(/^.$/.test(text));      // false
console.log(text.charAt(0));        // ""
console.log(text.charAt(1));        // ""
console.log(text.charCodeAt(0));    // 55362
console.log(text.charCodeAt(1));    // 57271
```

### The codePointAt\(\) Method

`codePointAt()`method

### The String.fromCodePoint\(\) Method

### The normalize\(\) Method

### The Regular Expression u Flag

ote here.[^16]

