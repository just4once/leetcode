# 167-two-sum-ii-input-array-is-sorted

## Question {#question}

[https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)

Given an array of integers that is already **sorted in ascending order**, find two numbers such that they add up to a specific target number.

The function twoSum should return indices of the two numbers such that they add up to the target, where index1 must be less than index2. Please note that your returned answers \(both index1 and index2\) are not zero-based.

You may assume that each input would have exactly one solution and you may not use the same element twice.

**Example:**

```text
Input: numbers={2, 7, 11, 15}, target=9
Output: index1=1, index2=2
```

## Thought Process {#thought-process}

1. Two Pointers
   1. Using two pointers to track the start and end of array
   2. Adjust the start and end pointers accordingly by comparing their sum and the target
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int[] twoSum(int[] numbers, int target) {
        int lo = 0, hi = numbers.length - 1;
        int[] indices = new int[2];
        while (lo < hi){
            int sum = numbers[lo] + numbers[hi];
            if (sum < target){
                lo++;
            } else if (sum > target){
                hi--;
            } else {
                indices[0] = lo + 1;
                indices[1] = hi + 1;
                break;
            }
        }
        return indices;
    }
}
```

## Additional {#additional}

