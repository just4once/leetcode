### Question {#question}

[https://leetcode.com/problems/self-crossing/description/](https://leetcode.com/problems/self-crossing/description/)

You are given an array x of n positive numbers. You start at point \(0,0\) and moves x\[0\] metres to the north, then x\[1\] metres to the west, x\[2\] metres to the south, x\[3\] metres to the east and so on. In other words, after each move your direction changes counter-clockwise.

Write a one-pass algorithm with O\(1\) extra space to determine, if your path crosses itself, or not.

**Example:**

```
Given x = [2, 1, 1, 2],
?????
?   ?
???????>
    ?

Return true (self crossing)
```

```
Given x = [1, 2, 3, 4],
????????
?      ?
?
?
?????????????>

Return false (not self crossing)
```

```
Given x = [1, 1, 1, 1],
?????
?   ?
?????>

Return true (self crossing)
```

### Thought Process {#thought-process}

1. Spiral Directions
   1. Spiraling outward: If the parallel lines' keep increasing, there will not be any cross, x\[i\] &gt; x\[i - 2\]
   2. Spiraling inward: once the direction switch, we need to make sure the distance keep decreasing
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

### Solution

```java
class Solution {
    public boolean isSelfCrossing(int[] x) {
        if (x.length < 4) return false;
        int i = 2;
        // spiraling outward
        while (i < x.length && x[i] > x[i - 2]) i++;
        if (i == x.length) return false;
        // transition
        if ((i == 3 && x[i] == x[i - 2]) || (i >= 4 && x[i] >= x[i - 2] - x[i - 4])) {
            x[i - 1] -= x[i - 3];
        }
        i++;
        // spiraling inward
        while (i < x.length) {
            if (x[i] >= x[i - 2]) return true;
            i++;
        }
        return false;
    }
}
```

### Additional {#additional}



