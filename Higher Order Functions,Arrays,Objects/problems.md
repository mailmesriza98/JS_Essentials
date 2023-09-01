# Implement your own version of filter

Implement filter: Create a function filter that takes an array and a predicate function (a function that returns a boolean) and returns a new array containing only the elements that satisfy the predicate.

```javascript
function myFilter(array, predicate) {
  const filteredArray = [];

  for (let i = 0; i < array.length; i++) {
    if (predicate(array[i])) {
      filteredArray.push(array[i]);
    }
  }

  return filteredArray;
}
function predicate(num){
return num<5;
}
```


function myFilter(array, predicate): This declares a function named myFilter that takes two arguments: an array and a predicate function. The predicate function is a function that returns a boolean value based on some condition.
const filteredArray = [];: This initializes an empty array called filteredArray, which will store the elements that satisfy the predicate condition.
for (let i = 0; i < array.length; i++) { ... }: This loop iterates through each element of the input array.
if (predicate(array[i])) { ... }: Inside the loop, the predicate function is invoked with three arguments:If the predicate function returns true for the current element, it means the element satisfies the condition. In that case, the element is pushed to the filteredArray.
array[i]: The current element of the array being processed.
return filteredArray;: After the loop is done, the filteredArray containing only the elements that satisfy the predicate is returned.


# Implement composition of functions

```javascript
function compose(...functions) {
  return function(x){
    for(let i=functions.length-1;i>=0;i--){
      x=functions[i](x);
    }
    return x;
}

function addTwo(x) {
    return x + 2;
}

function multiplyByThree(x) {
    return x * 3;
}

function subtractTen(x) {
    return x - 10;
}

const composed = compose(subtractTen, multiplyBythree, addTwo);
const result = composed(5);

console.log(result); // Output will be (5 + 2) * 3 - 10 = 11
```

In this simplified version of compose, we iterate through the array of functions in reverse order and directly apply each function to the value x, updating x with the result of each function application. 

# Implement your own version of foreach

Problem statement: 
Write your own version of the forEach function, which iterates over an array and applies a function to each element.

```javascript
const numbers = [1, 2, 3, 4, 5];

function printSquare(num) {
  console.log(num * num);
}

function doublePrint(num) {
  console.log(num * 2);
}

myForEach(numbers, printSquare); 
myForEach(numbers, doubleAndPrint); 
```

Now lets see what the myForEach function does:

```javascript
function myForEach(array,callback){
  for(let i=0;i<array.length;i++){
      callback(array[i]);
   }

}
```

So here the myForEach function essentially loops through all the elements of the array and calls the function as per the initial call of foreach

so if myForEach(numbers,printSquare) is called.: the line inside the for loop calls the printSquare function with the element at a particular index of nums array.

# Implement your own version of Reduce

```javascript
function myReduce(reducer, array, initial) {
    let accumulator = initial !== undefined ? initial : array[0];

    for (let i = initial !== undefined ? 0 : 1; i < array.length; i++) {
        accumulator = reducer(accumulator, array[i]);
    }
   
    return accumulator;
}

// Example usage
const numbers = [1, 2, 3, 4, 5];
const sumResult = myReduce((x, y) => x + y, numbers);
console.log(sumResult);  // Output: 15
```

The myReduce function takes three arguments:

reducer: A function that defines how two values should be combined into one. It takes two arguments and returns a single result.
array: The array of values that you want to accumulate.
initial: An optional initial value for the accumulation. If provided, the accumulation starts with this value; otherwise, it starts with the first element of the array.
Inside the function, accumulator is initialized. If an initial value is provided, it's used as the initial accumulator value. Otherwise, if no initial value is provided, the first element of the array is used as the initial accumulator value.

The for loop starts iterating over the array. If an initial value is provided, the loop starts from index 0; otherwise, it starts from index 1 to skip the first element since it's already set as the initial accumulator.

In each iteration, the reducer function is applied to the current accumulator value and the next element of the array (array[i]). The result of this reduction becomes the new value of the accumulator.

Once all elements have been iterated through, the final accumulated value is returned as the result of the myReduce function.

The example usage demonstrates how to use the myReduce function to sum up the numbers in the numbers array.

As for the differences between myReduce and Array.prototype.reduce, I've explained them in the previous response. The key takeaway is that Array.prototype.reduce is a built-in method with better error handling, potential performance optimizations, and broader recognition among developers. However, creating your custom version like myReduce can help you understand the underlying concepts and mechanics of reducing operations in JavaScript.

