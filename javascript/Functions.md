# Functions

**Important:** functions, if the `return` keyword is not specified, JavaScript will return `undefined` by default. An exception to this is with Arrow functions, where the `return` is implied.

### Closures

A closure gives you access to an outer function’s scope from an inner function (MDN, n.d.). In a way, we could say that it's when a function returns another function whose parameters can be accessed from its parent function? 

```js
function countdown(start, step) {
  let result = start + step 
  // if step wasn't added the starting number in the output would actually begin at the number of steps less.
  
  return function decrease() {
    result -= step
    return result
  }
}

const output = countdown(20, 5);

console.log(output()) // output is logged with () because its value is a function
```

---

### Default parameters

Consider the following function:

```js
// 1.
function convertTemperature(celsius, decimalPlaces) {
  const farhrenheit = celsius * 1.8 + 32
  return fahrenheit.toFixed(decimalPlaces)
}
// => In this simple function, the toFixed method would round the resulting temperature by the number of decimal places provided. The problem here is that toFixed returns a string. A quick solution would be to do wrap the return into the Number function:

function convertTemperature(celsius, decimalPlaces) {
  const farhrenheit = celsius * 1.8 + 32
  return Number(fahrenheit.toFixed(decimalPlaces))
}
console.log(convertTemperature(21, 1)) // => 69.8 => seems to be working fine.


// 2. Suppose that we don't know how many decimal places yet and were to only pass the celcius. The end result will be wrong:

console.log(convertTemperature(21)) // => 70

// A solution to this would be to write a conditional to set a default value if the argument isn't passed into the function:

function convertTemperature(celsius, decimalPlaces) {
  if (!decimalPlaces) {
    decimalPlaces = 1
  }
  const farhrenheit = celsius * 1.8 + 32
  return Number(fahrenheit.toFixed(decimalPlaces))
}
console.log(convertTemperature(21)) // => 69.8 => problem fixed


// 3. Another way to improve this would be by using short-circuiting instead of the if statement.
function convertTemperature(celsius, decimalPlaces) {
  // in this short circuit, if there decimalPlaces exist, then the provided value is stored in decimalPlaces; otherwise, it defaults the value to 1.
  decimalPlaces = decimalPlaces || 1
  
  const farhrenheit = celsius * 1.8 + 32
  return Number(fahrenheit.toFixed(decimalPlaces))
}
console.log(convertTemperature(21, 1)) // => 69.8 
console.log(convertTemperature(21, 0)) // => still 69.8 ... why?

// Despite specifying that there should be no decimal places. What's happening? 
// In an expression like 0 || 1, JavaScript interprets 0 is a falsy value, so that's why the decimalPlaces value is still defaulting to 1. 


// 4. The best way to avoid all of this is to set a default value within the function declaration:
function convertTemperature(celsius, decimalPlaces = 1) {
  const farhrenheit = celsius * 1.8 + 32
  return Number(fahrenheit.toFixed(decimalPlaces))
}
console.log(convertTemperature(21)) // => 69.8

// Since the default value is now an integer, when we pass a decimalPlaces argument of 0, JavaScript will recognize it as an integer instead of a falsy value.

console.log(convertTemperature(21, 0)) // => 70
```

---

### Partial Application for Single-Responsibility Functions

Here's how to take advantage of **closures** and **callback functions** to fetch data from an API and assign specific parts of it to Single-Responsibility functions. This helps in cutting down repetition (i.e. making the code DRY) and make things overall easier to follow.

```js
// 1. The following function gets the data from a REST API given the URL and the route.
function getData(baseUrl, route) {
  fetch(`${baseUrl}${route}`)
  // Once it fetches the API, it will return a response. The callback here transfers the response into JSON.
  	.then(res => res.json()) 
  // Once we have the data in JSON, the callback logs the data itself to the console.
  	.then(data => console.log(data))
}
getData('https://jsonplaceholder.typicode.com', '/posts')


// 2. Rewritten as a Partial Application
function getData(baseUrl) { 			// => const getSocialMediaData
  return function(route) { 				// => getSocialMediaData('/posts')
    return function(callback) {   // => getSocialMediaPosts(callback)
      fetch(`${baseUrl}${route}`)
      	.then(response => response.json())
      	.then(data => callback(data))
    }
  }
}
// The single responsibility here is for getSocialMediaData to get the data from the base url.
const getSocialMediaData = getData('https://jsonplaceholder.typicode.com')

// Since what's being actually assigned to getSocialMediaData is the RETURN of the getData function, we can pass in the ROUTE in order to get data specific to whatever route is passed.
getSocialMediaData('/posts')

// If we wanted to go a level deeper...
const getSocialMediaPosts = getSocialMediaData('/posts')

// Here we're passing a callback into getSocialMediaPosts because that's the RETURN value of getSocialMediaData('/posts')
getSocialMediaPosts(posts => {
  posts.forEach(post => console.log(post.title))
})


// Maybe rewritting the function as an Arrow function would be cleaner, but it also makes it a bit harder to follow (in my opinion).
const getData = (baseUrl) => (route) => (callback) => {
  fetch(`${baseUrl}${route}`)
    .then(response => response.json())
    .then(data => callback(data))
	}
}
```

---

























---

### References

MDN. (n.d.). Closures. Retrieved from https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures





