# 223-rectangle-area

## Question {#question}

[https://leetcode.com/problems/rectangle-area/description/](https://leetcode.com/problems/rectangle-area/description/)

Find the total area covered by two **rectilinear** rectangles in a **2D** plane.

Each rectangle is defined by its bottom left corner and top right corner as shown in the figure.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Check Overlap
   1. If there is no overlap, we know the total area is the sum of areas
   2. The overlap can be check if any of indices fall in the range of other, if any of the indices is outside of the range, there is no overlap
   3. Time complexity O\(1\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        // if one side of one rectangle lies outside the boundary of the other, the overlap is 0.
        int overlap;
        if (C <= E || A >= G || B >= H || D <= F) {
            overlap = 0;
        } else {
            // the width is the the minimum of right boundary - minimum of left boundary
            int width = Math.min(C, G) - Math.max(A, E);
            // the height is the minimum of the top boundary - maximum of bottom boundary
            int height = Math.min(D, H) - Math.max(B, F);
            overlap = width * height;
        }
        return (C - A) * (D - B) + (G - E) * (H - F) - overlap;
    }
}
```

## Additional {#additional}

