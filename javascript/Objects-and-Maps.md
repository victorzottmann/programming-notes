# Objects and Maps

### Object property shorthand

A neat trick ES6 allows us to use is to write properties in objects with its shorthand method. For example:

```js
// If you define a set of variables outside of an object, and whose names are the same as the names of the keys you specify inside the object, then you can just write it like this:

const red = "#ff0000"
const blue = "#00ff00"
const green = "#0000ff"

const colors = { red, blue, green }

// Doing it this way saves the trouble of repeting the same name for both keys and values.
const colors = {
  red: red,
  blue: blue,
  green, green
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

