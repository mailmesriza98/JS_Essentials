
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


# Write a function that takes an array of promises and returns the result of the first promise that resolves, while the others are discarded.

You can achieve this by using the `Promise.race()` method, which takes an array of promises and returns the result of the first promise that resolves (or the error of the first promise that rejects). Here's a function that does exactly that:

```javascript
function racePromises(promises) {
  return new Promise((resolve, reject) => {
    for (const promise of promises) {
      promise
        .then(result => {
          resolve(result); // Resolve with the result of the first resolved promise
        })
        .catch(error => {
          // Ignore errors from rejected promises
        });
    }
  });
}

// Example usage:
const promise1 = new Promise(resolve => setTimeout(() => resolve("Promise 1"), 1000));
const promise2 = new Promise(resolve => setTimeout(() => resolve("Promise 2"), 500));
const promise3 = new Promise((resolve, reject) => setTimeout(() => reject("Promise 3 Error"), 1500));

const promises = [promise1, promise2, promise3];

racePromises(promises)
  .then(result => {
    console.log("Resolved Promise:", result); // Output: Resolved Promise: Promise 2
  })
  .catch(error => {
    console.error("Error:", error); // This won't be called because we're ignoring errors from rejected promises
  });
```

In the `racePromises` function, we iterate through the array of promises and attach a `.then()` handler to each one. The first promise that resolves will trigger the `resolve()` function, and the result of that promise will be passed to the resolved value of the returned promise. Any errors from rejected promises are ignored.

In the example usage, `promise2` resolves before the others, so it becomes the result of the `racePromises` call.

# Fetch data from an API and transform it using promises. For instance, retrieve a list of users and transform it into a list of user names.

Let's retrieve a list of users from a hypothetical API and transform it into a list of user names using promises. In this example, we'll simulate the data fetching and transformation process. You can replace the placeholder API endpoint with a real one when working with an actual API.

```javascript
// Simulated API function that returns a list of users
function fetchUsersFromAPI() {
  return new Promise((resolve) => {
    // Simulated API response with user data
    setTimeout(() => {
      const users = [
        { id: 1, name: "John Doe" },
        { id: 2, name: "Jane Smith" },
        { id: 3, name: "Bob Johnson" },
      ];
      resolve(users);
    }, 1000);
  });
}

// Function to transform the list of users into a list of user names
function transformUsersToNames(users) {
  return users.map(user => user.name);
}

// Fetch data from the API and transform it
function fetchAndTransformData() {
  fetchUsersFromAPI()
    .then(users => {
      // Transform the list of users into a list of names
      const userNames = transformUsersToNames(users);
      return userNames;
    })
    .then(userNames => {
      // Display the list of user names
      console.log("User Names:", userNames);
    })
    .catch(error => {
      console.error("Error:", error);
    });
}

// Trigger the data fetching and transformation process
fetchAndTransformData();
```

In this example:

1. `fetchUsersFromAPI()` simulates fetching user data from an API. It returns a promise that resolves with a list of users after a simulated delay.

2. `transformUsersToNames(users)` is a function that takes the list of users and transforms it into a list of user names using the `map` function.

3. `fetchAndTransformData()` is the main function that orchestrates the data fetching and transformation process. It fetches data from the API, transforms it into user names, and then displays the list of user names.

When you run the `fetchAndTransformData()` function, it will fetch user data from the API (simulated delay in this case), transform it into user names, and then log the list of user names to the console.

You can adapt this example to work with a real API by replacing the `fetchUsersFromAPI` function with an actual API request using the Fetch API or any other HTTP library.


# Create a promise-based wrapper around a third-party API (e.g., a weather API), allowing for easier integration and error handling.

 Creating a promise-based wrapper around a third-party API is a good practice for encapsulating the API's functionality, making it easier to integrate and handle errors consistently. Below is an example of creating a promise-based wrapper for a hypothetical weather API. In this example, we'll use a simple mock API for demonstration purposes:

