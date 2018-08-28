# 325-maximum-size-subarray-sum-equals-k

## Question {#question}

[https://leetcode.com/problems/maximum-size-subarray-sum-equals-k/description/](https://leetcode.com/problems/maximum-size-subarray-sum-equals-k/description/)

Given an arraynumsand a target valuek, find the maximum length of a subarray that sums tok. If there isn't one, return 0 instead.

**Note:**  
The sum of the entirenumsarray is guaranteed to fit within the 32-bit signed integer range.

**Example:**

```text
Given nums = [1, -1, 5, -2, 3], k = 3,
return 4. (because the subarray [1, -1, 5, -2] sums to 3 and is the longest)


Given nums = [-2, -1, 2, 1], k = 1,
return 2. (because the subarray [-1, 2] sums to 1 and is the longest)
```

## Thought Process {#thought-process}

1. Brute Force
   1. Time complexity O\(n^2\)
   2. Space complexity O\(1\)
2. Prefix Sum - Hash Table
   1. To find the sum in O\(1\) time, we need to store the sum in the hash table to save the computation time
   2. Because we also need to find the longest subarray, we need to store the respective index in the table
   3. For every element, we check if we have seen presum - k, which means by deducting that index from cur index, the sum of that range is equal to k
   4. Time complexity O\(n\)
   5. Space complexity O\(n\)

## Solution

```java
class Solution {
    public int maxSubArrayLen(int[] nums, int k) {
        int n = nums.length;
        int max = 0;
        for (int i = 0; i < n; i++) {
            int sum = 0;
            for (int j = i; j < n; j++) {
                sum += nums[j];
                if (sum == k) max = Math.max(j - i + 1, max);
            }
        }
        return max;
    }
}
```

```java
class Solution {
    public int maxSubArrayLen(int[] nums, int k) {
        int n = nums.length;
        int max = 0;
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, -1);
        int presum = 0;
        for (int i = 0; i < n; i++) {
            presum += nums[i];
            if (map.containsKey(presum - k)) max = Math.max(max, i - map.get(presum - k));
            map.putIfAbsent(presum, i);
        }
        return max;
    }
}
```

## Additional {#additional}

