### Question {#question}

[https://leetcode.com/problems/find-k-closest-elements/description/](https://leetcode.com/problems/find-k-closest-elements/description/)

Given a sorted array, two integers k and x, find the k closest elements to x in the array. The result should also be sorted in ascending order. If there is a tie, the smaller elements are always preferred.

**Example 1:**

```
Input: [1,2,3,4,5], k=4, x=3
Output: [1,2,3,4]
```

**Example 2:**

```
Input: [1,2,3,4,5], k=4, x=-1
Output: [1,2,3,4]
```

**Note:**

1. The value k is positive and will always be smaller than the length of the sorted array.
2. Length of the given array is positive and will not exceed 104
3. Absolute value of elements in the array and x will not exceed 104

### Thought Process {#thought-process}

1. Binary Search and Expand Window
   1. Locate the closest element using modified binary search
   2. Scan left and right to find the window of length k, where it contains the closest elements to x
   3. Time complexity O\(nlogn\)
2. asd

### Solution

```java

```

### Additional {#additional}



