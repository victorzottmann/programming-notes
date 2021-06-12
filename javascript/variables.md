# Variables

### Global Object

If a *variable* is assigned to a value without either the `var`, or the `let` and `const` keywords, it won't throw an error, but instead will be assigned to the `Global Object`. It is referred to as `window` in the browser, and as `global` in the server. 

```js
message = "hello world" // message belongs to the Global Object in this case
```

In 2020 ECMA released a feature that uses `globalThis` to reference the Global Object both in the client- and server-side environements. In order to view the `message` global object, both the following methods make it possible. Remeber that in this case `message` is NOT a variable, but a **property of the global object**.

```js
console.log(window.message) // => hello world
console.log(message)        // => hello world
```

---

### Scripting Modes & Hoisting

JavaScript contains two scripting modes: **Sloppy mode (normal)** and **Strict mode**, which throws more errors and prevents mistakes from happening. For example, by using `strict mode`, JavaScript would throw and error when `message` was defined without a preceding keyword.

```js
"use strict"

message = "hello world" 
// => ReferenceError: message is not defined
```

** One thing to keep in mind about `strict mode` is that although it fixes some problems with variables declared with the `var` keyword, it misses out on some other areas, such as `hoisting`.  Hoisting allows you to access a variable before it is declared:

```js
"use strict"

console.log(age) // => null
var age = 28
// => it doesn't throw an error because of hoisting; rather, it returns null by default.
```

This issue with hoisting can be avoided by declaring variables with either `let` or `const`.

