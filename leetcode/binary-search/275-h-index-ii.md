### Question {#question}

[https://leetcode.com/problems/h-index-ii/description/](https://leetcode.com/problems/h-index-ii/description/)

Follow up for H-Index: What if the citations array is sorted in ascending order? Could you optimize your algorithm?

**Example:**

```

```

### Thought Process {#thought-process}

1. Binary Search
   1. Since there are n index, we have h index range from 1 to n
   2. Doing binary search, if the mid element is equal to n - mid, we have found our h index
   3. The n - mid is number of publications that are greater than or equal to citations\[mid\]
   4. Time complexity O\(logn\)
   5. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int hIndex(int[] citations) {
        int n = citations.length;
        if (n == 0) return 0;
        int lo = 0, hi = n - 1, mid;
        // If the citations and h index (n - mid) are equal, we reach the solution
        // Else if the citations is less than h, we move to right so less citation needed
        // Else move to left
        while (lo <= hi) {
            mid = lo + (hi -lo) / 2;
            if (citations[mid] == n - mid) return citations[mid];
            else if (citations[mid] < n - mid) lo = mid + 1;
            else hi = mid - 1;
        }
        return n - (hi + 1);
    }
}
```

### Additional {#additional}



