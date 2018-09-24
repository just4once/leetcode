# 169-majority-element

## Question {#question}

[https://leetcode.com/problems/majority-element/description/](https://leetcode.com/problems/majority-element/description/)

Given an array of size n, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋` times.

You may assume that the array is non-empty and the majority element always exist in the array.

**Example 1:**

```text
Input: [3,2,3]
Output: 3
```

**Example 2:**

```text
Input: [2,2,1,1,1,2,2]
Output: 2
```

## Thought Process {#thought-process}

1. Sorting
   1. Time complexity O\(nlogn\)
   2. Space complexity O\(1\)
2. HashMap
   1. Time complexity O\(n\)
   2. Space complexity O\(n\)
3. Divide and Conquer
   1. 
4. Boyer-Moore Voting Algorithm
   1. O\(n\)

## Solution

```java
class Solution {
    public int majorityElement(int[] nums) {
        Arrays.sort(nums);
        return nums[nums.length/2];
    }
}
```

```java
class Solution {
    public int majorityElement(int[] nums) {
        int major = 0, count = 0;
        Map<Integer, Integer> map = new HashMap<>();
        for (int num : nums) map.put(num, map.getOrDefault(num, 0) + 1);
        for (int key : map.keySet()) {
            if (map.get(key) > count) {
                count = map.get(key);
                major = key;
            }
        }
        return major;
    }
}
```

```java
class Solution {
    public int majorityElement(int[] nums) {
        return getMajor(nums, 0, nums.length - 1);
    }
    
    private int getMajor(int[] nums, int lo, int hi) {
        if (lo == hi) return nums[lo];
        int mi = lo + (hi - lo) / 2;
        int left = getMajor(nums, lo, mi);
        int right = getMajor(nums, mi + 1, hi);
        if (left == right) return left;
        int leftCount = countInRange(nums, left, lo, mi);
        int rightCount = countInRange(nums, right, mi + 1, hi);
        return leftCount > rightCount ? left : right;
    }
    
    private int countInRange(int[] nums, int target, int lo, int hi) {
        int count = 0;
        for (int i = lo; i <= hi; i++) {
            if (nums[i] == target) count++;
        }
        return count;
    }
}
```

```java
class Solution {
    public int majorityElement(int[] nums) {
        int major = 0, count = 0;
        for (int i = 0; i < nums.length; i++) {
            if (count == 0) major = nums[i];
            if (major == nums[i]) count++;
            else count--;
        }
        return major;
    }
}
```

## Additional {#additional}

