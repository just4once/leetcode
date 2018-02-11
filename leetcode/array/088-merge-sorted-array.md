### Question {#question}

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

**Note:**

You may assume that nums1 has enough space \(size that is greater or equal to m + n\) to hold additional elements from nums2. The number of elements initialized in nums1 and nums2 are m and n respectively.

**Example:**

```

```

### Thought Process {#thought-process}

1. Since array nums1 has enough space, we can put the the element directly into nums1
2. We can either start from beginning or the end
3. Starting from the end is better because we don't have tor swift the element
4. We can use two pointers to track the last index we fill while comparing these two arrays
5. Time complexity O\(n\)
6. Space complexity O\(1\)

### Solution

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int len = m + n;
        while (n > 0) {
            if (m > 0 && nums1[m - 1] > nums2[n - 1]) nums1[--len] = nums1[--m];
            else nums1[--len] = nums2[--n];
        }
    }
}
```

### Additional {#additional}



