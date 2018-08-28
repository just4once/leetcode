# 247-strobogrammatic-number-ii

## Question {#question}

[https://leetcode.com/problems/strobogrammatic-number-ii/description/](https://leetcode.com/problems/strobogrammatic-number-ii/description/)

A strobogrammatic number is a number that looks the same when rotated 180 degrees \(looked at upside down\).

Find all strobogrammatic numbers that are of length = n.

**Example:**

```text
Given n = 2, return ["11","69","88","96"].
```

## Thought Process {#thought-process}

1. Recursion
   1. We need to get previous string, meaning n - 2 set, and append the strobogrammatic pair to the head and tail
   2. The strobogrammatic pairs are 11, 69, 88, and 96
   3. One thing we need to keep in mind that number that contains 0XX0, although it's invalid at n - 2, we need them when constructing for n
   4. We pass another factor m to determine whether we are constructing at n
   5. Time complexity ???
   6. Space complexity ???
2. Iterative
   1. Time complexity ???
   2. Space complexity ???
3. Backtrack
   1. We can use an array of character to save the path to reach to the end
   2. 

## Solution

```java
class Solution {
    public List<String> findStrobogrammatic(int n) {
        return build(n, n);
    }

    private List<String> build(int n, int m) {
        List<String> res = new ArrayList<>();
        if (n <= 0) {
            res.add("");
        } else if (n == 1) {
            res.add("0");
            res.add("1");
            res.add("8");
        } else {
            List<String> pre = build(n - 2, m);
            for (String p : pre) {
                if (n != m) res.add("0" + p + "0");
                res.add("1" + p + "1");
                res.add("6" + p + "9");
                res.add("8" + p + "8");
                res.add("9" + p + "6");
            }
        }
        return res;
    }
}
```

```java
class Solution {
    public List<String> findStrobogrammatic(int n) {
        List<String> r = Arrays.asList("");
        if (n % 2 == 1) r = Arrays.asList("0", "1", "8");
        for (int i = (n % 2) + 2; i <= n; i += 2) {
            List<String> newList = new ArrayList<>();
            for (String s : r) {
                if (i != n) newList.add("0" + s + "0");
                newList.add("1" + s + "1");
                newList.add("6" + s + "9");
                newList.add("8" + s + "8");
                newList.add("9" + s + "6");
            }
            r = newList;
        }
        return r;
    }
}
```

```java
class Solution {
    public List<String> findStrobogrammatic(int n) {
        List<String> res = new ArrayList<>();
        backtrack(res, new char[n], 0, n - 1);
        return res;
    }

    private void backtrack(List<String> res, char[] path, int l, int r) {
        if (l > r) {
            res.add(String.valueOf(path));
        } else if (l == r) {
            // the middle element
            path[l] = '0';
            res.add(String.valueOf(path));
            path[l] = '1';
            res.add(String.valueOf(path));
            path[l] = '8';
            res.add(String.valueOf(path));
        } else {
            if (l != 0) {
                path[l] = '0';
                path[r] = '0';
                backtrack(res, path, l + 1, r - 1);
            }
            path[l] = '1';
            path[r] = '1';
            backtrack(res, path, l + 1, r - 1);
            path[l] = '6';
            path[r] = '9';
            backtrack(res, path, l + 1, r - 1);
            path[l] = '8';
            path[r] = '8';
            backtrack(res, path, l + 1, r - 1);
            path[l] = '9';
            path[r] = '6';
            backtrack(res, path, l + 1, r - 1);
        }
    }
}
```

```java
class Solution {
    private char[] single = {'0', '1', '8'};
    private char[][] pair = {{'0', '0'}, {'1', '1'}, {'6', '9'}, {'8', '8'}, {'9', '6'}};
    public List<String> findStrobogrammatic(int n) {
        List<String> res = new ArrayList<>();
        backtrack(res, new char[n], 0, n - 1);
        return res;
    }

    private void backtrack(List<String> res, char[] path, int l, int r) {
        if (l > r) {
            res.add(String.valueOf(path));
        } else if (l == r) {
            // the middle element, single element
            for (int i = 0; i < single.length; i++) {
                path[l] = single[i];
                res.add(String.valueOf(path));
            }
        } else {
            // padding the head and tail to the path
            for (int i = 0; i < pair.length; i++) {
                if (i == 0 && l == 0) continue;
                path[l] = pair[i][0];
                path[r] = pair[i][1];
                backtrack(res, path, l + 1, r - 1);
            }
        }
    }
}
```

## Additional {#additional}

