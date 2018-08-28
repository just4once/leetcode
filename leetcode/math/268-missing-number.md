# 268-missing-number

## Question {#question}

[https://leetcode.com/problems/missing-number/description/](https://leetcode.com/problems/missing-number/description/)

Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

**Example:**

```text
Input: [3,0,1]
Output: 2
```

```text
Input: [9,6,4,2,3,5,7,0,1]
Output: 8
```

## Thought Process {#thought-process}

1. Sort
   1. Sort the array, if the number is not equal to i, we know this index is the missing number
   2. Time complexity O\(n logn\)
   3. Space complexity O\(1\)
2. Hash Set
   1. We use hashset to store the number
   2. Time complexity O\(n\)
   3. Space complexity O\(n\)
3. XOR
   1. We can leverage the fact that XOR of same number twice will 0
   2. We XOR all the numbers and the index
   3. The final result is the missing number
   4. Time complexity O\(n\)
   5. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int missingNumber(int[] nums) {
        Arrays.sort(nums);
        int n = nums.length;
        for (int i = 0; i < n; i++) {
            if (nums[i] != i) return i;
        }
        return n;
    }
}
```

```java
class Solution {
    public int missingNumber(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for (int num : nums) {
            set.add(num);
        }
        int n = nums.length;
        for (int i = 0; i < n; i++) {
            if (!set.contains(i)) return i;
        }
        return n;
    }
}
```

```java
class Solution {
    public int missingNumber(int[] nums) {
        int res = nums.length;
        for (int i = 0; i < nums.length; i++) {
            res ^= i ^ nums[i];
        }
        return res;
    }
}
```

## Additional {#additional}

