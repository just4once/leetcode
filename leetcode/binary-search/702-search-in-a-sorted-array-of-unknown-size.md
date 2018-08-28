# 702-search-in-a-sorted-array-of-unknown-size

## Question {#question}

[https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size/description/](https://leetcode.com/problems/search-in-a-sorted-array-of-unknown-size/description/)

Given an integer array sorted in ascending order, write a function to search`target`in`nums`. If`target`exists, then return its index, otherwise return`-1`.**However, the array size is unknown to you**. You may only access the array using an`ArrayReader` interface, where `ArrayReader.get(k)`returns the element of the array at index`k` \(0-indexed\).

You may assume all integers in the array are less than `10000`, and if you access the array out of bounds,`ArrayReader.get`will return`2147483647`.

**Example 1:**

```text
Input: array = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```

**Example 2:**

```text
Input: array = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```

**Note:**    


1. You may assume that all elements in the array are unique.
2. The value of each element in the array will be in the range \[-9999, 9999\].

## Thought Process {#thought-process}

1. Binary Search
   1. We set our search index to be from 0 to 2147483647, named lo and hi
   2. Our search ends when we hit our target or hi &gt; lo
   3. Time complexity O\(1\) from 32 times or search
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int search(ArrayReader reader, int target) {
        int lo = 0, hi = Integer.MAX_VALUE;
        while (lo <= hi) {
            int mi = lo + (hi - lo) / 2;
            int val = reader.get(mi);
            if (val == target) return mi;
            else if (val < target) lo = mi + 1;
            else hi = mi - 1;
        }
        return -1;
    }
}
```

## Additional {#additional}

