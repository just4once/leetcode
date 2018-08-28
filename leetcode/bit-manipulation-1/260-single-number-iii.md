# 260-single-number-iii

## Question {#question}

[https://leetcode.com/problems/single-number-iii/description/](https://leetcode.com/problems/single-number-iii/description/)

Given an array of numbers nums, in which exactly two elements appear only once and all the other elements appear exactly twice. Find the two elements that appear only once.

**Example:**

```text
Given nums = [1, 2, 1, 3, 2, 5], return [3, 5].
```

## Thought Process {#thought-process}

1. XOR
   1. Initialize a variable call mask. after XOR with all the numbers, we have the XOR of target1 and target2 save
   2. To distinguish between target1 and target2, we need to XOR mask with mask - 1, this will unset all the digits except the bit position that target1 and target2 differs
   3. Now, we divide the numbers into two groups based on the that bit position, and XOR the numbers in that group only, we get the result
   4. Time complexity O\(n\)
   5. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int[] singleNumber(int[] nums) {
        int[] result = new int[2];
        int mask = 0;
        for (int num : nums) {
            mask ^= num;
        }
        // get the right most significant bit, i.e. [1,2,1,2,3,5]
        // mask = 6, 00110, -mask = 1..11010, mask & -mask = 0..010
        // becase 3 011 and 5 101 are differs at second bit, we can
        // run the process again and divide them into two groups.
        mask &= -mask;
        for (int num: nums) {
            if ((num & mask) == 0) result[0] ^= num;
            else result[1] ^= num;
        }
        return result;
    }
}
```

## Additional {#additional}

