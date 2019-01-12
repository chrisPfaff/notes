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

When handling errors in Async functions the best way to go about it is to wrap what ever await function in a try and catch block. The try catch block is so important because if you have multiple async functions that run sequentialy one can fail and the other will continue. This would only be the case if the multiple awaits were inside a try block. If the second await fetch had the wrong api endpoint the first would still work while the second would log error. 

```javascript 
const doSomethingAsync = async () => {
  try {
    await fetch('https://jsonplaceholder.typicode.com/todos/1')
  .then(response => response.json())
  .then(json => console.log(json))
    await fetch('https://jsonplaceholder.typicode.com/todos/2')
  .then(response => response.json())
  .then(json => console.log(json))
  } catch(err) {
    console.log('error');
  }
}

doSomethingAsync();
```


