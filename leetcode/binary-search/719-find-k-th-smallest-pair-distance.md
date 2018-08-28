# 719-find-k-th-smallest-pair-distance

## Question {#question}

[https://leetcode.com/problems/find-k-th-smallest-pair-distance/description/](https://leetcode.com/problems/find-k-th-smallest-pair-distance/description/)

Given an integer array, return the k-th smallest distance among all the pairs. The distance of a pair \(A, B\) is defined as the absolute difference between A and B.

**Example:**

```text
Input:
nums = [1,3,1]
k = 1
Output: 0 
Explanation:
Here are all the pairs:
(1,3) -> 2
(1,1) -> 0
(3,1) -> 2
Then the 1st smallest distance pair is (1,1), and its distance is 0.
```

**Note:**    


1. 2 &lt;= len\(nums\) &lt;= 10000.
2. 0 &lt;= nums\[i\] &lt; 1000000.
3. 1 &lt;= k &lt;= len\(nums\) \* \(len\(nums\) - 1\) / 2.

## Thought Process {#thought-process}

1. Brute Force \(TLE\)
   1. Generate all the distance pairs through n^2 process
   2. Sort the distances and return the k-th distance by returning distance\[k - 1\]
   3. Time complexity O\(n^2\)
   4. Space complexity O\(n^2\)
2. Heap \(TLE\)
   1. Sort the nums array and save all the adjacent pairs as nodes into the minHeap
   2. Every time, we poll the min distance pair out and save the next pair
   3. After looping for k times, the top node in the heap will contain the pair with kth distance
   4. Time complexity O\(nlogn + kLogn\)
   5. Space complexity O\(n\)
3. Binary Search
   1. Since all numbers are non-negative, the kth distance must be in between \[0, max - min\], lo and hi respectively
   2. We perform binary search on this range until lo and hi merge, and we narrow our search using a separate function count\(nums, mi\), where count\(nums, mi\) return numbers of distances &lt;= mi
   3. If count\(mi\) is smaller than k, we have to set lo = mi + 1
   4. Else hi = mi
   5. The count\(nums, mi\) can be efficiently implemented using two pointers \(sliding window\) method
   6. Time complexity O\(nlogn + n^2logw\), where w = max - min
   7. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int smallestDistancePair(int[] nums, int k) {
        int n = nums.length;
        int[] distances = new int[n * (n - 1) / 2];
        int z = 0;
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                distances[z++] = Math.abs(nums[i] - nums[j]);
            }
        }
        Arrays.sort(distances);
        return distances[k - 1];
    }
}
```

```java
class Solution {
    private static class Node {
        int i, j;
        public Node(int i, int j) {
            this.i = i;
            this.j = j;
        }
    }

    public int smallestDistancePair(int[] nums, int k) {
        Arrays.sort(nums);
        PriorityQueue<Node> minHeap = new PriorityQueue<>((a, b) -> (nums[a.j] - nums[a.i]) - (nums[b.j] - nums[b.i]));
        for (int i = 0; i + 1 < nums.length; i++) {
            minHeap.offer(new Node(i, i + 1));
        }
        Node cur = null;
        while (k-- > 0) {
            cur = minHeap.poll();
            if (cur.j + 1 < nums.length) minHeap.offer(new Node(cur.i, cur.j + 1));
        }
        return nums[cur.j] - nums[cur.i];
    }
}
```

```java
class Solution {
    public int smallestDistancePair(int[] nums, int k) {
        Arrays.sort(nums);
        int lo = 0, hi = nums[nums.length - 1] - nums[0];
        while (lo != hi) {
            int mi = lo + (hi - lo) / 2;
            if (count(nums, mi) < k) lo = mi + 1;
            else hi = mi;
        }
        return lo;
    }

    private int count(int[] nums, int d) {
        int right = 1;
        int count = 0;
        while (right < nums.length) {
            int left = 0;
            while (nums[right] - nums[left] > d) left++;
            count += right - left;
            right++;
        }
        return count;
    }
}
```

## Additional {#additional}

