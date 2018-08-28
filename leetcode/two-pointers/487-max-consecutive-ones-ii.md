# 487-max-consecutive-ones-ii

## Question {#question}

[https://leetcode.com/problems/max-consecutive-ones-ii/description/](https://leetcode.com/problems/max-consecutive-ones-ii/description/)

Given a binary array, find the maximum number of consecutive 1s in this array if you can flip at most one 0.

**Example:**

```text
Input: [1,0,1,1,0]
Output: 4

Explanation: Flip the first zero will get the the maximum number of consecutive 1s.
After flipping, the maximum number of consecutive 1s is 4.
```

**Note:**

The input array will only contain 0 and 1.

The length of input array is a positive integer and will not exceed 10,000

**Follow up:**

What if the input numbers come in one by one as an **infinite stream**?

In other words, you can't store all numbers coming from the stream as it's too large to hold in memory. Could you solve it efficiently?

## Thought Process {#thought-process}

1. Two Pointers
   1. We use one pointer to move though the elements. and another for the last zero
   2. When we encounter a 1, we just keep increasing the length
   3. When we encounter a 0, we deduct the last position of zero to get the length of sequence 1's ending with current 0
   4. Time complexity O\(n\)
   5. Space complexity O\(1\)
2. Two Pointers
   1. We can save the unnecessary use of math.max by doing it when num is 0
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int lastZero = -1, len = 0, cur = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 1) {
                cur++;
            } else {
                cur = i - lastZero;
                lastZero = i;
            }
            len = Math.max(cur, len);
        }
        return len;
    }
}
```

```java
class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int len = 0, pre = 0, cur = 0;
        boolean zero = false;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 1) {
                cur++;
            } else {
                zero = true;
                len = Math.max(len, pre + 1 + cur);
                pre = cur;
                cur = 0;
            }
        }
        return Math.max(len, zero? pre + 1 + cur : cur);
    }
}
```

## Additional {#additional}

