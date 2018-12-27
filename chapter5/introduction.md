# Destructuring for Easier Data Access

ES6简化了从对象和数组中获取数据的方法。解构把一个数据结构拆分成更小的部分。

## Summary

解构让JS的对象和数组更容易使用。用类似对象字面量和数组字面量语法，你可以把数据结构拆分，从而精准获取你要的信息。

对象和数组解构都可以设置默认值。

赋值运算右侧是`null`或`undefined`都会报错。

深度嵌套也一样可用，descending to any arbitrary depth。

*解构声明*用var、let、const来创建变量，并且 must always have a initializer。

*解构赋值*可以用来替换其他的赋值方式，允许解构到对象属性及已经存在的变量中。

*解构参数*使用解构语法让函数参数中的"options"对象更加透明，你可以在解构参数中把需要的参数挨个排列出来。解构参数可用是数组模式、对象模式、或者混合模式，你可以在这里使用全部的解构的特性。