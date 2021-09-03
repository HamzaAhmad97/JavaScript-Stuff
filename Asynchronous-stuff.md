# Asynchronous JavaScript

Before you start it is useful to understand the fetch API.

## The main idea

The main idea is that since js is single threaded, when we want to do something that requires us to wait until it is done like fetching data from a server or waiting for a user to give access to his camera and microphone, generally this will block the main thread, meaning that the who program will look like it is frozen since it is waiting for the results, so the solution is using asynch methods to allow the program to run normally and letting the things that are waiting for some kind of a response to work separately (usually on helper threads) and when they are finished their result will be used without blocking the main thread.

**You can't include an async code block that returns a result, which you then rely on later in a sync code block. You just can't guarantee that the async function will return before the browser has processed the sync block.**

## The execution context 

It is basically the **environment** where the js code is evaluated and executed. Whenever any code is run in JavaScript, it’s run inside an execution context.

The function code executes inside the function execution context, and the global code executes inside the global execution context. Each function has its own execution context.

## The stack

A last in first out structure (LIFO), it is basically used to store the execution context. **main()** is referred to as the global execution context.

![](https://www.javascripttutorial.net/wp-content/uploads/2019/12/JavaScript-Call-Stack.png)

## The event loop

The job of the Event loop is to look into the call stack and determine if the call stack is empty or not. If the call stack is empty, it looks into the message queue to see if there’s any pending callback waiting to be executed.


![](https://miro.medium.com/max/700/1*O_H6XRaDX9FaC4Q9viiRAA.png)

Suppose we have this code snippet:

```
const networkRequest = () => {
  setTimeout(() => {
    console.log('Async Code');
  }, 2000);
};
console.log('Hello World');
networkRequest();
console.log('The End');
```

The order with which the code will execute is as follows (I will not mention that everything that is about to execute will be pushed to the call stack, this is the normal behaviour, just know that everything that will get executed will be pushed to the call stack):

* at first 'Hello World' will get printed in the console.
* after that networkRequest will get called, since it has setTimeout which is part of the web APIs it a timer for 2 seconds will start.
* then 'the end will get printed.
* once 2 seconds pass, the call back in setTimeout which is `console.log('Async Code'); `will get pushed to the **message queue/ task queue**.
* finally, **once the call stack is empty**, the calback will get pushed to the stack and gets executed.

The message queue also contains the callbacks from the DOM events.

## The job queue

It is almost the same as the message queue but the difference is that is has higher priority, which means that they will get executed before the callbacks inside the message queue.

## Asynchronous js

Take this as an example:

```
let response = fetch('myImage.png'); // fetch is asynchronous
let blob = response.blob();
```

this will throw an error since the response will not be available at the time of the execution of the second line, so since most web APIs are asynchronous, we will need to do something else like using promises.

## Old school callbacks

They are function that are specified as arguments when calling a function which will start executing code in the background. When the background code finishes running, it calls the callback function to let you know that the work is done, an example is the tradition **addEventListener()** method.

Note that we only pass the callback function as an argument, only pass the function's reference, not the function itself, meaning that we do not put parantheses after it or we will be calling the function instead, like so `btn.addEventListener('click', () => {alert('You clicked me!');})`.

## Promises

A Promise is an object that represents an intermediate state of an operation — in effect, a promise that a result of some kind will be returned at some point in the future. 

### 1. Web APIs that return a promise 

Generally, the code will look like this:

```
doSth.then(...).catch(...)
```

Knowing that doSth returns a promise. And everything that relies on the result of that task will get executed inside the *then* block, *catch* just like try/ catch blocks, will catch errors.

Again, suppose that doSth is a function, or consider that the whole code is contained in another function, note that even if the results were not yet retreived, the function will return almost immediately, and even the whole containing function returns, when doSth finished working, it calls the handler you provide, meaning that it keeps on running.

Example:

```
fetch('coffee.jpg')
.then(response => {
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  } else {
    return response.blob();
  }
})
.then(myBlob => {
  let objectURL = URL.createObjectURL(myBlob);
  let image = document.createElement('img');
  image.src = objectURL;
  document.body.appendChild(image);
})
.catch(e => {
  console.log('There has been a problem with your fetch operation: ' + e.message);
});
```


Here fetch returns a promise that we are storing in a variable called promise, since the promise represents an intermediate state, here we can say that the status of the promise is **pending**.

When the promise **fulfills** (when a response object is returned) the chained **.then** method will get executed, and the response object will get passed to that code inside the then after the promise as a parameter.

The way that a .then() block works is similar to when you add an event listener to an object using AddEventListener(). It doesn't run until an event occurs (when the promise fulfills). The then block also returns a promise.



1. When a promise is created, it is neither in a success or failure state. It is said to be pending.

2. When a promise returns, it is said to be resolved.

2.a. A successfully resolved promise is said to be fulfilled. It returns a value, which can be accessed by chaining a .then() block onto the end of the promise chain. The callback function inside the .then() block will contain the promise's return value.

2.b. An unsuccessful resolved promise is said to be rejected. It returns a reason, an error message stating why the promise was rejected. This reason can be accessed by chaining a .catch() block onto the end of the promise chain.

### Dealing with multiple promises fulfilling

It is basically used when you want to do something if and only if multiple promises fulfill.

```
Promise.all([a, b, c]).then(values => {
  ...
});
```

### finally

When you want to execute a block of code regardless of whether a promise fulfills or gets rejected.

It looks like this:

```
myPromise
.then(response => {
  doSomething(response);
})
.catch(e => {
  returnError(e);
})
.finally(() => {
  runFinalCode();
});
```

### 2. Web APIs that DO NOT return a promise (custom promises)

Using the **Promise()** constructor.

```
let timeoutPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve('Success!');
  }, 2000);
});
```
resolve() and reject() are functions that you call to fulfil or reject the newly-created promise. The value inside either reslove or reject gets passed to the chained .then method. but in the case of reject() it is the value that will get passed to the catch block.

```
function timeoutPromise(message, interval) {
  return new Promise((resolve, reject) => {
    if (message === '' || typeof message !== 'string') {
      reject('Message is empty or not a string');
    } else if (interval < 0 || typeof interval !== 'number') {
      reject('Interval is negative or not a number');
    } else {
      setTimeout(() => {
        resolve(message);
      }, interval);
    }
  });
};
```
This function returns a promise so we can chain .then blocks and a .catch block as before.

## async and await


### 1. asynch 

Gets put in front of a dunction declaration (can also have async function expressions and arrow functions) and turns it into an async function, and the function will be guarnteed to return a promise.

An async function is a function that knows how to expect the possibility of the await keyword being used to invoke asynchronous code.

```
let hello = async () => { return "Hello" };

hello().then((value) => console.log(value))
```

### 2. await

await can be put in front of any async promise-based function to pause your code on that line until the promise fulfills, then return the resulting value. You can use await when calling any function that returns a Promise, including web API functions.

```
async function hello() {
  return greeting = await Promise.resolve("Hello");
};

hello().then(alert);
```
The prev example can be written as follows using async and await:

``` 
async function myFetch() {
  let response = await fetch('coffee.jpg');

  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }

  let myBlob = await response.blob();

  let objectURL = URL.createObjectURL(myBlob);
  let image = document.createElement('img');
  image.src = objectURL;
  document.body.appendChild(image);
}

myFetch()
.catch(e => {
  console.log('There has been a problem with your fetch operation: ' + e.message);
});
```

Since an async keyword turns a function into a promise, you could refactor your code to use a hybrid approach of promises and await, bringing the second half of the function out into a new block to make it more flexible:

```
async function myFetch() {
  let response = await fetch('coffee.jpg');
  if (!response.ok) {
    throw new Error(`HTTP error! status: ${response.status}`);
  }
  return await response.blob();

}

myFetch().then((blob) => {
  let objectURL = URL.createObjectURL(blob);
  let image = document.createElement('img');
  image.src = objectURL;
  document.body.appendChild(image);
}).catch(e => console.log(e));
```

await only works inside of async functions.

The await keyword causes the JavaScript runtime to pause your code on this line, not allowing further code to execute in the meantime until the async function call has returned its result — very useful if subsequent code relies on that result.

You can use the traditional try/catch to handle errors with async/ await

# End







