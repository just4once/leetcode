# 365-water-and-jug-problem

## Question {#question}

[https://leetcode.com/problems/water-and-jug-problem/description/](https://leetcode.com/problems/water-and-jug-problem/description/)

You are given two jugs with capacities x and y litres. There is an infinite amount of water supply available. You need to determine whether it is possible to measure exactlyzlitres using these two jugs.

If z liters of water is measurable, you must havezliters of water contained within **one or both buckets** by the end.

Operations allowed:

* Fill any of the jugs completely with water.
* Empty any of the jugs.
* Pour water from one jug into another till the other jug is completely full or the first jug itself is empty.

**Example:**

```text
Input: x = 3, y = 5, z = 4
Output: True
```

```text
Input: x = 2, y = 6, z = 5
Output: False
```

## Thought Process {#thought-process}

1. GCD
   1. We can eliminate the z volume that is greater than x + y
   2. We can return true for z = x or y, or z = x + y
   3. The problem can be summarized as ax + by = z, where positive a and b means filling jugs a or b times, negative a and b means emptying
   4. This can be solved by \[Bézout’s identity\]\([https://en.wikipedia.org/wiki/Bézout's\_identity](https://en.wikipedia.org/wiki/Bézout's_identity)\), where we check z is multiple of GCD\(x, y\)

## Solution

```java
class Solution {
    public boolean canMeasureWater(int x, int y, int z) {
        if (x + y < z) return false;
        if (x == z || y == z || (x + y) == z) return true;
        return z % GCD(x, y) == 0;
    }

    private int GCD(int x, int y) {
        int tmp;
        while (y != 0) {
            tmp = y;
            y = x % y;
            x = tmp;
        }
        return x;
    }

    private int GCD2(int x, int y) {
        if (y == 0) return x;
        return GCD(y, x % y);
    }
}
```

## Additional {#additional}

