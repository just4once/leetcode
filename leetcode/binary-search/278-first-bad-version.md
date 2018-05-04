### Question {#question}

[https://leetcode.com/problems/first-bad-version/description/](https://leetcode.com/problems/first-bad-version/description/)

You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have n versions \[1, 2, ..., n\] and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API bool isBadVersion\(version\) which will return whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

**Example:**

```

```

### Thought Process {#thought-process}

1. Binary Search
   1. We test the mid version is bad or not
   2. If it's bad, we move right pointer to mid, else we move left pointer to mid + 1
   3. Notice we we should not use lo &lt;= hi in the while condition, since it will stuck indefinitely
   4. Time complexity O\(logn\)
   5. Space complexity O\(1\)

### Solution

```java
/* The isBadVersion API is defined in the parent class VersionControl.
      boolean isBadVersion(int version); */

public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int lo = 1, hi = n, mi;
        while (lo < hi) {
            mi = lo + (hi - lo) / 2;
            if (isBadVersion(mi)) hi = mi;
            else lo = mi + 1;
        }
        return lo;
    }
}
```

### Additional {#additional}



