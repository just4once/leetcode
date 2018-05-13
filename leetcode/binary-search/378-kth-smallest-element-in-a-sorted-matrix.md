### Question {#question}

[https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/description/](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/description/)

Given anxnmatrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

**Example:**

```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],
k = 8,

return 13.
```

### Thought Process {#thought-process}

1. Heap
   1. Using min heap, we can add all the element into heap
   2. Getting kth value is trivial
   3. Time complexity O\(mn + klogk\)
   4. Space complexity O\(mn\)
2. Heap with Tuple
   1. Using tuple class to store the row, column and its value, we can use it to locate the next number
   2. We add the first row value into our heap
   3. As we poll the min element out, we can add its bottom element into our heap, which is next smallest element
   4. After looping for k - 1 time, the peek is our solution
   5. Time complexity O\(n + klogn\)
   6. Space complexity O\(n\)
3. Binary Search
   1. Using the smallest element as lo pointer and largest element as hi pointer, we can progressively narrow down our search for mid
   2. Mid is used as way to judge how many element are smaller or equal to it, and the count is used how we narrow our search for step i
   3. When count is less than k, we need to increase our lo, otherwise we decrease hi
   4. Time complexity O\(nlogm\), where m = max - min
   5. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        for (int i = 0; i < matrix.length; i++) {
            for (int j = 0; j < matrix[i].length; j++) {
                pq.offer(matrix[i][j]);
            }
        }
        while (--k > 0) {
            pq.poll();
        }
        return pq.peek();
    }
}
```

```java
class Solution {
    private class Tuple implements Comparable<Tuple> {
        private int row, col, val;
        public Tuple(int row, int col, int val) {
            this.row = row;
            this.col = col;
            this.val = val;
        }

        @Override
        public int compareTo(Tuple that) {
            return this.val - that.val;
        }
    }
    public int kthSmallest(int[][] matrix, int k) {
        if (matrix.length == 0) return -1;
        PriorityQueue<Tuple> pq = new PriorityQueue<>();
        int n = matrix.length;
        for (int col = 0; col < n; col++) {
            pq.offer(new Tuple(0, col, matrix[0][col]));
        }
        while (--k > 0) {
            Tuple t = pq.poll();
            if (t.row + 1 == n) continue;
            pq.offer(new Tuple(t.row + 1, t.col, matrix[t.row + 1][t.col]));
        }
        return pq.peek().val;
    }
}
```

```java
class Solution {
    // modified binary searching using median and count
    public int kthSmallest(int[][] matrix, int k) {
        int n= matrix.length;
        int lo = matrix[0][0], hi = matrix[n - 1][n - 1], mid;
        while (lo <= hi) {
            mid = lo + (hi - lo) / 2;
            int count = getCountLessOrEqual(matrix, mid, n);
            if (count < k) lo = mid + 1;
            else hi = mid - 1;
        }
        return lo;
    }

    private int getCountLessOrEqual(int[][] matrix, int val, int n) {
        int i = 0, j = n - 1;
        int res = 0;
        while (i < n) {
            while (j >= 0 && matrix[i][j] > val) j--;
            res += j + 1;
            i++;
        }
        return res;
    }
}
```

### Additional {#additional}