const sumResult = myReduce((x, y) => x + y, numbers);

Let's break down the line:

const sumResult: This declares a constant variable named sumResult which will hold the result of the accumulation performed by the myReduce function.

myReduce((x, y) => x + y, numbers): This is a call to the myReduce function. Here's what's happening within this call:

The first argument is a reducer function (x, y) => x + y. This function takes two arguments (x and y) and returns their sum (x + y).
The second argument is the numbers array that you want to accumulate.
Since there is no third argument provided, the initial value for accumulation will be the first element of the numbers array (which is 1).
;: This semicolon marks the end of the statement.

So, the line of code is essentially instructing the myReduce function to iterate through the numbers array and use the provided reducer function (x, y) => x + y to accumulate the values by adding them together. The result, in this case, will be the sum of all the numbers in the numbers array, which is 15.


# Given an array of strings, use the map function to transform each string to uppercase and return the modified array.

```javascript
const inputArray = ["hello", "world", "example", "strings"];

const uppercaseArray = inputArray.map(str => str.toUpperCase());

console.log(uppercaseArray);
```


# Use the reduce function to calculate the sum of all numbers in an array.

```javascript
const arr = [1,2,3,4,5]
const sum = arr,reduce((sum,cur)=>{
  return sum+cur;
},0)

console.log(sum); // Output: 15 (1 + 2 + 3 + 4 + 5)
```

In this example, the reduce function is used to iterate over each number in the numbers array. The accumulator starts with an initial value of 0, and for each number, it accumulates the sum by adding the currentValue to it. The final sum is stored in the sum variable and printed to the console


# Write a function that finds the maximum value in an array using the reduce function.

```javascript
function findMaxValue(array) {
    if(array.length===0) return undefined
    return arr.reduce((max,cur)={return max>cur?max:cur},array[0])
}

const numbers = [3, 8, 2, 10, 5];

const maxValue = findMaxValue(numbers);

console.log(maxValue); // Output: 10 (maximum value in the array)
```

In this function:

We first check if the array is empty, in which case we return undefined.
The reduce function iterates over the array. For each element, it compares the currentValue with the current max value. If the currentValue is greater, it becomes the new max value; otherwise, the max value remains the same.
The initial value of max is set to the first element of the array (array[0]).
The final result is the maximum value in the array, which is then stored in the maxValue variable and printed to the console.


# Chaining higher order functions

```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// Step 1: Use filter to get even numbers
const evenNumbers = numbers.filter(number => number % 2 === 0);

// Step 2: Use map to square each even number
const squaredEvenNumbers = evenNumbers.map(number => number ** 2);

// Step 3: Use reduce to calculate the sum
const sumOfSquaredEvenNumbers = squaredEvenNumbers.reduce((sum, currentValue) => {
    return sum + currentValue;
}, 0);

console.log(sumOfSquaredEvenNumbers); // Output: 220 (4 + 16 + 36 + 64 + 100)
```


# Function decorators:
Create a higher-order function repeat that takes a function and a number n, and returns a new function that calls the original function n times.

```javascript
function repeat(fn,n){
      return function(...args){
        for(let i=0;i<n;i++){ 
                  fn(...args);
        }
     }
}
```

create the repeat higher-order function in JavaScript:

```javascript
function repeat(fn, n) {
    return function(...args) {
        for (let i = 0; i < n; i++) {
            fn(...args);
        }
    };
}
```

In this function:

fn is the function you want to repeat.
n is the number of times you want to call the function.
The returned function uses the rest parameter ...args to capture any arguments that are passed to it.
Inside the returned function, a loop is used to call the original function n times, passing along any arguments.

example of the above

```javascript
function greet(name) {
    console.log(`Hello, ${name}!`);
}

const repeatedGreet = repeat(greet, 3);
repeatedGreet("Alice");  // Output: Hello, Alice!
                         //         Hello, Alice!
                         //         Hello, Alice!
```


In this example, the repeat function is used to create a new function repeatedGreet that will call the greet function 3 times. When you call repeatedGreet("Alice"), it calls greet("Alice") three times, printing the greeting three times


# Currying

 Currying is a technique in functional programming where a function that takes multiple arguments is transformed into a series of functions that each take a single argument. The curried function returns new functions that, when called with arguments, progressively accumulate and process those arguments until all the required arguments are supplied, at which point the original function is executed and the result is returned.

