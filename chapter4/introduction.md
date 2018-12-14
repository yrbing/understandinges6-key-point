# Expanded Object Functionality

ES6对对象进行了简单的句法扩展，对象操作和交互上的提升。

## Summary

对象字面量的变化。简写的属性定义。计算属性名。简写的方法。接受重复的对象属性名。

`Object.assign()`方法。

`Object.is()`方法，`===`操作符的安全版本。

定义对象自有属性的枚举顺序。numeric keys always come first in ascending order followed by string keys in insertion order and symbol keys in insertion order.

`Object.setPrototypeOf()`方法让我们可以修改对象的原型了。

可以使用`super`关键字调用对象原型的方法。super调用的方法内部的`this`绑定，就是当前的`this`值。（我觉得就是定义super.func()方法时候的上下文）

