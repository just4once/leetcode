### Question {#question}

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

**Example:**

```
Given [100, 4, 200, 1, 3, 2],
The longest consecutive elements sequence is [1, 2, 3, 4]. Return its length: 4.
```

### Thought Process {#thought-process}

1. Sorting
   1. We can compare the element to the previous element. If they are consecutive, we can just increment the counter, otherwise we reset it
   2. Time complexity O\(n log n\)
   3. Space complexity O\(1\)
2. Hash Set
   1. To reduce the time complexity to O\(n\), we have to avoid sorting
   2. Similar to the last idea, we have to build the sequence as long the cur exploring number is one value away from last, we can leverage this idea to build one as long as we can
   3. Now when the set has num - 1, that means we either explored it before or will explore it at the future, we should skip it
   4. Space complexity O\(n\)

### Solution

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums.length < 2) return nums.length;
        int len = 1;
        int cur = 1;
        Arrays.sort(nums);
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i - 1]) continue;
            if (nums[i] == nums[i - 1] + 1) cur++;
            else {
                len = Math.max(cur, len);
                cur = 1;
            }
        }
        return Math.max(cur, len);
    }
}
```

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        if (nums.length < 2) return nums.length;
        Set<Integer> set = new HashSet<>();
        for (int num : nums) {
            set.add(num);
        }
        int max = 0;
        for (int num : nums) {
            if (!set.contains(num - 1)) {
                int cur = 1;
                while (set.contains(++num)) cur++;
                max = Math.max(cur, max);
            }
        }
        return max;
    }
}
```

### Additional {#additional}



