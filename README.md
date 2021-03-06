# linearSystemUtility

[![Build Status](https://travis-ci.org/DylanKojiCheslin/linearSystemUtility.svg?branch=master)](https://travis-ci.org/DylanKojiCheslin/linearSystemUtility)  
tools for exploring linear systems

what is a [System of linear equations](https://en.wikipedia.org/wiki/System_of_linear_equations "System_of_linear_equations")

## project specifications

### features
takes a array of integers that conform to the augmented matrix notation
find out if the systems has: no solution, one solution, infinite solutions
if there is one or more solutions then define them for the user

a LinearSystem object.

```javascript
const intObject = [
  [2,3,0,5],
  [0,0,1,20],
  [0,-2,0,5]
]
const theSystem = new LinearSystem(intObject);
```

##find out if the systems has: no solution, one solution, infinite solutions

what is a [solving a linear system](https://en.wikipedia.org/wiki/Augmented_matrix#Solution_of_a_linear_system "solving_a_System_of_linear_equations")

[3 row operations:](https://en.wikipedia.org/wiki/Elementary_matrix#Operations "matrix_Operations")

1. (switch) switch 2 rows positions
2. (scaling) multiply every entry in a row by a non-zero constant
3. (rowReplacement) replace a row with its sum and a multiple of a different row and a non-zero constant


```javascript
const solution = theSystem.solve();
console.log(solution);
```

## API

## instance methods

### new LinearSystem
new LinearSystem( theSystemAugmentedMatrixNotation );

return an instance of LinearSystem

### solve
  yourInstance.solve({verbose:false,reduced:true})

optional parameter object has:
"verbose" bool prints console logs of the details of the solution default false,
"reduced" bool if the solutions should return in reduced echelon form default true

return a description of the systems solution (or lack of one)

_initializePivot
1. the left most non-zero column is the pivot column
2. the top row position of the pivot column is the pivot row

foreach row:
a. _largestAbsoluteMovedToTopOfColumn on the _pivotColumn - largest to top
b. _zeroAllRowsUnderThePevot() - row replacement operations to "zero" all entry under the pivot
c. _pivot.row++, _pivot.column++
3. foreach row:
a. _zeroAllRowsAboveThePivot(), _scalePivotToOne
b. _pivot.row--, _pivot--

### _switch
yourInstance._switch(rowNumberOne, rowNumberTwo)
exchange the location of 2 rows

### _scaling
yourInstance._scaling(rowNumber, scaleNumber)
scales all entries in row by a non-zero number

### _rowReplacement
yourInstance._rowReplacement(rowToBeReplaced, differentRowNumber, scaleNumberForOtherRow)
replaces the row in rowToBeReplaced with the the product of the row in differentRowNumber and scaleNumberForOtherRow

### _zeroAllRowsUnderThePivot
iterate over all entries below the pivot, use _rowReplacementRemover on each

### _zeroAllRowsAboveThePivot
iterate over all entries above the pivot, use _rowReplacementRemover on each

### _rowReplacementRemover()
zeros out the entry using _rowReplacement and the _pivot

### _scalePivotToOne
uses _scaling on the row of _pivot to scale _pivot to 1

### _largestAbsoluteMovedToTopOfColumn(columnNumber, rowsOffSetNumber)
rearranges rows to move the largest absolute value to the top of the column row to the top.
this is sometimes called partial pivoting

## instance properties

### _systemState
the internal storage of the linear systems matrix as an array

### _pivot
the pivot position, a obj with props row/column

### _isEchelonForm
returns a bool indicating if the matrix is in [echelon form](https://en.wikipedia.org/wiki/Row_echelon_form "etchlon_Form")

### _isReducedEchelonForm
returns a bool indicating if the matrix is in [reduced echelon form](https://en.wikipedia.org/wiki/Row_echelon_form#Reduced_row_echelon_form "reduced_echelon_form")

## possible features or research topics

### graph solutions
after solved a nice chart to look at if, low enough number of dimensions

### animation of algorithm behavior
ui element that shows system and animates switching, adding, scaling

### optional parameter bool back-substitution instead of going from echelon to reduced echelon form

### function approximation of this class with less complexity cost or overhead
find cases that are easy examples where skipping one or more steps doesn't affect the solution or an approximation of it

### how do linear systems handle infinite entries
many checks for non-zero numbers in code check like:

```javascript
Math.abs(x) > 0
```
could also be

```javascript
!isNaN(parseFloat(num)) && isFinite(num);
```

not sure how or if linear algebra handle infinite, or how could relate to the js version of infinity

### how neural networks solve linear system
there are many ways, check them out...... If you want me to list resources make an issue
