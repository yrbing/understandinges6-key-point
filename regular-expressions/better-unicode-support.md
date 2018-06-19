## Better Unicode Support

### UTF-16 Code Points

_code unit_

在ECMAScript 6之前，JavaScript strings 使用 16-bit character encoding \(UTF-16\)。每一个 16-bit sequence 是一个 code unit，代表了一个 character。所有的string属性和方法，比如 `length` 属性，`charAt()` 方法，都是基于 16-bit code unit。

16-bit 过去是足够包括所有 character 的。

### The codePointAt\(\) Method

_code points_

### The String.fromCodePoint\(\) Method

### The normalize\(\) Method

### The Regular Expression u Flag



