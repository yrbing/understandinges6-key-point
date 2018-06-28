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

#### The codePointAt\(\) Method

`codePointAt()`

```js
var text = "𠮷a";

console.log(text.charCodeAt(0));    // 55362
console.log(text.charCodeAt(1));    // 57271
console.log(text.charCodeAt(2));    // 97

console.log(text.codePointAt(0));   // 134071
console.log(text.codePointAt(1));   // 57271
console.log(text.codePointAt(2));   // 97
```

对于BMP characters，`codePointAt()`方法与 `charCodeAt()`返回同样的值。

对于 non-BMP characters 则不同。`codePointAt()`返回完整的 code point，尽管 code point 跨越多个 code units。

`codePointAt()`是最简单的区分一个 character 是由一个还是两个 code units 组成的方法。

```js
function is32Bit(c) {
    return c.codePointAt(0) > 0xFFFF;
}

console.log(is32Bit("𠮷"));         // true
console.log(is32Bit("a"));          // false
```

#### The String.fromCodePoint\(\) Method

```js
console.log(String.fromCodePoint(134071));  // "𠮷"
```

`String.fromCodePoint()`可以看做是 `String.fromCharCode()`方法的一个更加完整的版本。

对于BMP characters，返回同样的值。

对于 non-BMP characters 则不同。

#### The normalize\(\) Method

为了进行排序或者其他基于比较的操作 comparison-based operations，不同的characters可能会被认为是相等的 equivalent。

有两种方法来定义这种关系：

_canonical equivalence_

_compatibility_

ECMAScript 6 normalize\(\) 方法，可选参数：

* Normalization Form Canonical Composition \(`"NFC"`\), which is the default
* Normalization Form Canonical Decomposition \(`"NFD"`\)
* Normalization Form Compatibility Composition \(`"NFKC"`\)
* Normalization Form Compatibility Decomposition \(`"NFKD"`\)

### The Regular Expression u Flag

正则表达式也是基于16-bits code units。为了解决这个问题，ECMAScript 6 为 Unicode 定义了一个 `u` flag。

##### The u Flag in Action {#leanpub-auto-the-u-flag-in-action}

```js
var text = "𠮷";

console.log(text.length);           // 2
console.log(/^.$/.test(text));      // false
console.log(/^.$/u.test(text));     // true
```

##### Counting Code Points {#leanpub-auto-counting-code-points}

```js
function codePointLength(text) {
    var result = text.match(/[\s\S]/gu);
    return result ? result.length : 0;
}

console.log(codePointLength("abc"));    // 3
console.log(codePointLength("𠮷bc"));   // 3
```

> 尽管这个方法是可行的，但它并不是很快，尤其是应用长字符串行。你也可以使用 string iterator \(Chapter 8\)。
>
> 一般情况下，我们应该尽量减少counting code points。

##### Determining Support for the u Flag {#leanpub-auto-determining-support-for-the-u-flag}

  


