### Question {#question}

[https://leetcode.com/problems/contains-duplicate/description/](https://leetcode.com/problems/contains-duplicate/description/)

Given an array of integers, find if the array contains any duplicates. Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

**Example:**

```

```

### Thought Process {#thought-process}

1. Sort
   1. Time complexity O\(n logn\)
   2. Space complexity O\(1\) or O\(n\) depends on if we can temper the original array
2. Hash Table - Set
   1. Time complexity O\(n\)
   2. Space complexity O\(n\)

### Solution

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Arrays.sort(nums);
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i - 1]) return true;
        }
        return false;
    }
}
```

```java
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for (int num : nums){
            if (!set.add(num)) return true;
        }
        return false;
    }
}
```

### Additional {#additional}



