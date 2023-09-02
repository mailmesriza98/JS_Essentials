
# Basic Promises

```javascript
// Creating a promise that resolves after a delay
const simplePromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Promise resolved!");
  }, 2000);
});

// Using the promise
simplePromise
  .then(result => {
    console.log(result); // Output: Promise resolved!
  })
  .catch(error => {
    console.error(error);
  });

```

In the above example, a promise simplePromise is created. It resolves after a delay of 2 seconds and logs the resolved value when the promise is fulfilled.

```javascript
// Creating a promise that rejects immediately
const errorPromise = new Promise((resolve, reject) => {
  reject("Promise rejected!");
});

// Using the promise with error handling
errorPromise
  .then(result => {
    console.log(result);
  })
  .catch(error => {
    console.error(error); // Output: Promise rejected!
  });

```

Here, a promise errorPromise is created, which rejects immediately with an error message. The error is caught and logged using the .catch() method.

**Chaining Promises

```javascript
// Creating a promise that resolves with a number
const promise1 = new Promise((resolve, reject) => {
  resolve(5);
});

// Chaining promises
promise1
  .then(result => {
    console.log(result); // Output: 5
    return result * 2;
  })
  .then(result => {
    console.log(result); // Output: 10
  });
```
In this example, two .then() handlers are chained together. The first handler logs the result and returns a modified value, which is then passed to the second handler for further processing.

These are simple examples of promises in JavaScript, demonstrating how promises can be used to handle asynchronous operations and error handling.