```javascript
function curry(binaryFn) {
    return function(firstArg) {
        return function(secondArg) {
            return binaryFn(firstArg, secondArg);
        };
    };
}

function add(x, y) {
    return x + y;
}

const curriedVal = curry(add);
const add5 = curriedVal(5);
const add3 = add5(3)  //output: 8
```

the curry function takes a binary function (a function that takes two arguments) and returns a curried version of it. The returned curried function takes arguments one at a time and returns new functions until all the required arguments are gathered.

Here's a step-by-step breakdown:

The curry function takes a binary function, like add.
When you call curriedAdd(5), it returns a new function that takes one argument.
When you call the returned function with an argument, like add5(3), it applies the original binary function (add) to the accumulated arguments (5 and 3) and returns the result.
In this way, currying allows you to break down the process of applying a function with multiple arguments into a sequence of single-argument function calls. This can make code more modular and flexible, especially in functional programming contexts.


# Write a function that flattens a nested array using reduce.

```javascript
function flattenArray(arr) {
    return arr.reduce((flatArray, currentElement) => {
        if (Array.isArray(currentElement)) {
            return flatArray.concat(flattenArray(currentElement));
        } else {
            return flatArray.concat(currentElement);
        }
    }, []);
}

const nestedArray = [1, [2, [3, 4], 5], 6, [7, 8]];

const flattenedArray = flattenArray(nestedArray);

console.log(flattenedArray); // Output: [1, 2, 3, 4, 5, 6, 7, 8]
```


The flattenArray function takes an array as input and uses reduce to process each element.
If the current element is an array, it recursively calls flattenArray to further flatten it.
Otherwise, it directly adds the current element to the flatArray.
The initial value of the accumulator (flatArray) is an empty array ([]).
The resulting flattenedArray contains all the elements from the nested array flattened into a single-level array.


# Create a function partial that takes a function and some arguments, and returns a new function with those arguments pre-filled.

```javascript
function partial(fn, ...args) {
    return function(...remainingArgs) {
        return fn(...args, ...remainingArgs);
    };
}

function greet(greeting, name) {
    console.log(`${greeting}, ${name}!`);
}

const sayHello = partial(greet ,"Hello);
sayHello("Alice");
sayHello("Bob");
```

The greet function takes two arguments, greeting and name.
The partial function is used to create a new function sayHello where the first argument is pre-filled with "Hello".
When you call sayHello("Alice"), it's equivalent to calling greet("Hello", "Alice"), resulting in the output "Hello, Alice!". Similarly, sayHello("Bob") results in "Hello, Bob!".

# Implement a function map that takes an array and a callback function, and returns a new array with the result of applying the callback to each element.

```javascript
function map(array, callback) {
    const mappedArray = [];
    for (let i = 0; i < array.length; i++) {
        const result = callback(array[i]);
        mappedArray.push(result);
    }
    return mappedArray;
}
function square(num) {
    return num * num;
}

const numbers = [1, 2, 3, 4, 5];

const squaredNumbers = map(numbers, square);

console.log(squaredNumbers); // Output: [1, 4, 9, 16, 25]

```

In this implementation:

array is the input array you want to apply the callback to.
callback is the function that will be applied to each element in the array.
The map function iterates through each element in the array and applies the callback to it.
The result of applying the callback is then added to the mappedArray.
The mappedArray containing the results of applying the callback to each element is returned.

# Write a memoization function that caches the results of expensive calculations to improve performance

```javascript
function memoize(func) {
    const cache = new Map();
    return function(...args) {
        const key = JSON.stringify(args);
        if (cache.has(key)) {
            return cache.get(key);
        }
        const result = func(...args);
        cache.set(key, result);
        return result;
    };
}

function fibonacci(n) {
    if (n <= 1) {
        return n;
    }
    return fibonacci(n - 1) + fibonacci(n - 2);
}

const memoizedFibonacci = memoize(fibonacci);

console.time("Memoized");
console.log("before cache ",fibonacci(104)); 
console.timeEnd("Memoized");

console.time("Memoized");
console.log(memoizedFibonacci(104)); 
console.timeEnd("Memoized");

console.time("Original");
console.log("after cache ",fibonacci(104)); 
console.timeEnd("Original");
```

In this example, you'll likely notice a significant difference in execution time between the memoized version and the original version of the Fibonacci calculation, especially for larger values of n. The memoization technique helps avoid recalculating results for the same input, improving performance.

