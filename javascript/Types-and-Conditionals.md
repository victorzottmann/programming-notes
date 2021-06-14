# Data Types and Conditionals

### Primitive data types:

- String
- Number
- Boolean
- Undefined
- Null
- Symbol

### Object data types: 

- Everything else

---

To check the data type of any variable (or anything, really) you can use the `typeof` operator. For example:

```js
let str = 'random string'

console.log(typeof str)    // => String
console.log(typeof 43)     // => Number
console.log(typeof window) // => Object
```

JavaScript has two type conversion methods: **Explicit** and **Implicit**. When values are converted into data types implicitly, this is known as **type coercion**. For example:

- Explicit conversion

```js
let weather = "raining"

console.log(String(27)) 
// => "27" => String() converts the value into a string.
console.log(Boolean(weather)) 
// => true => Boolean() converts the weather string into a boolean.
```

- Implicit conversion (type coercion)

```js
console.log('1' * '3') // => 3 => it assumes multiplication, so converts it to a number
console.log('1' + 3)   // => 13 => it assumes string concatenation, so converts it to a string.
```

---

### Falsy values and conditional statements:

```js
false
0
''
null
undefined
NaN
```

When checking whether something is `true` or `false` in an `if` statement, JavaScript will always implicitly convert the condition to `true`. For example:

```js
const username = '' // => here username is false because it's assigned to an empty string.

if (username === false) {
  console.log('no username')
}
// in this if statement, the program will not log the message because, under the hood, JavaScript will convert username to 'true'. this is what's happening behind the scenes:

if (Boolean(username)) {
  console.log('no username')
}
// remember that Boolean(username) converts whatever the value is into a Boolean value that is set to 'true' (a truthy value). So, in order for the program to run successfully, it should be written like this:

if(!username) {
  console.log('no user')
}
// here, the ! tell JavaScript to evaluate the parameter into a falsy value.
```

---

### Chaining ternary operations

Instead of having a clunky `if`statement, JavaScript allows you to chaining multiple conditions in a `ternary` operation. For example:

```js
// if-else statement
let temperature = 14
let answer

if (temperature < 0) {
  answer = "I can't feel my hands!"
} else if (temperature >= 0 && temperature <= 10) {
  answer = "It's very cold!"
} else if (temperature > 10 && temperature <= 15) {
  answer = "It's quite cool."
} else if (temperature > 15 && temperature < 25) {
  answer = "It's very nice today."
} else {
  answer = "I'm melting!"
}
console.log('if-else answer:', answer) // => It's quite cool.

// chained ternary
let temperature = -8
let answer = temperature < 0 ? 
      "I can't feel my hands!" 
			: temperature >= 0 && temperature <= 10 ? 
      "It's very cold!"
			: temperature > 10 && temperature <= 15 ?
			"It's quite cool."
			: temperature > 15 && temperature <= 25 ? "It's very nice today." : "I'm melting!"

console.log('ternary answer:', answer) // => I can't feel my hands!	 
```

---









