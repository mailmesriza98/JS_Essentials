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

=========================================================================

# Implement composition of functions

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

In this simplified version of compose, we iterate through the array of functions in reverse order and directly apply each function to the value x, updating x with the result of each function application. 

================================================================================
# Implement your own version of foreach

Problem statement: 
Write your own version of the forEach function, which iterates over an array and applies a function to each element.



const numbers = [1, 2, 3, 4, 5];

function printSquare(num) {
  console.log(num * num);
}

function doublePrint(num) {
  console.log(num * 2);
}

myForEach(numbers, printSquare); 
myForEach(numbers, doubleAndPrint); 


Now lets see what the myForEach function does:


function myForEach(array,callback){

  for(let i=0;i<array.length;i++){
      callback(array[i]);
   }

}

So here the myForEach function essentially loops through all the elements of the array and calls the function as per the initial call of foreach

so if myForEach(numbers,printSquare) is called.: the line inside the for loop calls the printSquare function with the element at a particular index of nums array.

# Implement your own version of Reduce

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

====================================================================================================

# Given an array of strings, use the map function to transform each string to uppercase and return the modified array.

const inputArray = ["hello", "world", "example", "strings"];

const uppercaseArray = inputArray.map(str => str.toUpperCase());

console.log(uppercaseArray);

==================================================================================================

# Use the reduce function to calculate the sum of all numbers in an array.

const arr = [1,2,3,4,5]
const sum = arr,reduce((sum,cur)=>{
  return sum+cur;
},0)

console.log(sum); // Output: 15 (1 + 2 + 3 + 4 + 5)

In this example, the reduce function is used to iterate over each number in the numbers array. The accumulator starts with an initial value of 0, and for each number, it accumulates the sum by adding the currentValue to it. The final sum is stored in the sum variable and printed to the console

=================================================================================================

# Write a function that finds the maximum value in an array using the reduce function.

function findMaxValue(array) {
    if(array.length===0) return undefined
    return arr.reduce((max,cur)={return max>cur?max:cur},array[0])
}

const numbers = [3, 8, 2, 10, 5];

const maxValue = findMaxValue(numbers);

console.log(maxValue); // Output: 10 (maximum value in the array)
In this function:

We first check if the array is empty, in which case we return undefined.
The reduce function iterates over the array. For each element, it compares the currentValue with the current max value. If the currentValue is greater, it becomes the new max value; otherwise, the max value remains the same.
The initial value of max is set to the first element of the array (array[0]).
The final result is the maximum value in the array, which is then stored in the maxValue variable and printed to the console.

=================================================================================================

# Chaining higher order functions

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

====================================================================================================

# Function decorators:
Create a higher-order function repeat that takes a function and a number n, and returns a new function that calls the original function n times.

function repeat(fn,n){
      return function(...args){
        for(let i=0;i<n;i++){ 
                  fn(...args);
        }
     }
}


Certainly! Here's how you can create the repeat higher-order function in JavaScript:

javascript
Copy code
function repeat(fn, n) {
    return function(...args) {
        for (let i = 0; i < n; i++) {
            fn(...args);
        }
    };
}
In this function:

fn is the function you want to repeat.
n is the number of times you want to call the function.
The returned function uses the rest parameter ...args to capture any arguments that are passed to it.
Inside the returned function, a loop is used to call the original function n times, passing along any arguments.

example of the above

function greet(name) {
    console.log(`Hello, ${name}!`);
}

const repeatedGreet = repeat(greet, 3);
repeatedGreet("Alice");  // Output: Hello, Alice!
                         //         Hello, Alice!
                         //         Hello, Alice!
In this example, the repeat function is used to create a new function repeatedGreet that will call the greet function 3 times. When you call repeatedGreet("Alice"), it calls greet("Alice") three times, printing the greeting three times

==================================================================================================

# Currying

 Currying is a technique in functional programming where a function that takes multiple arguments is transformed into a series of functions that each take a single argument. The curried function returns new functions that, when called with arguments, progressively accumulate and process those arguments until all the required arguments are supplied, at which point the original function is executed and the result is returned.

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

the curry function takes a binary function (a function that takes two arguments) and returns a curried version of it. The returned curried function takes arguments one at a time and returns new functions until all the required arguments are gathered.

Here's a step-by-step breakdown:

The curry function takes a binary function, like add.
When you call curriedAdd(5), it returns a new function that takes one argument.
When you call the returned function with an argument, like add5(3), it applies the original binary function (add) to the accumulated arguments (5 and 3) and returns the result.
In this way, currying allows you to break down the process of applying a function with multiple arguments into a sequence of single-argument function calls. This can make code more modular and flexible, especially in functional programming contexts.

=====================================================================================================

# Write a function that flattens a nested array using reduce.

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


The flattenArray function takes an array as input and uses reduce to process each element.
If the current element is an array, it recursively calls flattenArray to further flatten it.
Otherwise, it directly adds the current element to the flatArray.
The initial value of the accumulator (flatArray) is an empty array ([]).
The resulting flattenedArray contains all the elements from the nested array flattened into a single-level array.

========================================================================================================

# Create a function partial that takes a function and some arguments, and returns a new function with those arguments pre-filled.

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

The greet function takes two arguments, greeting and name.
The partial function is used to create a new function sayHello where the first argument is pre-filled with "Hello".
When you call sayHello("Alice"), it's equivalent to calling greet("Hello", "Alice"), resulting in the output "Hello, Alice!". Similarly, sayHello("Bob") results in "Hello, Bob!".

=============================================================================================================
