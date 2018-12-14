## A Formal Method Definition

一个正式的“方法”定义。

在ES6之前，method的概念并没有一个正式的定义。method只是对象的属性，只不过包含的是functions而不是data。ES6正式定义了method，是一个有内部`[[HomeObject]]`属性的function，`[[HomeObject]]`包含的是method所属的那个object。

```js
let person = {

    // method
    getGreeting() {
        return "Hello";
    }
};

// not a method
function shareGreeting() {
    return "Hi!";
}
```

The `[[HomeObject]]` for `getGreeting()` is `person`。而shareGreeting()函数没有`[[HomeObject]]`。
当使用`super`references时，这个差别非常的重要。

任何对`super`的引用，都要使用`[[HomeObject]]`来确定做什么。第一步，在`[[HomeObject]]`上调用`Object.getPrototypeOf()`，取回 a reference to the prototype。第二步，在原型中寻找对应名字的函数。最后，确定`this`绑定，调用函数。

```js
let person = {
    getGreeting() {
        return "Hello";
    }
};

// prototype is person
let friend = {
    getGreeting() {
        return super.getGreeting() + ", hi!";
    }
};
Object.setPrototypeOf(friend, person);

console.log(friend.getGreeting());  // "Hello, hi!"
```

在本例中，`super.getGreeting()` is equivalent to `person.getGreeting.call(this)`。