# Strings and Regular Expressions

Strings 是编程中非常重要的一个数据类型之一。

正则表达式给了开发者更多的能力去处理 Strings 。

## Summary

Full Unicode support allows JavaScript to deal with UTF-16 characters in logical ways. The ability to transfer between code point and character via`codePointAt()`and`String.fromCodePoint()`is an important step for string manipulation. The addition of the regular expression`u`flag makes it possible to operate on code points instead of 16-bit characters, and the`normalize()`method allows for more appropriate string comparisons.

ECMAScript 6 also added new methods for working with strings, allowing you to more easily identify a substring regardless of its position in the parent string. More functionality was added to regular expressions, too.

Template literals are an important addition to ECMAScript 6 that allows you to create domain-specific languages \(DSLs\) to make creating strings easier. The ability to embed variables directly into template literals means that developers have a safer tool than string concatenation for composing long strings with variables.

Built-in support for multiline strings also makes template literals a useful upgrade over normal JavaScript strings, which have never had this ability. Despite allowing newlines directly inside the template literal, you can still use`\n`and other character escape sequences.

Template tags are the most important part of this feature for creating DSLs. Tags are functions that receive the pieces of the template literal as arguments. You can then use that data to return an appropriate string value. The data provided includes literals, their raw equivalents, and any substitution values. These pieces of information can then be used to determine the correct output for the tag.

