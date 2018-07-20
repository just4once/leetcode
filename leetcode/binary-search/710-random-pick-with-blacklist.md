### Question {#question}

Given a blacklist B containing unique integers from \[0, N\), write a function to return a uniform random integer from \[0, N\) which is NOT in B.

Optimize it such that it minimizes the call to system’s Math.random\(\).

**Note:          
**

1. 1 &lt;= N &lt;= 1000000000
2. 0 &lt;= B.length &lt; min\(100000, N\)
3. \[0, N\) does NOT include N. See interval notation.

**Example 1:**

```
Input: 
["Solution","pick","pick","pick"]
[[1,[]],[],[],[]]
Output: [null,0,0,0]
```

**Example 2:**

```
Input: 
["Solution","pick","pick","pick"]
[[2,[]],[],[],[]]
Output: [null,1,1,1]
```

**Example 3:**

```
Input: 
["Solution","pick","pick","pick"]
[[3,[1]],[],[],[]]
Output: [null,0,0,2]
```

**Example 4:**

```
Input: 
["Solution","pick","pick","pick"]
[[4,[2]],[],[],[]]
Output: [null,1,3,1]
```

**Explanation of Input Syntax:          
**

The input is two lists: the subroutines called and their arguments. Solution's constructor has two arguments, N and the blacklist B. pick has no arguments. Arguments are always wrapped with a list, even if there aren't any.

### Thought Process {#thought-process}

1. Set \(TLE\)
   1. Use set to save the blacklist and ignore the generated number r if it is inside the set
   2. Time complexity O\(B + x\), where x is times of getting blacklisted item, and the probability = B/N. The x gets worse as B gets close to N
   3. Space complexity O\(B\)
2. Set and List\(MLE\)
   1. Add all the number to the set and then remove the number form blacklist
   2. Time complexity O\(N\)
   3. Space complexity O\(N - B\)
3. Binary Search
   1. We define W to be the whitelist and B to be blacklist
   2. The question seeking W\[k\], we want to find the largest blacklist number that is smaller than W\[k\]
   3. We sort the blacklist array and then perform binary search from lo to hi
      1. loop from lo = 0 and hi = B.length - 1
      2. mid = \(lo + hi + 1\) / 2
      3. c = B\[mid\] - mid, the number of whitelist numbers less than B\[mid\]
      4. If c &gt; k, then B\[mid\] is larger then W\[k\], we should eliminate the larger part of B, so hi = mid - 1
      5. Else, B\[mid\] is our candidate, so lo = mid
      6. Step ii is important in avoiding infinite loop. When c &lt;= k, left leaning mid formula will set lo to itself
      7. At the end, our search will narrow to one blacklist number. If it's smaller than W\[k\], then W\[k\] = k + lo + 1. Else there is no blacklist number smaller than W\[k\] and res is simply k.
   4. Time complexity O\(BlogB\)
   5. Space complexity O\(1\)
4. ad

### Solution

```java
class Solution {
    private Set<Integer> set;
    private int N;
    public Solution(int N, int[] blacklist) {
        this.N = N;
        set = new HashSet<>();
        for (int num : blacklist) set.add(num);
    }

    public int pick() {
        int r = (int) (Math.random() * N);
        while (set.contains(r)) {
            r = (int) (Math.random() * N); 
        }
        return r;
    }
}
```

```java
class Solution {
    private List<Integer> list;
    private Random random;
    public Solution(int N, int[] blacklist) {
        Set<Integer> set = new HashSet<>();
        list = new ArrayList<>(N - blacklist.length);
        random = new Random();
        for (int i = 0; i < N; i++) set.add(i);
        for (int b : blacklist) set.remove(b);
        for (int w : set) list.add(w);
    }

    public int pick() {
        return list.get(random.nextInt(list.size()));
    }
}
```

```java
class Solution {
    private Random random;
    private int N;
    private int[] black;
    public Solution(int N, int[] blacklist) {
        this.random = new Random();
        this.N = N;
        this.black = blacklist;
        Arrays.sort(black);
    }
    
    public int pick() {
        int k = random.nextInt(N - black.length);
        int lo = 0, hi = black.length - 1;
        while (lo < hi) {
            int mi = lo + (hi - lo) / 2 + 1;
            if (black[mi]  - mi > k) hi = mi - 1;
            else lo = mi;
        }
        return lo == hi && black[lo] - lo <= k ? hi + k + 1 : k;
    }
}
```

### Additional {#additional}



