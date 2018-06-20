## Better Unicode Support

_code unit_

在ECMAScript 6之前，JavaScript strings 使用 16-bit character encoding \(UTF-16\)。每一个 16-bit sequence 是一个 code unit，代表了一个 character。所有的string属性和方法，比如 `length` 属性，`charAt()` 方法，都是基于 16-bit code unit。

16-bit 过去是足够包括所有 character 的。但是由于 Unicode 带来了一个 扩展的字符集合，that’s no longer true。

### UTF-16 Code Points

_code points_

Unicode 希望能给世界上的每一个字符提供一个 globally unique identifier，限制 character 的长度为 16 bits 是无法实现这个愿望的。这些 globally unique identifiers，被称作 _code points，_是从 0 开始的简单数字。

_code points_

,

_Basic Multilingual Plane \(BMP\)_

### The codePointAt\(\) Method

### The String.fromCodePoint\(\) Method

### The normalize\(\) Method

### The Regular Expression u Flag



