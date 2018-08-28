### Question {#question}

[https://leetcode.com/problems/minimize-max-distance-to-gas-station/description/](https://leetcode.com/problems/minimize-max-distance-to-gas-station/description/)

On a horizontal number line, we have gas stations at positions stations\[0\], stations\[1\], ..., stations\[N-1\], where N = stations.length.

Now, we add K more gas stations so that D, the maximum distance between adjacent gas stations, is minimized.

Return the smallest possible value of D.

**Example:**

```
Input: stations = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10], K = 9
Output: 0.500000
```

### Thought Process {#thought-process}

1. Dynamic Programing \(TLE\)
   1. Create a dp array to store the best answer, where dp\[s\]\[k\] defines to be the answer for inserting k ending at jth station
   2. We initialize dp\[0\]\[j\] with the distance\[0\] / \(j + 1\), where j ranges from 0 to K
   3. We start loop for all distance segments from 1 to N - 1 using i, and nested loop for inserting extra stations from 0 to K using j
   4. For insert j stations for ith segment, we need to check all the previous k insertions ranges from 0 to j stations against the inserting the k stations in ith segment, the maximum of them is the candidate for our answer
   5. The answer dp\[i\]\[j\] is then the minimum of all the candiates
   6. Time complexity O\(nK^2\)
   7. Space complexity O\(nK\)
2. Greedy Approach with Heap \(TLE\)
   1. Use heap to store each distance segments along with number of segments \(initially all 1\)
   2. Every time, we pull a max distance segment out considering along with number of segment and increase the number and pull it back
   3. After K operations, we have used up all the stations
   4. Then the answer will be on top of the heap
   5. Time complexity O\(Klogn\)
   6. Space complexity O\(n\)
3. Binary Search
   1. Using the boundaries of stations, the possible width will be in between 0 and 1e8
   2. Perform binary search on the width within these boundaries, we will narrow down our search until these boundaries differ less than our desired delta
   3. Now the conditions to narrow our search to left or right depends on a separate function possible\(mi, stations, K\), where it check if we can use less than or equal to K stations to achieve the mi distance
   4. If possible return true, we set hi = mi to find better distance
   5. Else we set lo = mi
   6. Time complexity O\(nlogW\), where w = 1e8/1e-6 = 1e14
   7. Space complexity O\(1\)

### Solution

```java
class Solution {
    public double minmaxGasDist(int[] stations, int K) {
        int n = stations.length;
        double[][] dp = new double[n - 1][K + 1];
        double[] distances = new double[n - 1];
        for (int i = 1; i < n; i++) {
            distances[i - 1] = stations[i] - stations[i - 1];
        }
        for (int k = 0; k <= K; k++) {
            dp[0][k] = distances[0] / (k + 1);
        }
        for (int i = 1; i < n - 1; i++) {
            for (int j = 0; j <= K; j++) {
                double ans = 99999999;
                for (int k = 0; k <= j; k++) {
                    ans = Math.min(ans, Math.max(dp[i - 1][k], distances[i] / (j - k + 1)));
                }
                dp[i][j] = ans;
            }
        }
        return dp[n - 2][K];
    }
}
```

```java
class Solution {
    public double minmaxGasDist(int[] stations, int K) {
        PriorityQueue<int[]> maxHeap = new PriorityQueue<>((a, b) -> a[0] * 1.0 / a[1] > b[0] * 1.0 / b[1] ? -1 : 1);
        for (int i = 1; i < stations.length; i++) {
            maxHeap.offer(new int[]{stations[i] - stations[i - 1], 1});
        }
        int[] node = null;
        while (K-- > 0) {
            node = maxHeap.poll();
            node[1]++;
            maxHeap.offer(node);
        }
        node = maxHeap.poll();
        return node[0] * 1.0 / node[1];
    }
}
```

### Additional {#additional}



