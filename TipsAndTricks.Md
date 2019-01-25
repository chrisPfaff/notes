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

# optional chaining
To solve the problem of accesing a nested object property, withouth knowing ig the object or one of the sub-properties even exists you can do optional chaning. Something that would look like this
```javascript
let data
if(myObj && myObj.firstProp && myObj.firstProp.secondProp && myObj.firstProp.secondProp.actualData) data = myObj.firstProp.secondProp.actualData
```
Can be made to look like this
```javascript
const data = myObj?.firstProp?.secondProp?.actualData
```
Currently this is not part of the spec and is only avaliable if you add babel-plugin-proposal-optional-chaining in the babelrc

# Class properties and binding
Binding functions in Javascript is a common task. With the introduction of arrow functions in the es6 spec, we now have a way to automatially `bind functions to the declaration context` very useful and commonly used amongst Javascript devs. When classes were first introduced, you could no longer really use arrow functions because class methods have to be declared in a specific way. We needed to bind functions elsewhere, for example in the constructor(best practice with React). I was always bugged by the workflow of first defining a class methods then binding them. It just seems rediculous after a while. With the class property syntax, we can use arrow functions again and get the advantages of auto-binding. Arrow function can now be used inside the class. Here is an example.
```javascript
class Counter extends React.Component {
    constructor(props) {
        super(props)
        this.state = { count: 0 }
    }
    
    render() {
        return(
            <div>
                <h1>{this.state.count}</h1>  
                <button onClick={this._increaseCount}>Increase Count</button>
            </div>
        )
    }
    
    _increaseCount = () => {
        this.setState({ count: this.state.count + 1 })
    }
}
```
Currently, class properties are not part of the official spec, but is at stage-3 as an experimental feature. You have to add @babel/plugin-proposal-class-properties in your babelrc to use it.

# User parcel
As a frontend developer, you almost certainly have encountered bundling and transpiling code. The de-facto standard for this was webpack for a long time. I first used webpack in version 1, which was a pain back then. Fiddling with all the different configuration options, I spent countless hours trying to get the bundling up and running. If I was able to do so, I wouldn’t touch it again in order not to break anything. A couple of months ago I came across parcel, which was an instant relief. It does pretty much everything for you out of the box, while still giving you the possibility to change it, if necessary. It also supports a plugin system, similar to webpack or babel and is incredibly fast. If you don’t know parcel, I definitely suggest you check it out!

#Truthy/falsey boolean conversion 
In JavaScript, any value can be evaluated in a boolean context.
If a value is evaluated to true it is said to be truthy and falsy otherwise.
The following values will always be evaluated to false in a boolean context.

* false
* null
* undefined 
* 0
* '', " "
* NaN

Anything else will be evaluated to true in a boolean context.

Sometimes we want to convert a value that is not a boolean, into a boolean.
We can accomplish that using the !! operator.

```javascript
!!null // false
!!undefined // false
!!NaN // false
!!"" // false
!!0 // false

!!1 // true
!!{} // true
!![] // true
!!"hi, mom" // true
```

# Object.entries

Maybe you were already aware that you can use Object.keys() to return a list containing the key-names of an object.
This is handy when you want to iterate through an object like so
```javascript
const obj = {
  msg: "hi",
  to: "mom",
  year: 2019
}

Object.keys(obj).forEach(k => {
  console.log(k);
});

// 'msg'
// 'to'
// 'year'
```

But you might not be aware that you can use Object.entries() to return a list of entries containing both the key-name and the value of an object.

```javascript
const obj = {
  msg: "hi",
  to: "mom",
  year: 2019
}

Object.entries(obj).forEach(([k, v]) => {
  console.log(k + " : " + v);
});

// 'msg : hi'
// 'to : mom'
// 'year : 2019'
```

If you didn’t figure it out yourself already, you can of course also return a list containing only the values, by using Object.values() like so
```javascript
const obj = {
  msg: "hi",
  to: "mom",
  year: 2019
}

Object.values(obj).forEach(v => {
  console.log(v);
});

// 'hi'
// 'mom'
// '2019'
```

# Rest and Spread with Objects

In ES6, the rest and spread operator was introduced.
They have very different effects, but are both used by setting three dots ...

* Spread operator allow iterables to be expanded into single arguments/element.
* Rest operator collects all remaining elements into an iterable.

The rest operator can be applied to arrays as well as objects, and this can be a strong tool when used correctly.

By combining destructuring and the rest operator on objects, we can easily extract wanted properties from an object, leaving the remaining properties in an object for itself.

```javascript
const obj = {
  msg: "hi",
  to: "mom",
  year: 2019,
  seen: false,
}

const { year, ...remainingObj } = obj;

console.log(year);
// 2019

console.log(remainingObj); 
// {
//  msg: 'hi',
//  seen: false,
//  to: 'mom'
// }
```
This is also really handy when we want to clean certain properties from an object.
No need for iterating through the whole object and creating a new clean object.

If you want to read more about the spread and rest operator, I suggest you read the article: Recursion in JavaScript with ES6, destructuring and rest/spread by Hugo Di Francesco.

# Finally 

Promises have become a huge thing in JavaScript.
As the entirety of this topic is beyond the scope of this article, I want to focus on a new function; finally() that has been added to JavaScript Promises as an instance method and can be used in extension with then().catch()

finally() is called without any value and is called regardless of a promise being resolved or rejected. That is, it is executed no matter what.

```javascript
const aPromise = new Promise((resolve, reject) => resolve("alles gut"));

aPromise
  .then(res => console.log(res)) // alles gut
  .catch(err => console.log(err))
  .finally(() => {
    // This is always executed!
  });
```
```javascript
const aPromise = new Promise((resolve, reject) => reject("uhff"));

const resolveThePromise = async () => {
  try {
    const msg = await aPromise;
    console.log(msg); 
  } 
  catch(err) {
    console.log(err); // uhff
  }
  finally {
    // this is still always executed!
  }
}

resolveThePromise();
```




















