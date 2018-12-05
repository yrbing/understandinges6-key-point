## Summary

let 和 const 在 JavaScript 中引入了词法作用域 lexical scoping。变量可以在需要使用的地方声明，但副作用就是，你不能在声明之前访问这个变量（TDZ），即使使用安全的运算符比如 typeof。

大多数情况下，let 以及 const 和 var 的行为是很相似的，除了loops。对于 let 和 const二者，for-in 和 for-of 在循环的每一个迭代都创建新的 binding。对于let 在 for 循环中的表现也是一样的。但在 for循环中应用 const 可能会导致抛出错误。

目前 block bindings 的最好实践是默认使用 const，只在变量值需要变化的时候使用 let。这就确保了一个基本的不可变性 a basic level of **immutability** in code，可以避免特定类型的错误。

