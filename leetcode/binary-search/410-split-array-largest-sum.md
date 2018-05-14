### Question {#question}

[https://leetcode.com/problems/split-array-largest-sum/description/](https://leetcode.com/problems/split-array-largest-sum/description/)

Given an array which consists of non-negative integers and an integerm, you can split the array intomnon-empty continuous subarrays. Write an algorithm to minimize the largest sum among thesemsubarrays.

**Note:**  
Ifnis the length of array, assume the following constraints are satisfied:

* 1 ≤ n ≤ 1000
* 1 ≤ m ≤ min\(50, n\)

**Example:**

```
Input:
nums = [7,2,5,10,8]
m = 2

Output:
18

Explanation:
There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8],
where the largest sum among the two subarrays is only 18.
```

### Thought Process {#thought-process}

1. Brute Force
   1. 
2. sad

### Solution

```java
class Solution {
    private int res = Integer.MAX_VALUE;
    public int splitArray(int[] nums, int m) {
        dfs(nums, m, 0, 0, 0, 0);
        return res;
    }
    
    private void dfs(int[] nums, int m, int i, int j, int cur, int max) {
        if (i == nums.length && j == m) {
            res = Math.min(max, res);
            return;
        }
        if (i == nums.length) return;
        if (i > 0) dfs(nums, m, i + 1, j, cur + nums[i], Math.max(max, cur + nums[i]));
        if (j < m) dfs(nums, m, i + 1, j + 1, nums[i], Math.max(max, nums[i]));
    }
}
```

### Additional {#additional}



