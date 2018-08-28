# 360-sort-transformed-array

## Question {#question}

[https://leetcode.com/problems/sort-transformed-array/description/](https://leetcode.com/problems/sort-transformed-array/description/)

Given a **sorted** array of integersnumsand integer valuesa,bandc. Apply a quadratic function of the form f\(x\) =ax2+bx+cto each elementxin the array.

The returned array must be in **sorted order**.

Expected time complexity: **O\(n\)**

**Example:**

```text
nums = [-4, -2, 2, 4], a = 1, b = 3, c = 5,

Result: [3, 9, 15, 33]

nums = [-4, -2, 2, 4], a = -1, b = 3, c = 5

Result: [-23, -5, 1, 7]
```

## Thought Process {#thought-process}

1. Two Pointers
   1. Start from the end of the array, the value is either the max or min depends on the value of a
   2. If a is positive the, the curve is concave upward, the max is on the edges
   3. Otherwise, the curve is concave downward, the min is on the edge
   4. Time complexity O\(n\)
   5. Space complexity O\(n\) or O\(1\) extra

## Solution

```java
class Solution {
    public int[] sortTransformedArray(int[] nums, int a, int b, int c) {
        int n = nums.length;
        int[] res = new int[n];
        int i = 0, j = n - 1, index = a >= 0 ? j : i;
        while (i <= j) {
            int left = cal(a, b, c, nums[i]);
            int right = cal(a, b, c, nums[j]);
            if (a >= 0) {
                if (left >= right) {
                    res[index--] = left;
                    i++;
                } else {
                    res[index--] = right;
                    j--;
                }
            } else {
                if (left <= right) {
                    res[index++] = left;
                    i++;
                } else {
                    res[index++] = right;
                    j--;
                }
            }
        }
        return res;
    }

    private int cal(int a, int b, int c, int x) {
        return a * x * x + b * x + c;
    }
}
```

## Additional {#additional}

