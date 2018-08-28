# 532-k-diff-pairs-in-an-array

## Question {#question}

[https://leetcode.com/problems/k-diff-pairs-in-an-array/description/](https://leetcode.com/problems/k-diff-pairs-in-an-array/description/)

Given an array of integers and an integer k, you need to find the number of unique k-diff pairs in the array. Here a k-diff pair is defined as an integer pair \(i, j\), where i and j are both numbers in the array and their absolute difference is k.

**Example 1:**

```text
Input: [3, 1, 4, 1, 5], k = 2
Output: 2
Explanation: There are two 2-diff pairs in the array, (1, 3) and (3, 5).
Although we have two 1s in the input, we should only return the number of unique pairs.
```

**Example 2:**

```text
Input:[1, 2, 3, 4, 5], k = 1
Output: 4
Explanation: There are four 1-diff pairs in the array, (1, 2), (2, 3), (3, 4) and (4, 5).
```

**Example 3:**

```text
Input: [1, 3, 1, 5, 4], k = 0
Output: 1
Explanation: There is one 0-diff pair in the array, (1, 1).
```

**Note:**

1. The pairs \(i, j\) and \(j, i\) count as the same pair.
2. The length of the array won't exceed 10,000.
3. All the integers in the given input belong to the range: \[-1e7, 1e7\].

## Thought Process {#thought-process}

1. Hash Table
   1. Store the number and its count in the hash table
   2. For each number we need to look for num + k exist in the hash table, if it does, we increase the count
   3. One thing we need to watch out is that when k = 0, we have to make sure the count is greater than 1
   4. Time compleixty O\(n\)
   5. Space complexity O\(n\)
2. Sort and Two Pointers
   1. 

## Solution

```java
class Solution {
    public int findPairs(int[] nums, int k) {
        if (nums == null || nums.length == 0 || k < 0)   return 0;
        Map<Integer, Integer> map = new HashMap<>();
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        int pair = 0, count = k == 0 ? 1 : 0;
        for (int key : map.keySet()) {
            if (map.getOrDefault(key + k, 0) > count) pair++;
        }
        return pair;
    }
}
```

```java
class Solution {
    public int findPairs(int[] nums, int k) {
        if (nums == null || nums.length == 0 || k < 0) return 0;
        Arrays.sort(nums);
        int pair = 0;
        int i = 0, j = 1;
        while (j < nums.length) {
            int diff = nums[j] - nums[i];
            // the right element is too small and i and j cannot be same element
            if (j <= i || diff < k) j++;
            // the left element is too small
            else if ((i > 0 && nums[i] == nums[i - 1]) || diff > k) i++;
            else {
                pair++;
                i++;
            }
        }
        return pair;
    }
}
```

## Additional {#additional}

