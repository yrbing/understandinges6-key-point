## Arrow Functions

箭头函数和传统JS函数在行为上有一些重要的不同：

* **没有 this，super，arguments，new.target bindings**
  * this，super，arguments，new.target 的值是由最近的包裹箭头函数的 noarrow function 决定的。\(`super`is covered in Chapter 4.\)
* **不能使用new调用**
  * 箭头函数没有`[[Construct]]`方法
* **没有原型 No prototype**



