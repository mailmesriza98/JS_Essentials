# Implement your own version of filter

Implement filter: Create a function filter that takes an array and a predicate function (a function that returns a boolean) and returns a new array containing only the elements that satisfy the predicate.

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
function myFilter(array, predicate): This declares a function named myFilter that takes two arguments: an array and a predicate function. The predicate function is a function that returns a boolean value based on some condition.
const filteredArray = [];: This initializes an empty array called filteredArray, which will store the elements that satisfy the predicate condition.
for (let i = 0; i < array.length; i++) { ... }: This loop iterates through each element of the input array.
if (predicate(array[i])) { ... }: Inside the loop, the predicate function is invoked with three arguments:If the predicate function returns true for the current element, it means the element satisfies the condition. In that case, the element is pushed to the filteredArray.
array[i]: The current element of the array being processed.
return filteredArray;: After the loop is done, the filteredArray containing only the elements that satisfy the predicate is returned.

=========================================================================

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

