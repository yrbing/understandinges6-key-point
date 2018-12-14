## More Powerful Prototypes

Prototype是JS中的inheritance的基础，ES6让prototype更加powerful。早期的JS版本严重限制了prototype的能力。

### Changing an Object's Prototype

一般情况下，当一个对象创建时，它的prototype就已经被指定了，无论是通过constructor或者`Object.create()`。ES5可以通过`Object.getPrototypeOf()`方法获取对象的prototype，但是不能在实例化之后改变对象的prototype。

ES6增加了`Object.setPrototypeOf()`方法。

```js
let person = {
    getGreeting() {
        return "Hello";
    }
};

let dog = {
    getGreeting() {
        return "Woof";
    }
};

// prototype is person
let friend = Object.create(person);
console.log(friend.getGreeting());                      // "Hello"
console.log(Object.getPrototypeOf(friend) === person);  // true

// set prototype to dog
Object.setPrototypeOf(friend, dog);
console.log(friend.getGreeting());                      // "Woof"
console.log(Object.getPrototypeOf(friend) === dog);     // true
```

**个人总结：`Object.setPrototypeOf()`只是改变对象的原型，因此会改变对象继承的方法，但不会改变对象的自有方法。**

```js
let person = {
    getGreeting() {
        return "Hello";
    }
};

let dog = {
    getGreeting() {
        return "Woof";
    }
};

Object.setPrototypeOf(dog, person)
console.log(Object.getPrototypeOf(dog) === person);  // true
console.log(dog.getGreeting());                      // "Woof"
```

对象原型的actual value存储在一个 internal-only 属性：`[[Protytype]]`。
`Object.getPrototypeOf()`方法返回存储在`[[Protytype]]`中的值，`Object.setPrototypeOf()`方法改变存储在`[[Protytype]]`中的值。

### Esay Prototype Access With Super References

ES6引入了 `super` references，可以更容易的获取一个对象原型。
比如，如果你想要override一个对象实例的方法，让它也去调用同名的原型方法，示例如下：

```js
let person = {
    getGreeting() {
        return "Hello";
    }
};

let dog = {
    getGreeting() {
        return "Woof";
    }
};


let friend = {
    getGreeting() {
        return Object.getPrototypeOf(this).getGreeting.call(this) + ", hi!";
    }
};

// set prototype to person
Object.setPrototypeOf(friend, person);
console.log(friend.getGreeting());                      // "Hello, hi!"
console.log(Object.getPrototypeOf(friend) === person);  // true

// set prototype to dog
Object.setPrototypeOf(friend, dog);
console.log(friend.getGreeting());                      // "Woof, hi!"
console.log(Object.getPrototypeOf(friend) === dog);     // true
```

The additional `.call(this)` ensures that the this value inside the prototype method is set correctly.

ES6 引入了 `super`。简单来说，super是一个指向当前对象原型的指针。

```js
let friend = {
    getGreeting() {
        // in the previous example, this is the same as:
        // Object.getPrototypeOf(this).getGreeting.call(this)
        return super.getGreeting() + ", hi!";
    }
};
```
`super.getGreeting()`的调用在上下文中等同于`Object.getPrototypeOf(this).getGreeting.call(this)`。

**`super`只能使用在concise method中。尝试在普通写法声明的对象方法中使用`super`，会导致syntax error。**

```js
let friend = {
    getGreeting: function() {
        // syntax error
        return super.getGreeting() + ", hi!";
    }
};
```

当你有multiple levels的继承时，`super`引用非常强大，因为在这种情况下，`Object.getPrototypeOf()`可能会在有的情况下失效。

```js
let person = {
    getGreeting() {
        return "Hello";
    }
};

// prototype is person
let friend = {
    getGreeting() {
        return Object.getPrototypeOf(this).getGreeting.call(this) + ", hi!";
    }
};
Object.setPrototypeOf(friend, person);


// prototype is friend
let relative = Object.create(friend);

console.log(person.getGreeting());                  // "Hello"
console.log(friend.getGreeting());                  // "Hello, hi!"
console.log(relative.getGreeting());                // error!
```

`relative.getGreeting()`会导致递归的调用，直到stack overflow error occurs。
Uncaught RangeError: Maximum call stack size exceeded

在ES5中这个问题很难解决，但有了ES6的`super`，就很容易：

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


// prototype is friend
let relative = Object.create(friend);

console.log(person.getGreeting());                  // "Hello"
console.log(friend.getGreeting());                  // "Hello, hi!"
console.log(relative.getGreeting());                // "Hello, hi!"
```

因为`super`不是动态的，它总是指向正确的对象。
