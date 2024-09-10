To determine the efficiency of an [[Algorithm]], we must calculate its complexity, especially when working with large amounts of data. This translates to a question: How long does it take to execute? However, this question does not refer to a unit of time, but to the number of instructions the algorithm requires to execute correctly. The instructions considered for this are: Comparisons, Assignments, Subscript access, Arithmetic operations.
## Complexity variable
We will calculate the complexity in the case of having a lot of data, which means we will have an array or some structure with this data. The "variable" on which we will calculate the complexity is the amount of data, that is, the number of elements in the array. An algorithm works the same way for 4, 5, or n elements, with n being the number of elements it has at the time of execution.
### Example:
Example written in [[JavaScript]]
```js
let values = [4,6,9,10,8]
let sum = 0
for (let i = 0; i < values.length; i++) {
  sum += values[i]
}
```
If we call n the length of the array, we can say that the for loop runs n times, that is, all the instructions it contains will run n times. In this case, we say that the order of complexity is Order n and it is written `O(n)`.
```js
let values = [4,6,9,10,8]
let sum = 0
for (let i = 0; i < values.length; i++) {
  for (let j = 0; j < values.length - 1; j++) {
    if (values[j] < values[j + 1]) {
      // Swap
    }
  }
}
```
In this case, the first for loop runs n times, and for each of those, the second for loop also runs n times, so we have `n+n+n+n = O(n^2)` or Order n squared.
### Rules:
If in an algorithm we find a sequence of `O(n)` complexity instructions, for example, a for loop over an array, and then a nested for loop of `O(n^2)` complexity, we stick with the highest of the two, that is, `O(n^2)`. Nested for loops over the same array multiply, that is, `O(n)*O(n)=O(n^2)`.