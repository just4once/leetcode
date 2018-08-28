# 027-remove-element

## Question {#question}

[https://leetcode.com/problems/remove-element/description/](https://leetcode.com/problems/remove-element/description/)

Given an array and a value, remove all instances of that value [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) and return the new length.

Do not allocate extra space for another array, you must do this by **modifying the input array** [**in-place**](https://en.wikipedia.org/wiki/In-place_algorithm) with O\(1\) extra memory.

The order of elements can be changed. It doesn't matter what you leave beyond the new length.

**Example:**

```text
Given nums = [3,2,2,3], val = 3,

Your function should return length = 2, with the first two elements of nums being 2.
```

## Thought Process {#thought-process}

1. Since we have to move non-targeted value to the front and target value to the back, we need two pointers.
2. One pointer track the location of non-targeted value from forward. T
3. The other points to the location of at the end where we can insert the target value. 
4. Time complexity O\(n\)
5. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int id = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] != val) {
                nums[id++] = nums[i];
            }
        }
        return id;
    }
}
```

## Additional {#additional}

