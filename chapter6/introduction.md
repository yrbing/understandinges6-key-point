# Symbols and Symbol Properties

Symbols是ES6引入的原始类型（primitive type），Symbols加入了JS的原始类型大家庭。

已有的家庭成员有：strings, numbers, booleans, `null`, and `undefined`. 

Symbols最开始出现是因为希望能够创建private object members。在此之前，任何使用字符串名字的属性都可以很容易获取到，不管这个名字写的多么晦涩难懂。“private names”特性的意思是，能够让开发者创建 non-string 属性名。

这个private name的提议最终发展成了ES6的symbols。虽然实现细节是一致的（属性名增加 non-string 值），但最初关于privacy的目的被丢弃了。Instead, symbol properties are categorized separately from other object properties.

## Summary