output:
before cache  55
Memoized: 1.6ms
55
Memoized: 1.382ms
after cache  55
Original: 0.433ms

# Write a function that takes an array of objects and sorts them based on a specific property.

```javascript
function sortByProperty(array, property) {
    // return array.sort((a, b) => {
    //     if (a[property] < b[property]) {
    //         return -1;
    //     }
    //     if (a[property] > b[property]) {
    //         return 1;
    //     }
    //     return 0;
    // });

   return array.sort((b,a) => {
     if(b[property]<a[property]){
       return 1;
     }
     if(b[property]>a[property]){
       return -1;
     }
     return 0;
   });
}

// Example array of objects
const people = [
    { name: "John", age: 30 },
    { name: "Alice", age: 25 },
    { name: "Bob", age: 35 },
];

// Sort the array of objects by the "age" property
const sortedPeople = sortByProperty(people, "age");

console.log(sortedPeople);
```
output
[
  { name: 'Bob', age: 35 },
  { name: 'John', age: 30 },
  { name: 'Alice', age: 25 }
]

in this example:

The sortByProperty function takes an array and a property name as its parameters.
It uses the sort method to sort the array of objects based on the specified property.
The comparison function passed to sort compares the values of the specified property (a[property] and b[property]) to determine the sorting order.
You can call sortByProperty with different properties to sort the array of objects by that property. In the example above, the objects are sorted by the "age" property in ascending order.

# Create a function that takes an array and returns a new array with unique values (no duplicates).

```javascript
function uniqueArray(arr) {
    return [...new Set(arr)];
}

// Example array with duplicates
const originalArray = [1, 2, 2, 3, 4, 4, 5];

// Get a new array with unique values
const uniqueValues = uniqueArray(originalArray);

console.log(uniqueValues); // Output: [1, 2, 3, 4, 5]

```

# Create a function that takes an array and returns a new array with unique values (no duplicates).

```javascript
function uniqueArray(arr) {
    return [...new Set(arr)];
}

// Example array with duplicates
const originalArray = [1, 2, 2, 3, 4, 4, 5];

// Get a new array with unique values
const uniqueValues = uniqueArray(originalArray);

console.log(uniqueValues); // Output: [1, 2, 3, 4, 5]
```

The uniqueArray function takes an array arr as its parameter.
It creates a Set from the input array, which automatically removes duplicate values because a Set can only contain unique values.
The Set is then converted back to an array using the spread operator [...new Set(arr)].
The result is a new array with unique values, and it's returned from the function.

# Given an array of objects representing people, implement functions to find the oldest person, filter people by a specific age range, and sort them by name.

```javascript
function findOldestPerson(people) {
    if (people.length === 0) {
        return null; // Return null for an empty array
    }

    return people.reduce((oldest, person) => {
        return person.age > oldest.age ? person : oldest;
    }, people[0]);
}
function filterByAgeRange(people, minAge, maxAge) {
    return people.filter(person => person.age >= minAge && person.age <= maxAge);
}
function sortByName(people) {
    return people.slice().sort((a, b) => {
        return a.name.localeCompare(b.name);
    });
}
const people = [
    { name: "Alice", age: 30 },
    { name: "Bob", age: 25 },
    { name: "Charlie", age: 35 },
    { name: "David", age: 40 }
];

const oldestPerson = findOldestPerson(people);
console.log(oldestPerson); // Output: { name: "David", age: 40 }

const ageRangeFiltered = filterByAgeRange(people, 30, 35);
console.log(ageRangeFiltered); // Output: [{ name: "Alice", age: 30 }, { name: "Charlie", age: 35 }]

const sortedByName = sortByName(people);
console.log(sortedByName);
```

# Write a function that extracts key-value pairs from an object and returns them as an array of arrays.

```javascript
function objectToArray(obj) {
    return Object.entries(obj);
}

// Example object
const person = {
    name: "Alice",
    age: 30,
    city: "New York"
};

const keyValuePairs = objectToArray(person);

console.log(keyValuePairs);

```

In this code:

The objectToArray function takes an object obj as its parameter.
It uses Object.entries(obj) to convert the object's key-value pairs into an array of arrays, where each inner array contains two elements: the key and its corresponding value.
When you call objectToArray(person) with the person object, you'll get the following output:

[
    ["name", "Alice"],
    ["age", 30],
    ["city", "New York"]
]