```javascript
// Mock weather API - Replace this with your actual weather API endpoint
const mockWeatherAPI = {
  fetchWeather(city) {
    return new Promise((resolve, reject) => {
      setTimeout(() => {
        const data = {
          city: city,
          temperature: 25,
          condition: 'Sunny',
        };
        resolve(data);
      }, 1000); // Simulated API delay
    });
  },
};

// Promise-based wrapper for the weather API
class WeatherAPIWrapper {
  constructor(api) {
    this.api = api;
  }

  // Fetch weather data for a specific city
  getWeather(city) {
    return new Promise((resolve, reject) => {
      this.api
        .fetchWeather(city)
        .then(data => {
          // Check for valid data from the API
          if (!data || !data.city || !data.temperature || !data.condition) {
            throw new Error('Invalid data from the weather API');
          }
          resolve(data);
        })
        .catch(error => {
          reject(error);
        });
    });
  }
}

// Example usage of the WeatherAPIWrapper
const weatherWrapper = new WeatherAPIWrapper(mockWeatherAPI);

weatherWrapper
  .getWeather('New York')
  .then(weatherData => {
    console.log('Weather in', weatherData.city);
    console.log('Temperature:', weatherData.temperature + '°C');
    console.log('Condition:', weatherData.condition);
  })
  .catch(error => {
    console.error('Error:', error.message);
  });
```

In this example:

1. We have a mock weather API (`mockWeatherAPI`) with a `fetchWeather` method that simulates fetching weather data for a specific city.

2. We create a `WeatherAPIWrapper` class that encapsulates the weather API. It has a `getWeather` method that fetches weather data for a given city using the wrapped API and returns a promise.

3. Inside the `getWeather` method, we check for valid data received from the API, and if the data is valid, we resolve the promise with the weather data. If there's an error during the API call or the data is invalid, we reject the promise with an error.

4. In the example usage, we create an instance of the `WeatherAPIWrapper` and use it to fetch weather data for 'New York'. We handle both successful data retrieval and errors using `.then()` and `.catch()` respectively.

You can replace the `mockWeatherAPI` with the actual weather API of your choice and adapt the wrapper to suit the API's specific endpoints and response structure.

# Fetch data from an API and cache the response using promises to improve performance and reduce network requests.

Caching API responses can significantly improve performance and reduce unnecessary network requests. You can achieve this using promises and a simple cache mechanism. Here's an example of how to fetch data from an API and cache the response using promises in JavaScript:

```javascript
// Simple cache object
const cache = {};

// Function to fetch data from an API and cache the response
function fetchDataWithCache(apiEndpoint) {
  // Check if the response is already cached
  if (cache[apiEndpoint]) {
    console.log('Data retrieved from cache for:', apiEndpoint);
    return Promise.resolve(cache[apiEndpoint]);
  }

  // If not cached, fetch the data from the API
  return fetch(apiEndpoint)
    .then(response => {
      if (!response.ok) {
        throw new Error('Network response was not ok');
      }
      return response.json();
    })
    .then(data => {
      // Cache the response
      cache[apiEndpoint] = data;
      console.log('Data retrieved from API and cached for:', apiEndpoint);
      return data;
    });
}

// Example usage:
fetchDataWithCache('https://jsonplaceholder.typicode.com/posts/1')
  .then(data => {
    console.log('Data:', data);
  })
  .catch(error => {
    console.error('Error:', error);
  });

// Re-fetching the same data should come from the cache, not the network
fetchDataWithCache('https://jsonplaceholder.typicode.com/posts/1')
  .then(data => {
    console.log('Data (from cache):', data);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

In this example:

1. We create a `cache` object to store cached responses.

2. The `fetchDataWithCache` function checks if the requested data is already cached. If it is, it returns a resolved promise with the cached data. If not, it fetches the data from the API, caches it, and returns it.

3. Inside the fetch request, we use the Fetch API to retrieve data from the API endpoint. If the response is successful, we parse it as JSON and cache the data before returning it.

4. In the example usage, we fetch data from the API the first time, and it gets cached. When we request the same data again, it's retrieved from the cache rather than making another network request.

This simple cache mechanism helps improve performance by reducing redundant API requests, especially when the same data is requested multiple times. Remember that this is a basic example, and in real applications, you may want to implement more advanced cache strategies, such as cache expiration and cache size management, depending on your specific requirements.

# Fetch paginated data from an API using promises, ensuring that all pages are fetched and combined before processing.

Fetching paginated data from an API using promises can be achieved by making multiple API requests for each page and then combining the results when all pages have been fetched. You can use promises, async/await, and the `Promise.all` method for this. Here's an example:

```javascript
// Function to fetch data from a paginated API
async function fetchPaginatedData(apiEndpoint, totalPages) {
  const promises = [];

  // Create an array of promises for each page
  for (let page = 1; page <= totalPages; page++) {
    const pageUrl = `${apiEndpoint}?page=${page}`;
    const pagePromise = fetch(pageUrl)
      .then(response => {
        if (!response.ok) {
          throw new Error('Network response was not ok');
        }
        return response.json();
      })
      .catch(error => {
        console.error('Error fetching page:', page, error);
        throw error; // Rethrow the error to propagate it
      });
    promises.push(pagePromise);
  }

  try {
    // Use Promise.all to wait for all page requests to complete
    const pageResponses = await Promise.all(promises);

    // Combine the data from all pages into a single array
    const combinedData = pageResponses.reduce((result, pageData) => {
      return result.concat(pageData);
    }, []);

    // Process the combined data as needed
    console.log('Combined Data:', combinedData);
    return combinedData;
  } catch (error) {
    console.error('Error:', error);
    throw error; // Rethrow the error to propagate it
  }
}

