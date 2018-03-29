### Question {#question}

[https://leetcode.com/problems/intersection-of-two-arrays-ii/description/](https://leetcode.com/problems/intersection-of-two-arrays-ii/description/)

Given two arrays, write a function to compute their intersection.

**Example:**

```
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2, 2].
```

### Thought Process {#thought-process}

1. Hash Table
   1. Save the count of number into the map
   2. As we loop through the second nums array, we save the repeated number into an array list and decrease the count
   3. Time complexity O\(m + n\)
   4. Space complexity O\(min\(m,n\)\) extra
2. Two Pointers
   1. Sort both array, and similar to , instead of using set we use array list to store the number
   2. Time complexity O\(mlogm + nlogn\)
   3. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int num : nums1) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }
        List<Integer> list = new ArrayList<>();
        for (int num : nums2) {
            if (map.getOrDefault(num, 0) > 0) {
                list.add(num);
                map.put(num, map.get(num) - 1);
            }
        }
        int[] res = new int[list.size()];
        for (int i = 0; i < res.length; i++) {
            res[i] = list.get(i);
        }
        return res;
    }
}
```

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int i = 0, j = 0;
        List<Integer> list = new ArrayList<>();
        while (i < nums1.length && j < nums2.length) {
            if (nums1[i] < nums2[j]) {
                i++;
            } else if (nums1[i] > nums2[j]) {
                j++;
            } else {
                list.add(nums1[i]);
                i++;
                j++;
            }
        }
        int[] res = new int[list.size()];
        for (int k = 0; k < res.length; k++) {
            res[k] = list.get(k);
        }
        return res;
    }
}
```

### Additional {#additional}

What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

* If only nums2 cannot fit in memory, put all elements of nums1 into a HashMap, read chunks of array that fit into the memory, and record the intersections.
* If both nums1 and nums2 are so huge that neither fit into the memory, sort them individually \(external sort\), then read 2 elements from each array at a time in memory, record intersections.



