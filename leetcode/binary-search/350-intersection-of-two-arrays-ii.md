### Question {#question}

[https://leetcode.com/problems/intersection-of-two-arrays-ii/description/](https://leetcode.com/problems/intersection-of-two-arrays-ii/description/)

Given two arrays, write a function to compute their intersection.

**Example:**

```
Given nums1 = [1, 2, 2, 1], nums2 = [2, 2], return [2, 2].
```

**Note:**

* Each element in the result should appear as many times as it shows in both arrays.
* The result can be in any order.

**Follow up:**

* What if the given array is already sorted? How would you optimize your algorithm?
* What if nums1's size is small compared to nums2's size? Which algorithm is better?
* What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?

### Thought Process {#thought-process}

1. Hashtable
   1. Using hashtable, we can record the frequency of numbers
   2. Every time we encounter a number from nums2, we check if we have enough count left
   3. Time complexity O\(m + n\)
   4. Space complexity O\(m\)
2. Two Pointers
   1. After sorting two array, we can use two pointers to find the match
   2. Time complexity O\(mlogm + nlogn\)
   3. Space complexity O\(min\(m, n\)\)
3. Binary Search
   1. If both arrays are sorted, we can use binary search to find the match
   2. We can further reduce the complexity if our binary search return the first match index, because that index can be used as left boundary to find the next element's match
   3. Time complexity O\(logn\)
   4. Space complexity O\(1\)

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

```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        Arrays.sort(nums1);
        Arrays.sort(nums2);
        int left = 0, right = nums2.length;
        List<Integer> list = new ArrayList<>();
        for (int num : nums1) {
            left = binarySearch(nums2, left, right, num);
            if (left >= right) break;
            if (nums2[left] == num) list.add(nums2[left++]);
        }
        int[] res = new int[list.size()];
        for (int k = 0; k < res.length; k++) {
            res[k] = list.get(k);
        }
        return res;
    }
    
    private int binarySearch(int[] nums, int lo, int hi, int target) {
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2;
            if (nums[mid] < target) lo = mid + 1;
            else hi = mid;
        }
        return hi;
    }
}
```

### Additional {#additional}



