## Better Unicode Support

_code unit_

在ECMAScript 6之前，JavaScript strings 使用 16-bit character encoding \(UTF-16\)。每一个 16-bit sequence 是一个 code unit，代表了一个 character。所有的string属性和方法，比如 `length` 属性，`charAt()` 方法，都是基于 16-bit code unit。

16-bit 过去是足够包括所有 character 的。但是由于 Unicode 带来了一个 扩展的字符集合，that’s no longer true。

### UTF-16 Code Points

_code points_

Unicode 希望能给世界上的每一个字符提供一个 globally unique identifier，限制 character 的长度为 16 bits 是无法实现这个愿望的。这些 globally unique identifiers，被称作 _code points，_是从 0 开始的简单数字。_code points _可以被认为是字符编码 character codes，既一个 number 代表 一个 character。character 的编码需要把 code points 编码成一致的 code units。对于 UTF-16, code points 可能是由多个 code units组成的。

_Basic Multilingual Plane \(BMP\)_

UTF-16中，最初的 2[^16] 个 code points 是 single 16-bit code units。这个范围叫做 _Basic Multilingual Plane \(BMP\)。_

_surrogate pairs_

所有不在这个范围内的被认为是在一个 _supplementary planes _中，code points 不能被表示为 16-bits。UTF-16 通过引入 _surrogate pairs _来解决这个问题，即 一个 code point 表示为 两个 16-bits 的 code units。

### The codePointAt\(\) Method

### The String.fromCodePoint\(\) Method

### The normalize\(\) Method

### The Regular Expression u Flag

ote here.[^16]

