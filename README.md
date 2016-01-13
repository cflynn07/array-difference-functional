array-subtract-functional-compare
=================================

Compute the difference between two arrays with an optional custom equality comparison method.

Inspired by Ruby's built in Array Difference: [Ruby Docs: Array-Difference][0]

`array-subtract-functional-compare` is slightly different from the NPM package
[array-difference][1]. This module will subtract one array from another array, and return a new
array with a unique subset of the values in the first array. `array-difference` computes the
[symmetric difference][2] (XOR) of two arrays.

Symmetric Difference vs Array Subtraction
-----------------------------------------
```
A: [1, 2, 3, 4, 5]
B: [3, 4, 5, 6, 7]

Symmetric difference: A XOR B = [1, 2, 6, 7]
Array subtraction A - B = [1, 2]
```

```js
// In Ruby the subtraction operator is overloaded to work with arrays
[1, 1, 1, 2, 2, 2, 3, 3, 3, 4, 4, 4, 5, 5, 5] - [2, 3, 4]
// => [1, 5]

// Equivalent operation in JavaScript using array-subtract
var Subtract = require('array-subtract')
var subtract = new Subtract({
  comparator: (a, b) => { return a === b }
})
subtract.sub([1, 1, 1, 2, 2, 2, 3, 3, 3, 4, 4, 4, 5, 5, 5], [2, 3, 4])
// => [1, 5]
```

Usage
-----
```js
var namesA = [{
  name: 'David'
}, {
  name: 'Jessica'
}, {
  name: 'Sam'
}]

var namesB = [{
  name: 'Sam'
}, {
  name: 'Tim'
}]

var Subtract = require('array-subtract')
var subtract = new Subtract({
  /**
   * @param {*} namesArrayItem
   * @param {Number} namesArrayIndex
   * @param {Number} subtractArgumentsIndex
   */
  accessor: (namesArrayItem, namesArrayIndex, subtractArgumentsIndex) => {
    return namesArrayItem.name
  }
})

// namesA - namesB
var namesC = subtract.sub(namesA, namesB)
// => [{
  name: 'David'
}, {
  name: 'Jessica'
}]
```

[0]: http://ruby-doc.org/core-2.3.0/Array.html#2D-method
[1]: https://www.npmjs.com/package/array-difference
[2]: https://en.wikipedia.org/wiki/Symmetric_difference
