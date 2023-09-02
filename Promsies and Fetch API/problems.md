
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

**Chaining Promises**

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


**1. Fetching Data from an API with Error Handling:**

In this example, we'll fetch data from a remote API and handle both success and error scenarios using promises.

```javascript
function fetchDataFromAPI() {
  return fetch("https://jsonplaceholder.typicode.com/posts/1")
    .then(response => {
      if (!response.ok) {
        throw new Error("Network response was not ok");
      }
      return response.json();
    })
    .then(data => {
      console.log("Data from API:", data);
    })
    .catch(error => {
      console.error("Error:", error.message);
    });
}

fetchDataFromAPI();
```

This code fetches data from a JSONPlaceholder API endpoint and checks for network errors. If there's an error, it's caught and logged.

**2. Parallel Promise Execution:**

In this example, we fetch data from multiple APIs concurrently and wait for all promises to resolve using `Promise.all()`.

```javascript
function fetchMultipleData() {
  const urls = ["https://api.example.com/data1", "https://api.example.com/data2"];

  const promises = urls.map(url => fetch(url).then(response => response.json()));

  return Promise.all(promises)
    .then(results => {
      console.log("Data from APIs:", results);
    })
    .catch(error => {
      console.error("Error:", error);
    });
}

fetchMultipleData();
```

Here, we create an array of promises for fetching data from different APIs and then use `Promise.all()` to wait for all of them to resolve or reject.

**3. Promisify Callback Functions:**

Sometimes, you may need to work with functions that use callbacks. You can convert them into promises. Here's an example with the `fs.readFile` function:

```javascript
const fs = require("fs");

function readFileAsync(filename) {
  return new Promise((resolve, reject) => {
    fs.readFile(filename, "utf8", (err, data) => {
      if (err) {
        reject(err);
      } else {
        resolve(data);
      }
    });
  });
}

readFileAsync("example.txt")
  .then(data => {
    console.log("File contents:", data);
  })
  .catch(error => {
    console.error("Error reading file:", error);
  });
```

This code converts `fs.readFile` into a promise-based function, making it easier to work with asynchronous file reading operations.

These examples demonstrate medium-complexity scenarios involving promises, including error handling, parallel execution, and promisifying callback functions.

================================================================================
Promisifying callback functions involves converting functions that use traditional callbacks into functions that return promises. Here are a few hands-on examples of promisifying callback functions in JavaScript:

**1. Promisifying `setTimeout`:**

In this example, we'll promisify the `setTimeout` function to create a delayed promise.

```javascript
function delay(ms) {
  return new Promise(resolve => {
    setTimeout(resolve, ms);
  });
}

delay(2000)
  .then(() => {
    console.log("Delayed for 2 seconds.");
  })
  .catch(error => {
    console.error("Error:", error);
  });
```

This code creates a `delay` function that returns a promise, allowing you to create delays with `await` or `.then()`.

**2. Promisifying `fs.readFile` for File Reading:**

Here's an example of promisifying the `fs.readFile` function to read a file asynchronously with promises.

```javascript
const fs = require("fs");

function readFileAsync(filename) {
  return new Promise((resolve, reject) => {
    fs.readFile(filename, "utf8", (err, data) => {
      if (err) {
        reject(err);
      } else {
        resolve(data);
      }
    });
  });
}

readFileAsync("example.txt")
  .then(data => {
    console.log("File contents:", data);
  })
  .catch(error => {
    console.error("Error reading file:", error);
  });
```

This code wraps the callback-based `fs.readFile` with a promise, making it easier to work with file reading operations asynchronously.

**3. Promisifying `XMLHttpRequest` for AJAX Requests:**

Promisifying AJAX requests with `XMLHttpRequest`:

```javascript
function makeRequest(method, url) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open(method, url);
    xhr.onload = function () {
      if (xhr.status >= 200 && xhr.status < 300) {
        resolve(xhr.responseText);
      } else {
        reject(new Error(`Request failed with status ${xhr.status}`));
      }
    };
    xhr.onerror = function () {
      reject(new Error("Request failed"));
    };
    xhr.send();
  });
}

makeRequest("GET", "https://jsonplaceholder.typicode.com/posts/1")
  .then(response => {
    console.log("Response:", response);
  })
  .catch(error => {
    console.error("Error:", error);
  });
```

This code wraps `XMLHttpRequest` with a promise, allowing you to make HTTP requests and handle the responses more easily.

These examples demonstrate how to promisify callback-based functions, making them work seamlessly with promises, which can simplify asynchronous programming in JavaScript.