// Example usage:
const apiEndpoint = 'https://jsonplaceholder.typicode.com/posts';
const totalPages = 3; // Replace with the actual number of pages in your API

fetchPaginatedData(apiEndpoint, totalPages)
  .then(data => {
    // Process the combined data here
    console.log('Total posts:', data.length);
  })
  .catch(error => {
    console.error('Error:', error);
  });
```

In this example:

1. We have a function `fetchPaginatedData` that fetches paginated data from an API. It takes the API endpoint and the total number of pages as arguments.

2. Inside the function, we create an array of promises (`promises`) where each promise represents fetching data for one page.

3. We use a loop to create and push promises for each page, fetching the data using the Fetch API.

4. We use `Promise.all` to wait for all page requests to complete. When all promises are resolved, it returns an array of responses (`pageResponses`).

5. We combine the data from all pages into a single array (`combinedData`) using `reduce`.

6. Finally, we process the combined data as needed and return it.

This approach ensures that all pages are fetched and combined before further processing, and it handles errors for each page request as well.


# Defference between promises and async await

Promises and async/await are both mechanisms in JavaScript for dealing with asynchronous operations, but they have different syntax and usage patterns. Here's an overview of the key differences between them:

1. **Syntax:**

   - **Promises:** Promises use a `.then()` and `.catch()` syntax for handling asynchronous operations. You chain `.then()` handlers to a promise to specify what should happen when the promise resolves, and you use `.catch()` to specify what should happen if it rejects.

   - **Async/Await:** Async/await uses the `async` keyword before a function to indicate that it contains asynchronous code. You use the `await` keyword inside the async function to pause execution until a promise is resolved. This allows you to write asynchronous code that looks more like synchronous code.

2. **Error Handling:**

   - **Promises:** Error handling in promises is typically done using the `.catch()` method or by chaining additional `.then()` handlers to handle errors at different stages of the promise chain.

   - **Async/Await:** Error handling in async/await is often done using traditional `try...catch` blocks. You can catch errors within the async function as if it were synchronous code.

3. **Readability:**

   - **Promises:** Promises can lead to callback hell or "pyramid of doom" when chaining multiple asynchronous operations. However, they can be quite explicit and readable when used with care and proper indentation.

   - **Async/Await:** Async/await is generally considered more readable and easier to understand, especially for complex asynchronous code. It allows you to write asynchronous code in a more linear, sequential style.

4. **Error Propagation:**

   - **Promises:** Errors in promises propagate through the chain, and you can catch them at various points in the chain using `.catch()`. This allows for fine-grained error handling.

   - **Async/Await:** Errors in async/await functions propagate upwards in the call stack. If an error is not caught within the async function, it will be caught by the caller, which can make error handling less granular.

5. **Compatibility:**

   - **Promises:** Promises have been available in JavaScript for a longer time and are supported in a wider range of environments, including older browsers. You can also wrap callback-based APIs with promises.

   - **Async/Await:** Async/await was introduced in ES2017 (ES8) and may not be available in older JavaScript environments without transpilation.

In summary, promises and async/await are both valuable tools for working with asynchronous code in JavaScript. Async/await is often favored for its readability and ease of use, especially for more complex asynchronous workflows. However, both have their strengths, and the choice between them may depend on factors like coding style, project requirements, and compatibility constraints.
