Created: 2024-09-17 15:44
## Family Tree:
1. Computer
2. Frontend Development
3. [[JavaScript]]
-- -
The simple concept of a matrix is that it is an array that holds other arrays. The complicated concept, on the other hand, is that it is a data structure that stores data in a two-dimensional form. They offer a complex but scalable structure for storing information. We can find them in applications that need to maintain cross-referenced information but within the same context, from search algorithms (Algorithm), electronic circuits, or image processing.
All following code is written in JavaScript, though most language support this data structure.
### Accessing information:
```js
const matrix = [
  [10, 15, 17], // Row 0
  [19, 25, 32]  // Row 1
];
let age25 = matrix[1][1]; // Row 1 Column 1
```
### Traversing a matrix:
When we traverse a matrix, we have 4 possible ways to do it. We can traverse only a row, only a column, traverse by rows, or traverse by columns.
```js
const matrix = [
  [1, 3, 5, 7],
  [0, 2, 4, 6],
  [8, 9, 10, 11]
];
```
#### Traverse a row:
We need to determine which row we want to traverse. For example, row 1. We traverse the elements of the chosen row. With `matrix[1].length`, we "measure" the number of elements in the row.
```js
for (let i = 0; i < matrix[1].length; i++) {
  console.log(matrix[1][i]);
}
// We get 0, 2, 4, 6
```
#### Traverse a column:
Now we determine the column we want to traverse, for example, column 2. We traverse the elements of the chosen column. With `matrix.length`, we "measure" the number of elements in the column, which would be the number of rows in the matrix.
```js
for (let i = 0; i < matrix.length; i++) {
  console.log(matrix[i][2]);
}
// We get 5, 4, 10
```
#### Traverse by rows:
We can traverse the entire matrix by first traversing row 0, then row 1, and so on until all rows are finished.
```js
for (let row = 0; row < matrix.length; row++) {
  for (let column = 0; column < matrix[row].length; column++) {
    console.log(matrix[row][column]);
  }
}
```
The first `for` loop traverses by rows, that is, it starts with row 0 and when positioned in this row, the other `for` loop traverses all the elements of this row. When the second `for` loop finishes its traversal, the first `for` loop moves to the second row. This repeats until all rows are finished.
#### Traverse by columns:
Now we are going to traverse the entire matrix, first traversing column 0, then column 1, and so on until all columns are finished.
```js
for (let column = 0; column < matrix[0].length; column++) {
  for (let row = 0; row < matrix.length; row++) {
    console.log(matrix[row][column]);
  }
}
```
The first `for` loop traverses by columns, that is, it starts with column 0 and when positioned in this column, the other `for` loop traverses all the elements of this column. When the second `for` loop finishes its traversal, the first `for` loop moves to the second column. This repeats until all columns are finished.