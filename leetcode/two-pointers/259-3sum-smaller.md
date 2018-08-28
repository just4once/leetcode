# 259-3sum-smaller

## Question {#question}

[https://leetcode.com/problems/3sum-smaller/description/](https://leetcode.com/problems/3sum-smaller/description/)

Given an array of n integers nums and a target, find the number of index triplets i, j, k with 0 &lt;= i &lt; j &lt; k &lt; n that satisfy the condition nums\[i\] + nums\[j\] + nums\[k\] &lt; target.

**Example:**

```text
Given nums = [-2, 0, 1, 3], and target = 2.
Return 2. Because there are two triplets which sums are less than 2:

[-2, 0, 1]
[-2, 0, 3]
```

## Thought Process {#thought-process}

1. Brute Force
   1. Triple loop for traversal through all elements
   2. Time complexity O\(n^3\)
   3. Space complexity O\(1\)
2. Sort and Binary Search
   1. First, we sort the number
   2. Then we do a double loop and search the respective end element for the second element
   3. Time complexity O\(n^2 logn\)
   4. Space complexity O\(1\)
3. Two Pointers
   1. As we loop through every element, we initialize the low pointer to be the next element and hi to be the end of element
   2. If we can find the hi element that nums\[i\] + nums\[lo\] + nums\[hi\] &lt; target. we can get the count immediately using hi - lo, since any element in the range can replace hi element
   3. Time complexity O\(n^2\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int threeSumSmaller(int[] nums, int target) {
        int n = nums.length, count = 0;
        for (int i = 0; i < n - 2; i++) {
            for (int j = i + 1; j < n - 1; j++) {
                for (int k = j + 1; k < n; k++) {
                    if (nums[i] + nums[j] + nums[k] < target) count++;
                }
            }
        }
        return count;
    }
}
```

```java
class Solution {
    public int threeSumSmaller(int[] nums, int target) {
        Arrays.sort(nums);
        int n = nums.length, count = 0;
        for (int i = 0; i < n - 2; i++) {
            for (int j = i + 1; j < n - 1; j++) {
                int k = search(nums, j + 1, n - 1, target - nums[i] - nums[j]);
                count += k - j;
            }
        }
        return count;
    }

    private int search(int[] nums, int low, int hi, int target) {
        while (low <= hi) {
            int mid = low + (hi - low) / 2;
            if (nums[mid] < target) low = mid + 1;
            else hi = mid - 1;
        }
        return hi;
    }
}
```

```java
class Solution {
    public int threeSumSmaller(int[] nums, int target) {
        Arrays.sort(nums);
        int n = nums.length, count = 0;
        for (int i = 0; i < n - 2; i++) {
            int lo = i + 1, hi = n - 1;
            while (lo < hi) {
                if (nums[i] + nums[lo] + nums[hi] < target) {
                    count += hi - lo;
                    lo++;
                } else {
                    hi--;
                }
            }
        }
        return count;
    }
}
```

## Additional {#additional}

