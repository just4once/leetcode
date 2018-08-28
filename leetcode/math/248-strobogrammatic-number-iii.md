# 248-strobogrammatic-number-iii

## Question {#question}

[https://leetcode.com/problems/strobogrammatic-number-iii/description/](https://leetcode.com/problems/strobogrammatic-number-iii/description/)

A strobogrammatic number is a number that looks the same when rotated 180 degrees \(looked at upside down\).

Write a function to count the total strobogrammatic numbers that exist in the range of low &lt;= num &lt;= high.

**Example:**

```text
Given low = "50", high = "100", return 3. Because 69, 88, and 96 are three strobogrammatic numbers.
```

## Thought Process {#thought-process}

1. Construct strobogrammatic number
   1. We construct the number from length low to high and compare it with the range
   2. We skip the number that falls outside the range, increase the count othersie
   3. Time complexity ???
   4. Space complexity ???
2. Count the number in range
   1. We can use count to speed up the process by avoiding number generation
   2. The number count is multiply by 5 for every increment on n
   3. The base cases are n = 1, 2, 3, which the number of stro number is 3, 4, 12
3. Count and Subtract
   1. We can actually use the count difference to get the number of strobogrammtic number in range
   2. Count\(num &lt;= high\) - count\(num &lt; low\)

## Solution

```java
class Solution {
    private char[][] pair = {{'0', '0'}, {'1', '1'}, {'6', '9'}, {'8', '8'}, {'9', '6'}};
    public int strobogrammaticInRange(String low, String high) {
        int[] count = new int[1];
        for (int i = low.length(); i <= high.length(); i++) {
            dfs(low, high, new char[i], 0, i -1, count);
        }
        return count[0];
    }

    private void dfs(String low, String high, char[] chars, int l, int r, int[] count) {
        if (l > r) {
            String num = String.valueOf(chars);
            // skip number that is smaller than the low || higher than the high
            if (num.length() == low.length() && num.compareTo(low) < 0) return;
            if (num.length() == high.length() && num.compareTo(high) > 0) return;
            count[0]++;
        } else {
            for (char[] p : pair) {
                chars[l] = p[0];
                chars[r] = p[1];
                // skip those invalid number starts with 0
                if (chars.length != 1 && chars[0] == '0') continue;
                // skip odd length number that we overcount for 69 and 96 pair
                if (l == r && p[0] != p[1]) continue;
                dfs(low, high, chars, l + 1, r - 1, count);
            }
        }
    }
}
```

```java
class Solution {
    private char[][] pair = {{'0', '0'}, {'1', '1'}, {'6', '9'}, {'8', '8'}, {'9', '6'}};
    public int strobogrammaticInRange(String low, String high) {
        int[] count = new int[1];
        for (int i = low.length(); i <= high.length(); i++) {
            if (i > low.length() && i < high.length()) count[0] += getCount(i);
            else dfs(low, high, new char[i], 0, i -1, count);
        }
        return count[0];
    }

    private void dfs(String low, String high, char[] chars, int l, int r, int[] count) {
        if (l > r) {
            String num = String.valueOf(chars);
            // skip number that is smaller than the low || higher than the high
            if (num.length() == low.length() && num.compareTo(low) < 0) return;
            if (num.length() == high.length() && num.compareTo(high) > 0) return;
            count[0]++;
        } else {
            for (char[] p : pair) {
                chars[l] = p[0];
                chars[r] = p[1];
                // skip those invalid number starts with 0
                if (chars.length != 1 && chars[0] == '0') continue;
                // skip odd length number that we overcount for 69 and 96 pair
                if (l == r && p[0] != p[1]) continue;
                dfs(low, high, chars, l + 1, r - 1, count);
            }
        }
    }

    private int getCount(int k) {
        int res = 4;
        if (k % 2 == 1) res *= 3;
        for (int i = 1; i < k / 2; i++) {
            res *= 5;
        }
        return res;
    }
}
```

```java
class Solution {
    private char[][] pair = {{'0', '0'}, {'1', '1'}, {'6', '9'}, {'8', '8'}, {'9', '6'}};
    public int strobogrammaticInRange(String low, String high) {
        if (low.length() > high.length()) return 0;
        if (low.length() == high.length() && low.compareTo(high) > 0) return 0;
        int lowCount = count(low, false);
        return count(high, true) - count(low, false);
    }

    private int count(String num, boolean include) {
        int count = 0, n = num.length();
        // count all smaller numbers
        for (int i = 1; i < n; i++) {
            count += getCount(i);
        }
        // count the equal length;
        count += getEqualLength(num.toCharArray(), new char[n], 0, n - 1, include);
        return count;
    }

    private int getEqualLength(char[] num, char[] chars, int l, int r, boolean include) {
        if (l > r) {
            int compare = compare(chars, num);
            if (include) {
                return compare <= 0 ? 1 : 0;
            } else {
                return compare < 0 ? 1: 0;
            }
        }
        int count = 0;
        for (char[] p : pair) {
            chars[l] = p[0];
            chars[r] = p[1];
            if (num.length != 1 && chars[0] == '0') continue;
            if (l == r && p[0] != p[1]) continue;
            count += getEqualLength(num, chars, l + 1, r - 1, include);
        }
        return count;
    }

    private int compare(char[] n1, char[] n2) {
        for (int i = 0; i < n1.length; i++) {
            if (n1[i] < n2[i]) return -1;
            else if (n1[i] > n2[i]) return 1;
        }
        return 0;
    }

    private int getCount(int k) {
        if (k == 1) return 3;
        int res = 4;
        if (k % 2 == 1) res *= 3;
        for (int i = 1; i < k / 2; i++) {
            res *= 5;
        }
        return res;
    }
}
```

## Additional {#additional}

