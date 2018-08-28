# 283-move-zeroes

## Question {#question}

[https://leetcode.com/problems/move-zeroes/description/](https://leetcode.com/problems/move-zeroes/description/)

Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

**Example:**

```text
Given nums = [0, 1, 0, 3, 12], 
after calling your function, 
nums should be [1, 3, 12, 0, 0].
```

## Thought Process {#thought-process}

1. Two Pointers
   1. Use one pointer to keep track the last inserted position
   2. Anther pointer moves forward as we progress the element
   3. Insert the element if it is not equal to 0
   4. Time complexity O\(n\)
   5. Space complexity O\(1\)

## Solution

```java
class Solution {
    public void moveZeroes(int[] nums) {
        int id = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != 0) nums[id++] = nums[i];
        }
        while (id < nums.length) nums[id++] = 0;
    }
}
```

## Additional {#additional}

