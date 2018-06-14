## Emerging Best Practices for Block Bindings

默认使用 const，只有在你知道变量的值需要变化时，再使用 let。

根本依据是：

The rationale is that most variables should not change their value after initialization because unexpected value changes are a source of bugs.

