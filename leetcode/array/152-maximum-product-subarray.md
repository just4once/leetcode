### Question {#question}

[https://leetcode.com/problems/maximum-product-subarray/description/](https://leetcode.com/problems/maximum-product-subarray/description/)

Find the contiguous subarray within an array \(containing at least one number\) which has the largest product.

**Example:**

```
For example, given the array [2,3,-2,4],
the contiguous subarray [2,3] has the largest product = 6.
```

### Thought Process {#thought-process}

1. Brute Force
   1. Check the max product for every subsequence
   2. Time complexity O\(n^2\)
   3. Space complexity O\(1\)
2. Dynamic Programing
   1. Because there is negative number, we need to keep track of the min product as well for the next negative that turn the sign back to positive
   2. We need to have two dimensional array size of 2 x n for storing both min and max product. We need to compare the previous max and min product to current number, reset it when appropriate
   3. Because we only depends on the previous value, we can reduce the two dimensional array to two variables
   4. Time complexity O\(n\)
   5. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int maxProduct(int[] nums) {
        int r = nums[0];
        // max and min stores the max/min product of subarray that ends with the current number
        for (int i = 1, min = r, max = r; i < nums.length; i++){
            if (nums[i] < 0) {
                int tmp = max;
                max = min;
                min = tmp;
            }
            // the max and min are either previous number times cur or the cur itselft
            max = Math.max(max * nums[i], nums[i]);
            min = Math.min(min * nums[i], nums[i]);
            r = Math.max(r, max);
        }
        return r;
    }
}
```

### Additional {#additional}



