## Other Regular Expression Changes

配合string的一些更新，ECMAScript 6 对正则表达式做了一些improvements。

### The Regular Expression y Flag

Firefox将 `y` flag 作为正则表达式的扩展进行了实现，本次 ECMAScript 6 标准化了 `y` flag。

`y`flag 影响了正则表达式搜索的 sticky 属性，它规定了search要从正则表达式的 `lastIndex` 属性开始匹配。如果在指定位置没有匹配，正则表达式会停止继续匹配。

```js
var text = "hello1 hello2 hello3",
    pattern = /hello\d\s?/,
    result = pattern.exec(text),
    globalPattern = /hello\d\s?/g,
    globalResult = globalPattern.exec(text),
    stickyPattern = /hello\d\s?/y,
    stickyResult = stickyPattern.exec(text);

console.log(result[0]);         // "hello1 "
console.log(globalResult[0]);   // "hello1 "
console.log(stickyResult[0]);   // "hello1 "

pattern.lastIndex = 1;
globalPattern.lastIndex = 1;
stickyPattern.lastIndex = 1;

result = pattern.exec(text);
globalResult = globalPattern.exec(text);
stickyResult = stickyPattern.exec(text);

console.log(result[0]);         // "hello1 "
console.log(globalResult[0]);   // "hello2 "
console.log(stickyResult[0]);   // Error! stickyResult is null
```

第一次调用`console.log()`时，三个正则表达式均输出`“hello1 ”`，以空格结尾。

然后`lastIndex`属性被赋值1，因此正则表达式应该从第二个字符开始匹配。没有flags的正则表达式无视了`lastIndex`的变化。g flag 匹配了"hello2 "。第三个sticky regular expression从第二个字符开始匹配，没有匹配到任何东西。

sticky flag 保存了最后一个匹配之后的下一个字符的index值。如果一个操作的结果是no match，lastIndex被重置为0。global flag也是如此。

```js
var text = "hello1 hello2 hello3",
    pattern = /hello\d\s?/,
    result = pattern.exec(text),
    globalPattern = /hello\d\s?/g,
    globalResult = globalPattern.exec(text),
    stickyPattern = /hello\d\s?/y,
    stickyResult = stickyPattern.exec(text);

console.log(result[0]);         // "hello1 "
console.log(globalResult[0]);   // "hello1 "
console.log(stickyResult[0]);   // "hello1 "

console.log(pattern.lastIndex);         // 0
console.log(globalPattern.lastIndex);   // 7
console.log(stickyPattern.lastIndex);   // 7

result = pattern.exec(text);
globalResult = globalPattern.exec(text);
stickyResult = stickyPattern.exec(text);

console.log(result[0]);         // "hello1 "
console.log(globalResult[0]);   // "hello2 "
console.log(stickyResult[0]);   // "hello2 "

console.log(pattern.lastIndex);         // 0
console.log(globalPattern.lastIndex);   // 14
console.log(stickyPattern.lastIndex);   // 14
```

the sticky flag 还有两个小细节需要注意：

1. `lastIndex`属性只有在调用属于正则表达式对象的方法时，才是生效的。比如`exec()`和`test()`方法。在string的方法里传入正则表达式不会有sticky的效果，比如`match()`方法。
2. 如果使用`^`字符去匹配字符串的起始位置，sticky 正则表达式基本上没有什么意义，只从string的开头进行匹配（或者start of the line in multiline mode）。当`lastIndex`为0，`^`字符使得sticky正则表达式和non-sticky正则表达式没有什么区别。当`lastIndex`不指向单行模式下的string的开头，或者多行模式下的一行的开头时，sticky正则表达式wil never match。

### Duplicating Regular Expressions

### The`flags`Property



