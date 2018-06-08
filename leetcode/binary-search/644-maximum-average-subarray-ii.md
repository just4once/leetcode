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

**Note:**

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
   5. Time complexity O\(nlog\(max-min\)\)
   6. Space complexity O\(1\)

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

### Additional {#additional}



