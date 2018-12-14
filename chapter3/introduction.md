# Functions

函数是任何编程语言的一个重要部分。在ES6之前，JS函数自这门语言创建之后就没有太多变化了。因此不仅积压了很多问题，也导致出错很容易，并且需要更多代码来完成一些基本功能。

ES6函数向前跳跃了一大步。在ES5的基础上做出了很多提升，让JS编程更少出错，并且更加powerful。

## Summary

ES6不是在增加功能，而是想办法让功能更加好用。

Functions haven’t undergone a huge change in ECMAScript 6, but rather, a series of incremental changes that make them easier to work with.

Default function parameters allow you to easily specify what value to use when a particular argument isn’t passed. Prior to ECMAScript 6, this would require some extra code inside the function, to both check for the presence of arguments and assign a different value.

Rest parameters allow you to specify an array into which all remaining parameters should be placed. Using a real array and letting you indicate which parameters to include makes rest parameters a much more flexible solution than`arguments`.

The spread operator is a companion to rest parameters, allowing you to deconstruct an array into separate parameters when calling a function. Prior to ECMAScript 6, there were only two ways to pass individual parameters contained in an array: by manually specifying each parameter or using`apply()`. With the spread operator, you can easily pass an array to any function without worrying about the`this`binding of the function.

The addition of the`name`property should help you more easily identify functions for debugging and evaluation purposes. Additionally, ECMAScript 6 formally defines the behavior of block-level functions so they are no longer a syntax error in strict mode.

In ECMAScript 6, the behavior of a function is defined by`[[Call]]`, normal function execution, and`[[Construct]]`, when a function is called with`new`. The`new.target`metaproperty also allows you to determine if a function was called using`new`or not.

The biggest change to functions in ECMAScript 6 was the addition of arrow functions. Arrow functions are designed to be used in place of anonymous function expressions. Arrow functions have a more concise syntax, lexical`this`binding, and no`arguments`object. Additionally, arrow functions can’t change their`this`binding, and so can’t be used as constructors.

Tail call optimization allows some function calls to be optimized in order to keep a smaller call stack, use less memory, and prevent stack overflow errors. This optimization is applied by the engine automatically when it is safe to do so, however, you may decide to rewrite recursive functions in order to take advantage of this optimization.

