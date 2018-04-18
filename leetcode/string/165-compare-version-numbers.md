### Question {#question}

[https://leetcode.com/problems/compare-version-numbers/description/](https://leetcode.com/problems/compare-version-numbers/description/)

Compare two version numbers version1 and version2.

If version1 &gt; version2 return 1, if version1 &lt; version2 return -1, otherwise return 0.

You may assume that the version strings are non-empty and contain only digits and the . character.

The . character does not represent a decimal point and is used to separate number sequences.

For instance, 2.5 is not "two and a half" or "half way to version three", it is the fifth second-level revision of the second first-level revision.

**Example:**

```
0.1 < 1.1 < 1.2 < 13.37
```

### Thought Process {#thought-process}

1. Split and Compare
   1. Start from the first field until we reach the end or the numbers are different
   2. Time complexity O\(n\), where n is number of fields
   3. Space complexity O\(n\)

### Solution

```java
class Solution {
    public int compareVersion(String version1, String version2) {
        String[] ver1 = version1.split("\\.");
        String[] ver2 = version2.split("\\.");
        int n = Math.max(ver1.length, ver2.length);
        for (int i = 0; i < n; i++){
            int v1 = i >= ver1.length ? 0 : Integer.parseInt(ver1[i]);
            int v2 = i >= ver2.length ? 0 : Integer.parseInt(ver2[i]);
            int cmp = Integer.compare(v1, v2);
            if (cmp != 0) return cmp;
        }
        return 0;
    }
}
```

### Additional {#additional}



