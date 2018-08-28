# 528-random-pick-with-weight

## Question {#question}

[https://leetcode.com/problems/random-pick-with-weight/description/](https://leetcode.com/problems/random-pick-with-weight/description/)

Given an array w of positive integers, where w\[i\] describes the weight of index i, write a function pickIndex which randomly picks an index in proportion to its weight.

**Note:**

1. 1 &lt;= w.length &lt;= 10000
2. 1 &lt;= w\[i\] &lt;= 10^5
3. pickIndex will be called at most 10000 times.

**Example 1:**

```text
Input: 
["Solution","pickIndex"]
[[[1]],[]]
Output: [null,0]
```

**Example 2:**

```text
Input: 
["Solution","pickIndex","pickIndex","pickIndex","pickIndex","pickIndex"]
[[[1,3]],[],[],[],[],[]]
Output: [null,0,1,1,1,0]
```

**Explanation of Input Syntax:**

The input is two lists: the subroutines called and their arguments. Solution's constructor has one argument, the array w. pickIndex has no arguments. Arguments are always wrapped with a list, even if there aren't any.

## Thought Process {#thought-process}

1. Binary Search
   1. Since every integer is weighted, we need to get the total sum before we pick a point
   2. The total sum does not exceed the integer max value, so we can use a int to store the sum
   3. After creating accumulated sum array, we generate a random point, r, between \[0, sum\) and perform binary search on this accumulated array
   4. Time complexity O\(n\)
   5. Space complexity O\(n\)
2. TreeMap
   1. We can leverage the treemap built-in treemap to do similar thing as above
   2. Save the accumulated sum and its index, we can retrieve the index latter
   3. Time complexity O\(n\)
   4. Space complexity O\(n\)
3. asd

## Solution

```java
class Solution {
    private int[] presum;
    private int n;
    private Random rand;

    public Solution(int[] w) {
        n = w.length;
        presum = new int[n];
        rand = new Random();
        presum[0] = w[0];
        for (int i = 1; i < n; i++) presum[i] = presum[i - 1] + w[i];
    }

    public int pickIndex() {
        int r = rand.nextInt(presum[n - 1]) + 1;
        int i = Arrays.binarySearch(presum, r);
        if (i < 0) i = -(i + 1);
        return i;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(w);
 * int param_1 = obj.pickIndex();
 */
```

```java
class Solution {
    private TreeMap<Integer, Integer> map;
    private Random rand;
    private int total;

    public Solution(int[] w) {
        map = new TreeMap<>();
        total = 0;
        rand = new Random();
        for (int i = 0; i < w.length; i++) {
            total += w[i];
            map.put(total, i);
        }
    }

    public int pickIndex() {
        int k = map.higherKey(rand.nextInt(total));
        return map.get(k);
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(w);
 * int param_1 = obj.pickIndex();
 */
```

## Additional {#additional}

