### Question {#question}

[https://leetcode.com/problems/two-sum/description/](https://leetcode.com/problems/two-sum/description/)

Given an array of integers, return **indices **of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly **one solution, and you may not use the same element twice.

**Example:**

```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

### Thought Process {#thought-process}

1. Brute Force
   1. Use every element as an anchor and search its right element
   2. The time complexity is O\(n^2\) = \(n - 1\) + \(n - 2\) + ... + 1
   3. The space complexity is O\(1\)
2. Optimal
   1. Leverage the power of hashmap and store the number and its index in the map
   2. When the map contain target - curNum, we know the search is complete
   3. The time complexity is O\(n\)
   4. The space complexity is O\(n\)

### Solution {#solution}

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        if (nums == null) return null;
        int[] result = new int[2];
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            if (map.containsKey(target - nums[i])) {
                result[0] = map.get(target - nums[i]);
                result[1] = i;
                return result;
            }
            map.put(nums[i], i);
        }
        return result;
    }
}
```

### Additional {#additional}



