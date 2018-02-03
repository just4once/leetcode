### Question {#question}

[https://leetcode.com/problems/3sum-closest/description/](https://leetcode.com/problems/3sum-closest/description/)

Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

**Example:**

```
For example, given array S = {-1 2 1 -4}, and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

### Thought Process {#thought-process}

1. Very similar to Q015 [https://leetcode.com/problems/3sum/description/](https://leetcode.com/problems/3sum/description/)

### Solution

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        if (nums == null || nums.length < 3) return 0;
		Arrays.sort(nums);
		int sum = 0;
		int closest = nums[0] + nums[1] + nums[2];
		for (int i = 0; i < nums.length - 2; i++) {
			if (i > 1 && nums[i] == nums[i - 1]) continue;
			int lo = i + 1;
			int hi = nums.length - 1;
			while (lo < hi) {
				sum = nums[i] + nums[lo] + nums[hi];
				if (sum == target) {
					return target;
				} else if (sum < target) {
					lo++;
				} else {
					hi--;
				}
				if (Math.abs(sum - target) < Math.abs(closest - target)) closest = sum;
			}

		}
		return closest;
    }
}
```

### Additional {#additional}



