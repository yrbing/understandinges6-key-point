## Emerging Best Practices for Block Bindings

默认使用 const，只有在你知道变量的值需要变化时，再使用 let。

根本依据是：大多数变量在初始化之后不应该改变它们的值，因为不可预期的值的变化是bugs之源。unexpected value changes are a source of bugs.

