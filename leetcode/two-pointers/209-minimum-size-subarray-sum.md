### Question {#question}

[https://leetcode.com/problems/minimum-size-subarray-sum/description/](https://leetcode.com/problems/minimum-size-subarray-sum/description/)

Given an array of n positive integers and a positive integer s, find the minimal length of a contiguous subarray of which the sum ≥ s. If there isn't one, return 0 instead.

**Example:**

```
Given the array [2,3,1,2,4,3] and s = 7,
the subarray [4,3] has the minimal length under the problem constraint.
```

### Thought Process {#thought-process}

1. Presum and Binary Search
   1. We do partial sum on the array ending at that element
   2. Then we do binary search on sum\[i\] + s in the range between i and the n - 1
   3. Time complexity O\(n logn\)
   4. Space complexity O\(n\)
2. Two Pointers and Running Sum
   1. Use two pointers to keep track the range of sum to add up to target
   2. Once the target is reach, we can get the length of range, and also deduct the beginning to start a new sequence
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        int n = nums.length;
        if (n == 0) return 0;
        int[] sums = new int[n];
        sums[0] = nums[0];
        for (int i = 1; i < n; i++) {
            sums[i] = sums[i - 1] + nums[i];
        }
        if (sums[n - 1] < s) return 0;
        int min = n;
        for (int i = 0; i < n; i++) {
            if (sums[i] >= s) {
                int j = lowerBound(sums, 0, i, sums[i] - s);
                min = Math.min(min, i - j);
            }
        }
        return min;
    }
    
    public int lowerBound(int[] a, int lo, int hi, int target) {
        while (lo <= hi) {
			int mid = lo + (hi - lo) / 2;
			if (a[mid] == target) return mid;
			else if (a[mid] < target) lo = mid + 1;
			else hi = mid - 1;
		}
		return hi;
    }
}
```

```java
class Solution {
    public int minSubArrayLen(int s, int[] nums) {
        int sum = 0, min = Integer.MAX_VALUE;
        int i = 0, j = 0;
        while (j < nums.length) {
            sum += nums[j++];
            while (sum >= s) {
                min = Math.min(min, j - i);
                sum -= nums[i++];
            }
        }
        if (min == Integer.MAX_VALUE) min = 0;
        return min;
    }
}
```

### Additional {#additional}



