## Arrow Functions

箭头函数和传统JS函数在行为上有一些重要的不同：

* **没有 this，super，arguments，new.target bindings**
  * this，super，arguments，new.target 的值是由最近的包裹箭头函数的 noarrow function 决定的。\(`super`is covered in Chapter 4.\)
* **不能使用new调用**
  * 箭头函数没有`[[Construct]]`方法
* **没有原型 No prototype**
  * 不能使用new，因此不需要prototype
* **不能改变this**
  * 函数内的this值不能被改变，在整个函数生命周期中保持一样。It remains the same throughout the entire lifecycle of the function.
* **没有arguments对象**
  * 箭头函数没有arguments binding，因此需要依赖 named parameters 和 rest parameters 来获取函数参数。
* 不允许重复名称的参数 **No duplicate named parameters**
  * strict or nostrict mode，noarrow gunction 只有在严格模式才不能用重复名字的参数

> 减少错误和歧义。First and foremost, `this`binding is a common source of error in JavaScript.
>
> 优化性能。Second，通过限制this的值为唯一的，JS引擎可以更加容易地**优化函数执行**。普通函数可能被用作 constructor，或者被修改。



