### Question {#question}

[https://leetcode.com/problems/search-a-2d-matrix-ii/description/](https://leetcode.com/problems/search-a-2d-matrix-ii/description/)

Write an efficient algorithm that searches for a value in anmxnmatrix. This matrix has the following properties:

* Integers in each row are sorted in ascending from left to right.
* Integers in each column are sorted in ascending from top to bottom.

**Example:**

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

Given target = 5, return true.

Given target = 20, return false.

### Thought Process {#thought-process}

1. Top Right to Bottom Left
   1. Since the array is sorted ascendingly from left to right and top to bottom, we use the top right to decide where to go
   2. If the target is smaller than the top right \(i,j\), then the target might be on the left of it
   3. If the target is greater than the top right, then the target might be below it

### Solution

```java

```

### Additional {#additional}



