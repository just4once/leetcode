### Question {#question}

[https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

Given a sorted array, remove the duplicates [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array **[**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) with O\(1\) extra memory.

**Example:**

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
It doesn't matter what you leave beyond the new length.
```

### Thought Process {#thought-process}

1. Because the question ask we do it in place and return the new length, we have somehow scanning through the array and insert/discard the exploring element
2. This hint inspires the use of two pointers, where one points to the current element and the other points to the correct position that element should be reside

### Solution

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length <= 1) return nums.length;
    int id = 1;
    for (int i = 1; i < nums.length; i++) {
        if (nums[i] != nums[i-1]) {
            nums[id] = nums[i];
            id++;
        }
    }
    return id;
    }
}
```

### Additional {#additional}



