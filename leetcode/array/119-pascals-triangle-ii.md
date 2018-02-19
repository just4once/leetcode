### Question {#question}

[https://leetcode.com/problems/pascals-triangle-ii/description/](https://leetcode.com/problems/pascals-triangle-ii/description/)

Given an index k, return the kth row of the Pascal's triangle.

**Example:**

```
For example, given k = 3,
Return [1,3,3,1].
```

### Thought Process {#thought-process}

1. We have use Combination formula nCk = n! / \(n - k\)! k!
2. We have to be careful about potential integer overflow when multiplying, so we use long to store our intermediate answer
3. Time complexity O\(n\)
4. Space complexity O\(n\)

### Solution

```java
class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> list = new ArrayList<>(rowIndex + 1);
        long res = 1;
        for(int i = 0; i <= rowIndex; i++){
            list.add((int) res);
            res *= rowIndex - i;
            res /= i + 1;
        }
        return list;
    }
}
```

### Additional {#additional}



