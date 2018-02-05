### Question {#question}

[https://leetcode.com/problems/maximum-subarray/description/](https://leetcode.com/problems/maximum-subarray/description/)

Find the contiguous subarray within an array \(containing at least one number\) which has the largest sum.

**Example:**

```
Given the array [-2,1,-3,4,-1,2,1,-5,4],
the contiguous subarray [4,-1,2,1] has the largest sum = 6.
```

### Thought Process {#thought-process}

1. Typical maximum subarray problem
2. We add the element if it doesn't make the sum negative
3. If the sum goes negative, we reset the sum

### Solution

```java
class Solution {
    public int maxSubArray(int[] nums) {
        if (nums == null || nums.length == 0) return -1;
        int maxSoFar = nums[0];
        int maxCur = nums[0];
        for (int i = 1; i < nums.length; i++) {
            maxCur = Math.max(maxCur + nums[i], nums[i]);
            maxSoFar = Math.max(maxSoFar, maxCur);
        }
        return maxSoFar;
    }
}
```

### Additional {#additional}



