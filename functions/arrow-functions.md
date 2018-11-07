## Arrow Functions

箭头函数和传统JS函数在行为上有一些重要的不同：

* 没有 this，super，arguments，new.target bindings
  * 这些变量的值是由最近的包裹箭头函数的noarrow function 决定的。

**No`this`,`super`,`arguments`, and`new.target`bindings**

* The value of`this`,`super`,`arguments`, and`new.target`inside of the function is by the closest containing nonarrow function. \(`super`is covered in Chapter 4.\)
* 


**Cannot be called with**

**`new`**

- Arrow functions do not have a

`[[Construct]]`

method and therefore cannot be used as constructors. Arrow functions throw an error when used with

`new`

.

* **No prototype**
  - since you can’t use
  `new`
  on an arrow function, there’s no need for a prototype. The
  `prototype`
  property of an arrow function doesn’t exist.
* **Can’t change**
  **`this`**
  - The value of
  `this`
  inside of the function can’t be changed. It remains the same throughout the entire lifecycle of the function.
* **No**
  **`arguments`**
  **object**
  - Since arrow functions have no
  `arguments`
  binding, you must rely on named and rest parameters to access function arguments.
* **No duplicate named parameters**
  - arrow functions cannot have duplicate named parameters in strict or nonstrict mode, as opposed to nonarrow functions that cannot have duplicate named parameters only in strict mode.



