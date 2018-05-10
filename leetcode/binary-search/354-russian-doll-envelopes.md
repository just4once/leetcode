### Question {#question}

[https://leetcode.com/problems/russian-doll-envelopes/description/](https://leetcode.com/problems/russian-doll-envelopes/description/)

You have a number of envelopes with widths and heights given as a pair of integers \(w, h\). One envelope can fit into another if and only if both the width and height of one envelope is greater than the width and height of the other envelope.

What is the maximum number of envelopes can you Russian doll? \(put one inside other\)

**Example:**

```
Given envelopes = [[5,4],[6,4],[6,7],[2,3]],
the maximum number of envelopes you can Russian doll is 3 ([2,3] => [5,4] => [6,7]).
```

### Thought Process {#thought-process}

1. DP
   1. Using dp\[i\] to store the max number ending at envelope i
   2. We need to sort the element based on their width, w
   3. Then for each envelope before envelope i, we try to see if it can be placed inside envelope i
   4. Time complexity O\(n^2\)
   5. Space complexity O\(n\)
2. Binary Search
   1. Similar to longest increasing sequence, we can try to find longest increasing envelope sequence
   2. However, we need to sort the envelope ascendingly based on weight, descendingly based on hjeight
   3. This way we can make sure we safely skip the envelope that has the same weight but higher height
   4. Time complexity O\(nlogn\)
   5. Space complexity O\(n\)

### Solution

```java
class Solution {
    public int maxEnvelopes(int[][] envelopes) {
        if (envelopes == null || envelopes.length == 0 || envelopes[0] == null || envelopes[0].length != 2) return 0;
        Arrays.sort(envelopes, (a, b) -> a[0] - b[0]);
        int n = envelopes.length, res = 1;
        int[] dp = new int[n];
        dp[0] = 1;
        for (int i = 1; i < n; i++) {
            int prev = 0;
            for (int j = 0; j < i; j++) {
                if (canPlaceIn(envelopes[j], envelopes[i])) {
                    prev = Math.max(dp[j], prev);
                }
            }
            dp[i] = prev + 1;
            res = Math.max(dp[i], res);
        }
        return res;
    }

    private boolean canPlaceIn(int[] en1, int[] en2) {
        return en1[0] < en2[0] && en1[1] < en2[1];
    }
}
```

```java
class Solution {
    public int maxEnvelopes(int[][] envelopes) {
        if (envelopes == null || envelopes.length == 0 || envelopes[0] == null || envelopes[0].length != 2) return 0;
        Arrays.sort(envelopes, (a, b) -> a[0] == b[0] ? b[1] - a[1] : a[0] - b[0]);
        int n = envelopes.length, len = 1;
        int[] dp = new int[n];
        dp[0] = envelopes[0][1];
        for (int i = 1; i < n; i++) {
            if (envelopes[i][1] > dp[len - 1]) {
                dp[len++] = envelopes[i][1];
            } else {
                int id = Arrays.binarySearch(dp, 0, len, envelopes[i][1]);
                if (id < 0) id = -(id + 1);
                dp[id] = envelopes[i][1];
            }
        }
        return len;
    }
}
```

### Additional {#additional}



