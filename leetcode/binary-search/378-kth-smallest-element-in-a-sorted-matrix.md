### Question {#question}

[https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/description/](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/description/)

Given anxnmatrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

**Example:**

```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

return 13.
```

### Thought Process {#thought-process}

1. Heap
   1. Using min heap, we can add all the element into heap
   2. Getting kth value is trivial
   3. Time complexity O\(mn + klogk\)
   4. Space complexity O\(mn\)
2. Heap with Tuple
   1. Using tuple class to store the row, column and its value, we can use it to locate the next number
   2. We add the first row value into our heap
   3. As we poll the min element out, we can add its bottom element into our heap, which is next smallest element
   4. After looping for k - 1 time, the peek is our solution
   5. Time complexity O\(n + klogk\)
   6. Space complexity O\(n\)
3. asd

### Solution

```java

```

### Additional {#additional}



