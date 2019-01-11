# Async Await

In ES2015 Promises were meant to solve a problem with asynchronouse code and solve the callback hell problem. Though they did help they had some of the same issues as callbacks as well as a complexity issue. When async functions were introduced which is just promises with a better syntax this helped code look like it was synchronous but in reality it is non-blocking behind the scenes.

An async function ALWAYS returns a promise like this for example

```javascript
const doSomethingAsync = () => {
    return new Promise((resolve) => {
        setTimeout(() => resolve('I did something'), 3000)
    })
}
```

If you were to call this function with the await keyword in front of it the code will stop until the promise is resolved or rejected. 

```javascript
“const doSomeThingElseAsync = async () => {
    console.log(await doSomethingAsync())
}
```

When handling errors in Async functions the best way to go about it is to wrap what ever await function in a try and catch block. 

```javascript 
const fetch = require('node-fetch');

const doSomethingAsync = async () => {
  try {
    const getData = await fetch('https://jsonplaceholder.typicode.com/todos/1')
  .then(response => response.json())
  .then(json => console.log(json))
  return getData;
  } catch(err) {
    console.log('eeeerrrrorr');
  }
}

doSomethingAsync();


```

