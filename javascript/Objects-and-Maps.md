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

