## Other Regular Expression Changes

配合string的一些更新，ECMAScript 6 对正则表达式做了一些improvements。

### The Regular Expression y Flag

Firefox将 y flag 作为正则表达式的扩展进行了实现，本次 ECMAScript 6 标准化了 `y` flag。

`y`flag 影响了正则表达式搜索的 sticky 属性，它规定了search要从正则表达式的 lastIndex 属性开始匹配。如果在指定位置没有匹配，正则表达式会停止继续匹配。

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

然后lastIndex属性被赋值1，因此正则表达式应该从第二个字符开始匹配。没有flags的正则表达式无视了lastIndex的变化。g flag 匹配了"hello2 "。第三个sticky regular expression从第二个字符开始匹配，没有匹配到任何东西。

sticky flag 保存了最后一个匹配之后的下一个字符的index值。如果一个操作的结果是no match，lastIndex被重置为0.

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

### Duplicating Regular Expressions

### The`flags`Property



