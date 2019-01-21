# async/await

You can `await` every promise in Javascript in case a library you're using is returning a Promise simply `await` it. In fact `async/await` is just syntactical sugar around promises. To make your code work, you only need to add the `async` keyword in front of a function

```javascript
async function getData() {
    const result = await axios.get('https://dube.io/service/ping')
    const data = result.data
    
    console.log('data', data)
    
    return data
}

getData();
```

Note that `await` on the top level is not possible, you can only call an `async` function.

# async control flow

Often times it is necessary to fetch mulitiple datatsets and do something for each of those or complete a task after all of the async calls have returned a value.

### for...of

Let’s say we have a couple of Pokemon on our page, and we have to fetch detailed information about them. We do not want to wait for all calls to finish, especially when we don’t know how many there are, but we want to update our datasets as soon as we get something in return. We can use `for...of` to loop through an array and execute `async` code inside the block, the execution will be halted until each call has succeeded. It is important to note that there may be performance bottlenecks if you do something like this in your code, but it is very useful to keep in your toolset. Here is an example:

```javascript
import axios from 'axios'

let myData = [{id: 0}, {id: 1}, {id: 2}, {id: 3}]

async function fetchData(dataSet) {
    for(entry of dataSet) {
        const result = await axios.get(`https://ironhack-pokeapi.herokuapp.com/pokemon/${entry.id}`)
        const newData = result.data
        updateData(newData)
        
        console.log(myData)
    }
}

function updateData(newData) {
    myData = myData.map(el => {
        if(el.id === newData.id) return newData
        return el
    })
}
```

### Promise.all

This allows you to fetch in parallel

```javascript
import axios from 'axios' 

let myData = [{id: 0}, {id: 1}, {id: 2}, {id: 3}]

async function fetchData(dataSet) {
    const pokemonPromises = dataSet.map(entry => {
        return axios.get(`https://ironhack-pokeapi.herokuapp.com/pokemon/${entry.id}`)
    })

    const results = await Promise.all(pokemonPromises)
    
    results.forEach(result => {
        updateData(result.data)
    })
    
    console.log(myData) 
}

function updateData(newData) {
    myData = myData.map(el => {
        if(el.id === newData.id) return newData
        return el
    })
}
```

# Destructuring and default values

```javascript 
const result = axios.get(`https://ironhack-pokeapi.herokuapp.com/pokemon/${entry.id}`)
const data = result.data
```
There us an easier way to do this, we can use destructuring to just take one or some of values from and object or an array. We would like this:

```javascript
const { data } = await axios.get(...)
```
You can also rename the variable
```javascript
const { data: newData } = await axios.get(...)
```
Another nice trick is to give `default values` when destruturing. This ensures that you will never end up with undefined and dont have to check the variables maually.
```javascript
const { id = 5 } = {}
console.log(id) // 5
```
These tricks can also be used with function parameters for example:
```javascript
function calculate({operands = [1, 2], type="addition"} = {}) {
    return operands.reduce((acc, val) => {
        switch(type) {
             case 'addition':
                return acc + val
            case 'subtraction':
                return acc - val
            case 'multiplication':
                return acc * val
            case 'division':
                return acc / val
        }
    }, ['addition', 'subtraction'].includes(type) ? 0 : 1)
}

console.log(calculate()) // 3
console.log(calculate({type: 'division'})) // 0.5
console.log(calculate({operands: [2, 3, 4], type: 'multiplication'})) // 24
```
The example might seem a bit confusing at first, but take your time and play around with it. When we do not pass any values as arguments to our function, the default values are used. As soon as we start passing values, only the default values for non-existing arguments are used.

# Truthy and falsy values
When using default values, some of the checks for existing values will be a thing of the past. However, it is very nice to know that you can work with truthy and falsy values. This will improve your code and save you a couple of instructions, making it more eloquent. Often times I see people doing something like:

```javascript
if(myBool === true) {
  console.log(...)
}
// OR
if(myString.length > 0) {
  console.log(...)
}
// OR
if(isNaN(myNumber)) {
  console.log(...)
}
```
All of those can be shortened to 

```javascript
if(myBool) {
  console.log(...)
}
// OR
if(myString) {
  console.log(...)
}
// OR
if(!myNumber) {
  console.log(...)
}
```

To really take advantage of these statements, you have to understand what truthy and falsy values are. Here is a small overview:

### falsy
* strings with the lenght of 0
* the number 0
* false
* undefiend
* null
* NaN
### truthy
* empty arrays
* empty objects
* everythng else

Note that when checking for truthy / falsy values, there is no explicit comparison, which equates to checking with double equal signs == and not three ===. In general, it behaves the same way but there are certain situations where you will end up with a bug. For me, it happened mostly with the number 0 .

# Logical and ternary operators

These are, again used to shorten your code, saving you precious lines of code. Often times they are nice tools and help keep your code clean, but they can also create some confusion, especially when chaining them.

### logical operators
The logical operators basically combine two expressions and will return either `true`, `false` or the matching value and are represented by `&&`, meaning "and" as well as `||` meaning or.

```javascript
console.log(true && true) // true
console.log(false && true) // false
console.log(true && false) // false
console.log(false && false) // false
console.log(true || true) // true
console.log(true || false) // true
console.log(false || true) // true
console.log(false || false) // false
```

We can combine logical operators with our knowlege form the last point, truthy and falsey values. When using logical operators, the following rules apply:

* `&&` : The first falsey value gets returned, if there us none, the last truthy value is being returned
* `||`: The first truthy value gets returned, if there is none, the operation will equal to the last falsy value.

```javascript
console.log(0 && {a: 1}) // 0
console.log(false && 'a') // false
console.log('2' && 5) // 5
console.log([] || false) // []
console.log(NaN || null) // null
console.log(true || 'a') // true
```

### Ternary operator

The ternary operator is very similiar tot he logical operator, but has three parts in order: 
* The comparison, which will either be falsy or truthy
* The first return value, in case the comparision is truthy
* The second return value, in case the comparison is falsy

```javascript
const lang = 'German'
console.log(lang === 'German' ? 'Hallo' : 'Hello') // Hallo
console.log(lang ? 'Ja' : 'Yes') // Ja
console.log(lang === 'French' ? 'Bon soir' : 'Good evening') // Good eveing
```







