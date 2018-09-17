# 778-swim-in-rising-water

## Question {#question}

[https://leetcode.com/problems/swim-in-rising-water/description/](https://leetcode.com/problems/swim-in-rising-water/description/)

On an N x N grid, each square grid\[i\]\[j\] represents the elevation at that point \(i,j\).

Now rain starts to fall. At time t, the depth of the water everywhere is t. You can swim from a square to another 4-directionally adjacent square if and only if the elevation of both squares individually are at most t. You can swim infinite distance in zero time. Of course, you must stay within the boundaries of the grid during your swim.

You start at the top left square \(0, 0\). What is the least time until you can reach the bottom right square \(N-1, N-1\)?

**Example 1:**

```text
Input: [[0,2],[1,3]]
Output: 3
Explanation:
At time 0, you are in grid location (0, 0).
You cannot go anywhere else because 4-directionally adjacent neighbors have a higher elevation than t = 0.

You cannot reach point (1, 1) until time 3.
When the depth of water is 3, we can swim anywhere inside the grid.
```

**Example 2:**

```text
Input: [[0,1,2,3,4],[24,23,22,21,5],[12,13,14,15,16],[11,17,18,19,20],[10,9,8,7,6]]
Output: 16
Explanation:
 0  1  2  3  4
24 23 22 21  5
12 13 14 15 16
11 17 18 19 20
10  9  8  7  6

The final route is marked in bold.
We need to wait until time 16 so that (0, 0) and (4, 4) are connected.
```

**Note:**

1. 2 &lt;= N &lt;= 50.
2. grid\[i\]\[j\] is a permutation of \[0, ..., N\*N - 1\].

## Thought Process {#thought-process}

1. Binary Search and DFS
   1. Search between 0 and N \* N  - 1 using binary search
   2. We stop when at a particular time, t, that the bottom is reached
   3. We create a DFS function reachBottom\(grid, t, N, visit, i, j\), where t is the candidate and visit is boolean array to avoid repeated check
   4. Time complexity O\(log\(N\) \* N^2\)
   5. Space complexity O\(N^2\)
2. Union Find
   1. Union find structure will be particularly useful for finding if two points are connected
   2. We start putting each grid and its flattened index in the map
   3. Use while loop to check 0 and N \* N - 1 is connected
   4. If not, we increase the water depth and get the respective flattened index out of map and connect its neighbors if the depth is greater than theirs
   5. If yes, we can simply return the depth
   6. Time complexity O\(N^2\)???
   7. Space complexity O\(N^2\)
3. Dijkstra's Search
   1. Create a node to store val and respective location i
   2. Use heap to store the nodes based on its val
   3. Every time, we poll the min node out and compared node's val with our current answer, res, where the max of two is our new answer
   4. If we have reach the right bottom corner, our search is done
   5. Else, we need to add current node's unvisited neighbors to the heap
   6. Time complexity O\(N^2log\(N\)\)
   7. Space complexity O\(N^2\)

## Solution

```java
class Solution {
    public int swimInWater(int[][] grid) {
        int N = grid.length;
        int lo = 0, hi = N * N - 1;
        while (lo < hi) {
            int mi = lo + (hi - lo) / 2;
            boolean[][] visit = new boolean[N][N];
            if (reachBottom(grid, mi, N, visit, 0, 0)) hi = mi;
            else lo = mi + 1;
        }
        return lo;
    }
    
    private boolean reachBottom(int[][] grid, int t, int N, boolean[][] visit, int i, int j) {
        if (i < 0 || i >= N || j < 0 || j >= N || visit[i][j] || grid[i][j] > t) return false;
        visit[i][j] = true;
        if (i == N - 1 && j == N - 1) return true;
        else return reachBottom(grid, t, N, visit, i + 1, j) || reachBottom(grid, t, N, visit, i - 1, j) || reachBottom(grid, t, N, visit, i, j - 1) || reachBottom(grid, t, N, visit, i, j + 1);
    }
}
```

```java
class Solution {
    private int[][] dirs = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
    
    private class UF {
        int[] ids;
        int[] size;
        public UF(int n) {
            ids = new int[n];
            size = new int[n];
            for (int i = 0; i < n; i++) {
                ids[i] = i;
                size[i] = 1;
            }
        }
        
        public boolean isConnected(int i, int j) {
            return find(i) == find(j);
        }
        
        private int find(int i) {
            int root = i;
            while (ids[root] != root) root = ids[root];
            while (i != root) {
                int next = ids[i];
                ids[i] = root;
                i = next;
            }
            return ids[i];
        }
        
        public void union(int i, int j) {
            int rootI = find(i), rootJ = find(j);
            if (rootI == rootJ) return;
            if (size[rootI] < size[rootJ]) {
                ids[rootI] = rootJ;
                size[rootJ] += size[rootI];
            } else {
                ids[rootJ] = rootI;
                size[rootI] += size[rootJ];
            }
        }
    }
    
    public int swimInWater(int[][] grid) {
        int N = grid.length;
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                map.put(grid[i][j], i * N + j);
            }
        }
        UF uf = new UF(N * N);
        int res = 0;
        while (!uf.isConnected(0, N * N - 1)) {
            res++;
            int k = map.get(res);
            int i = k / N, j = k % N;
            for (int[] dir : dirs) {
                int x = i + dir[0], y = j + dir[1];
                if (x >= 0 && x < N && y >= 0 && y < N && grid[i][j] > grid[x][y]) {
                    uf.union(k, x * N + y);
                }
            }
        }
        return res;
    }
}
```

```java
class Solution {
    private class Node{
        int v, i, j;
        public Node(int v, int i, int j) {
            this.v = v;
            this.i = i;
            this.j = j;
        }
    }
    
    private int[][] dirs = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
    
    public int swimInWater(int[][] grid) {
        int N = grid.length;
        PriorityQueue<Node> pq = new PriorityQueue<>((a, b) -> a.v - b.v);
        pq.offer(new Node(grid[0][0], 0, 0));
        int res = grid[0][0];
        boolean[][] visited = new boolean[N][N];
        while (!pq.isEmpty()) {
            Node cur = pq.poll();
            res = Math.max(cur.v, res);
            if (cur.i == N - 1 && cur.j == N - 1) break;
            for (int[] dir : dirs) {
                int x = cur.i + dir[0];
                int y = cur.j + dir[1];
                if (x >= 0 && x < N && y >= 0 && y < N && !visited[x][y]) {
                    pq.offer(new Node(grid[x][y], x, y));
                    visited[x][y] = true;
                }
            }
        }
        return res;
    }
}
```

## Additional {#additional}

