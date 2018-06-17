### Question {#question}

[https://leetcode.com/problems/maximum-average-subarray-ii/description/](https://leetcode.com/problems/maximum-average-subarray-ii/description/)

Given an array consisting of n integers, find the contiguous subarray whose length is greater than or equal to k that has the maximum average value. And you need to output the maximum average value.

**Example:**

```
Input: [1,12,-5,-6,50,3], k = 4
Output: 12.75
Explanation:
when length is 5, maximum average value is 10.8,
when length is 6, maximum average value is 9.16667.
Thus return 12.75.
```

**Note:      
**

1. 1 &lt;= k &lt;= n &lt;= 10,000.
2. Elements of the given array will be in range \[-10,000, 10,000\].
3. The answer with the calculation error less than 10-5 will be accepted.

### Thought Process {#thought-process}

1. Presum and Linear Scan \(TLE\)
   1. Create a presum array and start searching the left pointer from 0th to n - kth element
   2. We have another pointer points at the left + k, and continues increasing until we hit the end
   3. We then can calculate the average pretty easily using the \(presum\[right\] - presum\[left\]\) / \(right - left\)
   4. Time complexity O\(n^2\)
   5. Space complexity O\(n\)
2. Binary Search
   1. We find the min and max of the numbers and then perform binary search within this range
   2. We then check our nums array to see if there is a continuous subarray with at least length k that has average greater than mid
   3. If that is the case, we know our average is at least mid, so we set our min to mid
   4. Otherwise, we set our max to mid
   5. We build a valid function to check if the nums array has the subarray
      1. We first accumulate the first k items difference with target, if the sum is greater than 0, we can return true
      2. Otherwise, we need to see if the remaining elements' difference can form a sum greater than min sum \(k elements before or min prev sum encountered so far\)
   6. Time complexity O\(nlog\(max-min\)\)
   7. Space complexity O\(1\)
3. Convex Hull Window
   1. We create presum array to help calculate average in O\(1\) time
   2. For every sequence ending with index j, we try to find an index i where the average before i is less than average before j
   3. We investigate i from \[0, j - k

### Solution

```java
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int n = nums.length;
        double maxAvg = Double.NEGATIVE_INFINITY;
        for (int i = 0; i <= n - k; i++) {
            double sum = 0;
            int c = 0;
            while (c < k - 1) {
                sum += nums[i + c];
                c++;
            }
            while (i + c < n) {
                sum += nums[i + c];
                c++;
                maxAvg = Math.max(maxAvg, sum / c);
            }
        }
        return maxAvg;
    }
}
```

```java
class Solution {
    public double findMaxAverage(int[] nums, int k) {
        int n = nums.length;
        int nmin = Integer.MAX_VALUE, nmax = Integer.MIN_VALUE;
        for (int num : nums) {
            nmin = Math.min(nmin, num);
            nmax = Math.max(nmax, num);
        }
        double min = nmin, max = nmax;
        double epsilon = 0.00001, error = 1;
        while (max - min > epsilon) {
            double mid = min + (max - min) / 2;
            if (valid(nums, mid, k)) min = mid;
            else max = mid;
        }
        return min;
    }

    private boolean valid(int[] nums, double target, int k) {
        int i = 0;
        double sum = 0;
        while (i < k) {
            sum += nums[i++] - target;
        }
        if (sum >= 0) return true;
        double prev = 0, min = 0;
        while (i < nums.length) {
            sum += nums[i] - target;
            prev += nums[i - k] - target;
            i++;
            min = Math.min(min, prev);
            if (sum >= min) return true;
        }
        return false;
    }
}
```

### Additional {#additional}



