# 454-4sum-ii

## Question {#question}

[https://leetcode.com/problems/4sum-ii/description/](https://leetcode.com/problems/4sum-ii/description/)

Given four lists A, B, C, D of integer values, compute how many tuples \(i, j, k, l\) there are such that A\[i\] + B\[j\] + C\[k\] + D\[l\] is zero.

To make problem a bit easier, all A, B, C, D have same length of N where 0 ≤ N ≤ 500. All integers are in the range of -228 to 228 - 1 and the result is guaranteed to be at most 231 - 1.

**Example:**

```text
Input:
A = [ 1, 2]
B = [-2,-1]
C = [-1, 2]
D = [ 0, 2]

Output:
2

Explanation:
The two tuples are:
1. (0, 0, 0, 1) -> A[0] + B[0] + C[0] + D[1] = 1 + (-2) + (-1) + 2 = 0
2. (1, 1, 0, 0) -> A[1] + B[1] + C[0] + D[0] = 2 + (-1) + (-1) + 0 = 0
```

## Thought Process {#thought-process}

1. Binary Search
   1. Storing sum permutations from A and B, and negative sum permutation from C and D, we can do left bound and right bound search to get number of natches
   2. Time complexity O\(n^2logn\)
   3. Space complexity O\(n^2\)
2. Hash Table
   1. Using map to store the sum from A and B, and separate map for C and D, we can find the pair in O\(1\) time
   2. The key is sum and value is count
   3. The number of pair can be calculated from count1 \* count2
   4. Time complexity O\(n^2\)
   5. Space complexity O\(n^2\)

## Solution

```java
class Solution {
    public int fourSumCount(int[] A, int[] B, int[] C, int[] D) {
        if (A.length == 0) return 0;
        int n = A.length;
        int[] part1 = new int[n * n], part2 = new int[n * n];
        int i = 0;
        for (int a : A) {
            for (int b : B) {
                part1[i++] = a + b;
            }
        }
        i = 0;
        for (int c : C) {
            for (int d : D) {
                part2[i++] = - (c + d);
            }
        }
        //Arrays.sort(part1);
        Arrays.sort(part2);
        int res = 0;
        i = 0;
        while (i < part1.length) {
            int left = binarySearch(part2, part1[i], 0, part2.length);
            if (left < part2.length && part2[left] == part1[i]) {
                int right = binarySearch(part2, part1[i] + 1, left + 1, part2.length);
                res += right - left;
            }
            i++;
        }
        return res;
    }

    private int binarySearch(int[] nums, int target, int i, int j) {
        while (i < j) {
            int m = i + (j - i) / 2;
            if (nums[m] < target) i = m + 1;
            else j = m;
        }
        return i;
    }
}
```

```java
class Solution {
    public int fourSumCount(int[] A, int[] B, int[] C, int[] D) {
        if (A.length == 0) return 0;
        Map<Integer, Integer> part1 = merge(A, B), part2 = merge(C, D);
        int res = 0;
        for (Map.Entry<Integer, Integer> entry : part1.entrySet()) {
            int count1 = entry.getValue();
            int count2 = part2.getOrDefault(-entry.getKey(), 0);
            res += count1 * count2;
        }
        return res;
    }

    private Map<Integer, Integer> merge(int[] A, int[] B) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int a : A) {
            for (int b : B) {
                map.put(a + b, map.getOrDefault(a + b, 0) + 1);
            }
        }
        return map;
    }
}
```

## Additional {#additional}

