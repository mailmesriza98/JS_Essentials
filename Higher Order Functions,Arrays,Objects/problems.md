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

**Implement your own version of filter**

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
