### Question {#question}

[https://leetcode.com/problems/random-point-in-non-overlapping-rectangles/description/](https://leetcode.com/problems/random-point-in-non-overlapping-rectangles/description/)

Given a list of non-overlapping axis-aligned rectangles rects, write a function pick which randomly and uniformily picks an integer point in the space covered by the rectangles.

**Note:          
**

1. An integer point is a point that has integer coordinates. 
2. A point on the perimeter of a rectangle is included in the space covered by the rectangles. 
3. ith rectangle = rects\[i\] = \[x1,y1,x2,y2\], where \[x1, y1\] are the integer coordinates of the bottom-left corner, and \[x2, y2\] are the integer coordinates of the top-right corner.
4. length and width of each rectangle does not exceed 2000.
5. 1 &lt;= rects.length &lt;= 100
6. pick return a point as an array of integer coordinates \[p\_x, p\_y\]
7. pick is called at most 10000 times.

**Example 1:**

```
Input: 
["Solution","pick","pick","pick"]
[[[[1,1,5,5]]],[],[],[]]
Output: 
[null,[4,1],[4,1],[3,3]]
```

**Example 2:**

```
Input: 
["Solution","pick","pick","pick","pick","pick"]
[[[[-2,-2,-1,-1],[1,0,3,0]]],[],[],[],[],[]]
Output: 
[null,[-1,-2],[2,0],[-2,-1],[3,0],[-2,-2]]
```

**Explanation of Input Syntax:  **

The input is two lists: the subroutines called and their arguments. Solution's constructor has one argument, the array of rectangles rects. pick has no arguments. Arguments are always wrapped with a list, even if there aren't any.

### Thought Process {#thought-process}

1. Binary Search
   1. To get a random point, we have to locate one rectangle then pick from it
   2. Initial thought using area fails due to some rectangles have area of 0, we use count of points instead
   3. As we count through each rectangles, we accumulate the count in presum array and record total counts
   4. Then we generate a number, r,  in \[0, total\) or better \[1, total\], this number is used to find the largest presum that are smaller or equal to r
   5. After locating the rectangle, we can either generate a point in x plus a point in y or use r generated above to get the final result
   6. The second way avoid extra random point generation, and the formula is x = x0 + \(r % w\), and y = y0 + \(r / w\) where r is reset to zero-based and rectangle-based by presum\[i\] - r and w is width of rectangle
   7. Time complexity O\(n\)
   8. Space complexity O\(n\)

### Solution

```java
class Solution {
    private int total;
    private int[][] rects;
    private int[] presum;
    private Random rand;

    public Solution(int[][] rects) {
        this.total = 0;
        this.rects = rects;
        this.presum = new int[rects.length];
        this.rand = new Random();
        for (int i = 0; i < rects.length; i++) {
            total += (rects[i][2] - rects[i][0] + 1) * (rects[i][3] - rects[i][1] + 1) ;
            presum[i] = total;
        }
    }
    
    public int[] pick() {
        int r = rand.nextInt(total) + 1;
        int i = binarySearch(presum, r);
        r = presum[i] - r;
        int w = rects[i][2] - rects[i][0] + 1;
        int x = rects[i][0] + r % w;
        int y = rects[i][1] + r / w;
        return new int[]{x, y};
    }

    private int binarySearch(int[] nums, int target) {
        int lo = 0, hi = nums.length - 1;
        while (lo < hi) {
            int mi = lo + (hi - lo) / 2;
            if (target > nums[mi]) lo = mi + 1;
            else hi = mi;
        }
        return lo;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(rects);
 * int[] param_1 = obj.pick();
 */
```

### Additional {#additional}



