### Question {#question}

[https://leetcode.com/problems/rotate-function/description/](https://leetcode.com/problems/rotate-function/description/)

Given an array of integers A and let n to be its length.

Assume Bk to be an array obtained by rotating the array A k positions clock-wise, we define a "rotation function" F on A as follow:

F\(k\) = 0 \* Bk\[0\] + 1 \* Bk\[1\] + ... + \(n-1\) \* Bk\[n-1\].

Calculate the maximum value of F\(0\), F\(1\), ..., F\(n-1\).

**Example:**

```
A = [4, 3, 2, 6]

F(0) = (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6) = 0 + 3 + 4 + 18 = 25
F(1) = (0 * 6) + (1 * 4) + (2 * 3) + (3 * 2) = 0 + 4 + 6 + 6 = 16
F(2) = (0 * 2) + (1 * 6) + (2 * 4) + (3 * 3) = 0 + 6 + 8 + 9 = 23
F(3) = (0 * 3) + (1 * 2) + (2 * 6) + (3 * 4) = 0 + 2 + 12 + 12 = 26

So the maximum value of F(0), F(1), F(2), F(3) is F(3) = 26.
```

### Thought Process {#thought-process}

1. Math
   1. As we rotate the number clockwise, the value is increased by sum - the length \* preLastNum
   2. We start from the back, since every rotation will move the last element to the first
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int maxRotateFunction(int[] A) {
        // F(k) = 0 * Bk[0] + 1 * Bk[1] + ... + (n-1) * Bk[n-1]
        // F(k+1) = 0 * Bk+1[0] + 1 * Bk+1[1] + ... + (n-1) * Bk+1[n-1]
        //        = 0 * Bk[n - 1] + 1 * Bk[0] + ... + (n -1) * Bk[n-2]
        // F(k+1) - F(k) = Bk[0] + Bk[1] + .. Bk[n -2] - (n-1) * Bk[n-1]
        //               = sum(0 to n - 1) - n * Bk[n - 1]
        int sum = 0, F = 0, n = A.length;
        for (int i = 0; i < n; i++) {
            sum += A[i];
            F += i * A[i];
        }
        int max = F;
        for (int i = n - 1; i > 0; i--) {
            F = F + sum - n * A[i];
            max = Math.max(max, F);
        }
        return max;
    }
}
```

### Additional {#additional}



