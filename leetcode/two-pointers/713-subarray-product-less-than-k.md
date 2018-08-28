# 713-subarray-product-less-than-k

## Question {#question}

[https://leetcode.com/problems/subarray-product-less-than-k/description/](https://leetcode.com/problems/subarray-product-less-than-k/description/)

Your are given an array of positive integers nums.

Count and print the number of \(contiguous\) subarrays where the product of all the elements in the subarray is less than k.

**Example:**

```text
Input: nums = [10, 5, 2, 6], k = 100
Output: 8
Explanation: The 8 subarrays that have product less than 100 are: [10], [5], [2], [6], [10, 5], [5, 2], [2, 6], [5, 2, 6].
Note that [10, 5, 2] is not included as the product of 100 is not strictly less than k.
```

**Note:**

* 0 &lt; nums.length &lt;= 50000.
* 0 &lt; nums\[i\] &lt; 1000.
* 0 &lt;= k &lt; 10^6.

## Thought Process {#thought-process}

1. Two Pointers
   1. Since the multiplication will not overflow, we can use one variable to store the product
   2. We multiply the current number and adjust the left pointer until we have product smaller than k
   3. Then the number of product less than k is equal to current - left + 1
   4. Time complexity O\(n\)
   5. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int numSubarrayProductLessThanK(int[] nums, int k) {
        if (k <= 1) return 0;
        int prod = 1;
        int count = 0, left = 0;
        for (int i = 0; i < nums.length; i++) {
            prod *= nums[i];
            while (prod >= k) prod /= nums[left++];
            count += i - left + 1;
        }
        return count;
    }
}
```

## Additional {#additional}

