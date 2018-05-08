### Question {#question}

[https://leetcode.com/problems/intersection-of-two-arrays/description/](https://leetcode.com/problems/intersection-of-two-arrays/description/)

Given two arrays, write a function to compute their intersection.

**Example:**

```
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].
```

**Note:**

* Each element in the result must be unique.
* The result can be in any order.

### Thought Process {#thought-process}

1. Set
   1. Using set we can easily store the number we have seen in nums1 and compare with nums2
   2. Time complexity O\(m + n\)
   3. Space complexity O\(m\) or O\(min\(m, n\)\)
2. Binary Search

### Solution

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet<>();
        for (int num : nums1) set.add(num);
        Set<Integer> res = new HashSet<>();
        for (int num : nums2) {
            if (set.contains(num)) res.add(num);
        }
        int[] result = new int[res.size()];
        int i = 0;
        for (int num : res) {
            result[i++] = num;
        }
        return result;
    }
}
```

### Additional {#additional}



