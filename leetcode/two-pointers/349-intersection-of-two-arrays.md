### Question {#question}

[https://leetcode.com/problems/intersection-of-two-arrays/description/](https://leetcode.com/problems/intersection-of-two-arrays/description/)

Given two arrays, write a function to compute their intersection.

**Example:**

```
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2].
```

### Thought Process {#thought-process}

1. Hash Table
   1. Use hash table to store the number, then visit the nums2
   2. Add the number from nums2 to the result when we have seen this number before in nums1
   3. Time complexity O\(m + n\)
   4. Space complexity O\(m\) or O\(min\(m, n\)\)
2. Two Pointers
   1. We sort the array, and use two pointers to track the two num arrays
   2. If the num is smaller in one num array we move the pointer
   3. Time complexity O\(nlogn\)
   4. Space complexity O\(1\)

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

```java
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int i = 0, j = 0;
        Set<Integer> set = new HashSet<>();
        while (i < nums1.length && j < nums2.length) {
            if (nums1[i] < nums2[j]) {
                i++;
            } else if (nums1[i] > nums2[j]) {
                j++;
            } else {
                set.add(nums1[i]);
                i++;
                j++;
            }
        }
        int[] res = new int[set.size()];
        int k = 0;
        for (int num : set) {
            res[k++] = num;
        }
        return res;
    }
}
```

### Additional {#additional}



