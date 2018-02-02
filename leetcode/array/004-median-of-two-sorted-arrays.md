### Question {#question}

[https://leetcode.com/problems/median-of-two-sorted-arrays/description/](https://leetcode.com/problems/median-of-two-sorted-arrays/description/)

There are two sorted arrays **nums1 **and **nums2 **of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O\(log \(m+n\)\).

**Example 1:**

```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```

**Example 2:**

```
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

### Thought Process {#thought-process}

1. Brute Force
   1. Knowing the length of both array, we can use a counter to count the element until it reach n/2 for odd number or n/2 + 1, and taking average for the second case
   2. Time complexity will be O\(m+ n\)
   3. Space complexity will be O\(1\)
2. Optimal \(Binary Search\)
   1. Because the question warrants O\(log\(m+n\)\), binary search is probably the desired approach
   2. Looking back at the definition of median of an array, it's located in the middle
   3. If we can divide these two arrays into left part and right part, where all the elements on left are all smaller than the right's, we have found our solution

### Solution

```java

```

### Additional {#additional}



