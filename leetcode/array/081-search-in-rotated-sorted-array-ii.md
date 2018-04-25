### Question {#question}

[https://leetcode.com/problems/search-in-rotated-sorted-array-ii/description/](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/description/)

Follow up for "[033-Search in Rotated Sorted Array](/leetcode/array/033-search-in-rotated-sorted-array.md)":  
What ifduplicatesare allowed?

Would this affect the run-time complexity? How and why?

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

\(i.e.,`0 1 2 4 5 6 7`might become`4 5 6 7 0 1 2`\).

Write a function to determine if a given target is in the array.

The array may contain duplicates.

**Example:**

```

```

### Thought Process {#thought-process}

1. Similar to [033-Search in Rotated Sorted Array](/leetcode/array/033-search-in-rotated-sorted-array.md), we need two pointers to search, and we also divide the search into different cases
   1. The mid is the target, we can return immediately
   2. The left part is sorted, we then check whether the target is within the range of left and proceed to the correct side
   3. The right part is sorted, and we perform similar step as above
   4. Lastly, when left, middle and right are the same, we can really decide to search which part, we just increment the lo pointer
   5. Time complexity O\(n\) worst, O\(log n\) average
   6. Space complexity O\(1\)

### Solution

```java
class Solution {
    public boolean search(int[] nums, int target) {
        int lo = 0, hi = nums.length - 1;
        int mid = 0;
        while (lo <= hi){
            mid = lo + (hi - lo)/2;
            if (nums[mid] == target) return true;
            // left part is sorted
            else if (nums[lo] < nums[mid]) {
                if (target >= nums[lo] && target < nums[mid]) hi = mid - 1;
                else lo = mid + 1;
            // right part is sorted
            } else if (nums[lo] > nums[mid]) {
                if (target > nums[mid] && target <= nums[hi]) lo = mid + 1;
                else hi = mid - 1;
            // this means nums[lo] == nums[mid] == nums[hi]
            } else {
                lo++;
            }
        }
        return false;
    }
}
```

### Additional {#additional}



