## Global Block Bindings

let， const 和 var 不同的另一个地方就是：在 global scope 中的行为。

var在global scope：创建一个全局变量 global variable，并且是全局对象 global object \( `window` in browsers\) 的一个属性。因此你可能会不小心覆盖了一个已经存在的全局变量。



