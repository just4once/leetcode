### Question {#question}

[https://leetcode.com/problems/permutation-sequence/description/](https://leetcode.com/problems/permutation-sequence/description/)

The set \[1,2,3,…,n\] contains a total of n! unique permutations.

By listing and labeling all of the permutations in order,

We get the following sequence \(ie, for n = 3\):

1. "123"
2. "132"
3. "213"
4. "231"
5. "312"
6. "321"

Given n and k, return the kth permutation sequence.

**Note:** Given n will be between 1 and 9 inclusive.

**Example:**

```

```

### Thought Process {#thought-process}

1. Find Pattern
   1. The number of permutation is n!
   2. Each digit of the permutation can be determined by the k, using the formula k / \(n - 1\)
   3. As we find out the number we want, \(technically index in this case\), we remove the number from the list
   4. The k need to be mod as well to find the new relative position without each group
   5. Time complexity O\(n^2\)
   6. Space complexity O\(n\)

### Solution

```java
class Solution {
    public String getPermutation(int n, int k) {
        /*  1 2 3 4     2 1 3 4     3 1 2 4     4 1 2 3
            1 2 4 3     2 1 4 3     3 1 4 2     4 1 3 2
            1 3 2 4     2 3 1 4     3 2 1 4     4 2 1 3
            1 3 4 2     2 3 4 1     3 2 4 1     4 2 3 1
            1 4 2 3     2 4 1 3     3 4 1 2     4 3 1 2
            1 4 3 2     2 4 3 1     3 4 2 1     4 3 2 1*/
        int weight = 1;
        List<Integer> nums = new LinkedList<>();
        StringBuilder sb = new StringBuilder();
        for (int i = 1; i <= n; i++) {
            nums.add(i);
            weight *= i;
        }
        k--;
        for (int i = n; i > 0; i--) {
            weight /= i;
            int id = k / weight;
            sb.append(nums.get(id));
            nums.remove(id);
            k %= weight;
        }
        return sb.toString();
    }
}
```

### Additional {#additional}



