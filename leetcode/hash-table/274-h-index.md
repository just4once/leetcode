### Question {#question}

[https://leetcode.com/problems/h-index/description/](https://leetcode.com/problems/h-index/description/)

Given an array of citations \(each citation is a non-negative integer\) of a researcher, write a function to compute the researcher's h-index.

According to the [definition of h-index on Wikipedia](https://en.wikipedia.org/wiki/H-index): "A scientist has index h if h of his/her N papers have **at least **h citations each, and the other N − h papers have **no more than **hcitations each."

**Example:**

```
Given citations = [3, 0, 6, 1, 5], 
which means the researcher has 5 papers in total and each of them had received 3, 0, 6, 1, 5 citations respectively.
Since the researcher has 3 papers with at least 3 citations each and the remaining two with no more than 3 citations 
each, his h-index is 3.
```

### Thought Process {#thought-process}

1. Sort
   1. If we sort citations in descending order and every index is a potential h-index
   2. As long we can make sure the citation is greater than its index, there are index on its left that satisfy the same requirement
   3. Because int array cannot take collections comparator, we can do it in reverse
   4. Time complexity O\(n logn\)
   5. Space complexity O\(1\)
2. Bucket Sort
   1. Store the respective count in each potential h-index bucket
   2. 

### Solution

```java
class Solution {
    public int hIndex(int[] citations) {
        Arrays.sort(citations);
        int n = citations.length, i = n - 1;
        while (i >= 0 && citations[i] >= n - i) i--;
        return n - i - 1;
    }
}
```

```java
class Solution {
    public int hIndex(int[] citations) {
        int n = citations.length;
        int[] buckets = new int[n + 1];
        for (int cite : citations) {
            buckets[Math.min(cite, n)]++;
        }
        int total = 0;
        for (int h = n; h >= 0; h--) {
            total += buckets[h];
            if (total >= h) return h;
        }
        return 0;
    }
}
```

### Additional {#additional}



