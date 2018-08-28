# 080-remove-duplicates-from-sorted-array-ii

## Question {#question}

[https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/description/](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/description/)

Follow up for "Remove Duplicates":

What if duplicates are allowed at most twice?

**Example:**

```text
Given sorted array nums = [1,1,1,2,2,3],
Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3. It doesn't matter what you leave beyond the new length.
```

## Thought Process {#thought-process}

1. Unlike [026-Remove Duplicates from Sorted Array ](026-remove-duplicates-from-sorted-array.md)where duplicates aren't allowed, this question allow to have 2 duplicates
2. We simply compare current ith element with the i - 2 element
   1. We can have two pointers, one going forward and one keep track of last inserted index
   2. We increment the last inserted index when the element is different, so we insert it directly to the array
3. Time complexity O\(n\)
4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums == null) return 0;
        if (nums.length < 3) return nums.length;
        int k = 2, id = 2;
        for (int i = 2; i < nums.length; i++) {
            if (nums[i] != nums[id - 2]) {
                nums[id] = nums[i];
                id++;
            }
        }
        return id;
    }
}
```

## Additional {#additional}

