Created: 2024-09-17 17:01
## Family Tree:
1. Computer
2. Frontend Development
3. [[JavaScript]]
-- -
In programming, order is important: Computers are based on numbers, making it very necessary to maintain a mathematical structure. On many occasions, we will need to have our data sorted, especially when there is a lot of it. There are many methods -algorithms- already created to achieve this. The Bubble Sort method is one of the most used.
## Bubble Sort
Computers can only respond yes or no, so it will be necessary to sort one value at a time. We compare two values to decide the correct place for each one. In reality, we do the same if we have to sort a group of elements, for example, people's ages, comparing two at a time, although it may seem like we compare all at once. The Bubble Sort sorting method is based on the idea that "bubbles rise and settle in their place."
### Syntax:
To understand how it works and how it is written, let's assume an array of positive integers. Example written in JavaScript:
```js
let numbers = [6, 5, 1, 2, 4, 3, 8, 7]
```
Generally, this algorithm needs to iterate through all the elements of the array. For this, a `for` loop is used that goes from the first element of the array to the last.
```js
for (let i = 0; i < numbers.length; i++) {}
```
The question this algorithm asks is the following: starting from the first number in the array, ask the next number if it is greater and, if so, swap positions. Otherwise, move to the next number and ask the same question. A first iteration through each number does not guarantee that the numbers will be sorted, so we will have to repeat this process, not only starting from the first element of the array but from all elements except the last one. For this, we will have to use a nested `for` loop within the one we already had.
```js
for (let i = 0; i < numbers.length; i++) {
  for (let j = 0; j < numbers.length - 1; j++) {}
}
```
The last step of the Bubble Sort algorithm tells us to ask a logical question, being in the inner `for` loop: Is the next number in the list greater than the current one (the one corresponding to the index)? If so, swap positions, and repeat this until the end of the array. When finished, move to the second element of the array and repeat the inner `for` loop. And so on.
```js
for (let i = 0; i < numbers.length; i++) {
  for (let j = 0; j < numbers.length - 1; j++) {
    if (numbers[j] > numbers[j + 1]) {
      let aux = numbers[j]
      numbers[j] = numbers[j + 1]
      numbers[j + 1] = aux
    }
  }
}
```
**Note**: an auxiliary variable is used to swap the values of the array elements.
## Binary Search Algorithm
This search algorithm only works on lists sorted in ascending order. Example written in JavaScript.
```js
const binarySearch = (arr, item) => {
  let start = 0;
  let end = arr.length - 1;
  let mid;
  let found;
  
  while (start <= end) {
    mid = Math.floor((start + end) / 2);
    found = arr[mid];
    
    if (found === item) {
      return mid;
    }
    
    if (found > item) {
      end = mid - 1;
    } else {
      start = mid + 1;
    }
  }
  
  return "Element not found";
}
```