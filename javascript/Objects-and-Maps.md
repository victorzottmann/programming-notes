# Objects and Maps

### Object property shorthand

A neat trick ES6 allows us to use is to write properties in objects with its shorthand method. For example:

```js
// If you define a set of variables outside of an object, and whose names are the same as the names of the keys you specify inside the object, then you can just write it like this:

const red = "#f00"
const green = "#0f0"
const blue = "#00f"

const colors = { red, blue, green }

// Doing it this way saves the trouble of repeting the same name for both keys and values.
const colors = {
  red: red,
  green: green,
  blue: blue
}
```

---

### Primitive vs Object Types (Passed by Value vs Passed by Reference)

As opposed to primitive data types, objects in JavaScript are known to be "**passed by reference**" **instead of "passed by value**". For example, if we have two variables that hold the exact same numbers, when we compare their values we will get `true`.

```js
const num = 20
const anotherNum = 20
console.log(num === anotherNum) // => true
```

However, if we do the same thing with objects, we get `false`

```js
const obj = {}
const anotherObj = {}
console.log(obj === anotherObj) // => false
```

This is what the **"passed by reference"** idea comes up. JavaScript considers every object to hold a unique value, so whenever an object is assigned to a variable, what is actually being assigned to it is a **reference** to the object itself, **NOT a value**. 

To make this clearer, consider the following:

```js
const obj = {}
const anotherObj = obj
anotherObj.a = 1 
// => here we are creating a new key inside anotherObj and adding a value of 1.
```

In theory, only `anotherObj` should contain the key-value pair of `a: 1`, right? Not really. What happens when we assign `anotherObj` to `obj` is that we are actually assigning the **same reference** from `obj` to `anotherObj`. Consequently, updating the data of `anotherObj` will automatically update `obj` as well.

---

### Object Destructuring

Destructing is a way to store object data into variables. This makes it easier to access nested data instead of having to always use `dot notation` everywhere. It also helps us make the code DRY.

```js
// Take this user object for example:
const user = {
  name: "Victor",
  username: "v123",
  email: "victor@random.com",
  details: {
    jobTitle: "Developer",
    age: 28,
  }
}
// This function returns a string from the data that is passed in the return.
const displayUserData = () => {
  return `${user.name} is ${user.details.age} years old and is a ${user.details.jobTitle}.`
}
console.log(displayUserData()) // => Victor is 28 years old and is a Developer.


// Instead of using dot notation everywhere, we can destructure those keys into variables:
const { name, details: { jobTitle, age } } = user

// In this case, the keys that are inside the details key are the ones that are being destructured from details. This is also called 'nested destructuring'. And this is the result:
const displayUserData = () => {
  return `${name} is ${age} years old and is a ${jobTitle}.`
}
console.log(displayUserData()) // => Victor is 28 years old and is a Developer.
```















