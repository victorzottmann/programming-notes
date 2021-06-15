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

---

### Merging Objects and the Spread Operator

Suppose that we want to create a new user when they signup for our website. We could start by having a `user` object with empty values as a template. The empty values are useful in order to give the user the freedom not to have to submit the fields that aren't necessarily required.

```js
const user = {
  name: "",
  username: "",
  phoneNumber: "",
  email: "",
  password: ""
}
```

Then, when the user enter their details and submit, we can store them in a separate `newUser` object:

```js
const newUser = {
  username: "v123",
  email: "victor@random.com",
  password: "helloworld"
}
```

Once we have the data in `newUser`, how can we update that empty `user` object? We can use the `Object.assign()` method, which essentially allows you to update an object with properties from another object.

```js
Object.assign(user, newUser) // => this merges the second object with the first object.
```

But the problem here is that `Object.assign` will mutate the object that is passed into the first argument and, depending on the circumstance, this is not what we want at all. 

```js
// => the merge mutates the user object (not what we want)
const user = {
  name: "",
  username: "v123",
  phoneNumber: "",
  email: "victor@random.com",
  password: "helloworld"
}
```

To fix this, we can pass in an empty object as the first argument, which will host the resulting merge of `user` with `newUser`:

```js
Object.assign({}, user, newUser)
```

In case you want to include another property into the object created from `Object.assign()`, you can do this:

```js
Object.assign({}, user, newUser, { verified: false })
// alternatively, depending on the size of the object, it might be better to create it first, then pass it into the above.
```

##### The Object Spread Operator

Instead of using `Object.assign()`, we can use the spread operator `...` to merge properties of an object into another. The advantage of this is that it doesn't mutate the original object.

```js
const user = {
  name: "",
  username: "",
  phoneNumber: "",
  email: "",
  password: ""
}

const newUser = {
  username: "v123",
  email: "victor@random.com",
  password: "helloworld"
}

const createdUser = { ...user, ...newUser, verified: false }
console.log(createdUser)
/*
	{
		name: "",
  	username: "v123",
  	phoneNumber: "",
  	email: "victor@random.com",
  	password: "helloworld"
	}
*/
```

**Important:** one thing to note here is that the order in which you use the spread operator does matter. For example, because we passed the `user` object followed by the `newUser` object into `createdUser`, the properties from `user` will be updated by those of `newUser`. However, if `newUser` was passed as the first argument, the resulting object will consist of empty strings, because these are the values within `user`.

```js
const createdUser = { ...newUser, ...user, verified: false }
console.log(createdUser)
/*
	{
		name: "",
  	username: "",
  	phoneNumber: "",
  	email: "",
  	password: ""
	}
*/
```

---

### Maps

One key difference between objects and maps is that maps are ordered, meaning that when keys are added they are stored in sequence, whereas the keys in objects don't follow any order. Maps are also more flexible regarding the range of data types it can hold as keys.

```js
// To create a new map:
const myMap = new Map([
  [1, 1],
  [true, true]
])

// To add a new key-value pair:
myMap.set('hello', 'world')

console.log([...myMap.keys()]) // => [1, true, 'hello']

// Looping over a map:
myMap.forEach((value, key) => { // => it has to be in the inverse order
  console.log(key, value)
})
/*
	1, 1
	true, true,
	hello, 'world'
*/
```

Another very cool feature of maps is related to attaching sensitive data into the properties of an object, without exactly storing them in the object itself (e.g. mapping passwords related to their users). Doing this with objects alone isn't possible, so that's why maps are so useful.

```js
// Suppose we have two users and two passwords:

const user1 = { name: "john" }
const user2 = { name: "beth" }

const password1 = "fhdsfhkdjfh"
const password2 = "ivjibslabfn"

// Instead of storing each password within its related user object, we can create a map to attach each user with their corresponding password.

const passwordMap = new Map([
  [user1, password1], // we can use objects as keys
  [user2, password2]
])
// The problem with this approach is that it makes it hard to get the keys of the user objects. This approach is useful for when we need to access the values.

// To GET the password of the first user:
const pw = passwordMap.get(user1)
console.log(pw) // => ivjibslabfn

// It is better to use a variant of Map to access the values when we use objects as keys, called WeakMap.
const passwordMap = new WeakMap([
  [user1, password1],
  [user2, password2]
])

// To get the size of a map
const newMap = new Map([
  ["name", "john"],
  ["age", 32] 
])
console.log(newMap.size) // => 2
```

---

### Improving Methods with Arrow Functions

How to make the `this` keyword accessible from nested methods (and how to avoid returning `undefined`).

```js
const userData = {
  username: "victor",
  jobTitle: "Developer",
  getBio() {
    console.log(`User ${this.username} is  a ${this.jobTitle}`)
  }, // => in this case, the `this` keyword refers to the object itself (userData)
  askToFriend() {
    setTimeOut(function() {
      // it's gonna throw an error because the 'this' keyword not defined within the scope. 
			console.log(`Would you like to add ${this.username} to your friends list?`)
    }, 2000)
  }
}


const userData = {
  username: "victor",
  jobTitle: "Developer",
  getBio() {
    console.log(`User ${this.username} is  a ${this.jobTitle}`)
  }, 
  askToFriend() {
    setTimeOut(() => {
			console.log(`Would you like to add ${this.username} to your friends list?`)
    }, 2000)
  }
}
```

In order to fix the `this` keyword in the `askToFriend()` method, we need to change the function declaration in the `setTimeOut()` to an arrow function. The `this` keyword lies in the lexical scope when used within an arrow function, as opposed to a normal function declaration. In other words, the `this` keyword will be reference from the "parent" scope (outside the `askToFriend()` method).

However, it is important to note that if we were to set the `getBio` method as an arrow function, the `this` keyword will reference outer scope, which is essentially the global scope. In the global scope, `this` points to the `window` object, also known as the **Global Object**.

```js
const userData = {
  username: "victor",
  jobTitle: "Developer",
  getBio: () => {
    // this.username and this.jobTitle will be undefined since 'this' is referencing the global scope, as defined through the arrow function in this case.
    console.log(`User ${this.username} is  a ${this.jobTitle}`)
  }, 
  askToFriend() {
    setTimeOut(() => {
			console.log(`Would you like to add ${this.username} to your friends list?`)
    }, 2000)
  }
}
```

























