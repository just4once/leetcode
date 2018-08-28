# 744-find-smallest-letter-greater-than-target

## Question {#question}

[https://leetcode.com/problems/find-smallest-letter-greater-than-target/description/](https://leetcode.com/problems/find-smallest-letter-greater-than-target/description/)

Given a list of sorted characters letters containing only lowercase letters, and given a target letter target, find the smallest element in the list that is larger than the given target.

Letters also wrap around. For example, if the target is target = 'z' and letters = \['a', 'b'\], the answer is 'a'.

**Example:**

```text
Input:
letters = ["c", "f", "j"]
target = "a"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "c"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "d"
Output: "f"

Input:
letters = ["c", "f", "j"]
target = "g"
Output: "j"

Input:
letters = ["c", "f", "j"]
target = "j"
Output: "c"

Input:
letters = ["c", "f", "j"]
target = "k"
Output: "c"
```

**Note:**    


1. letters has a length in range \[2, 10000\].
2. letters consists of lowercase letters, and contains at least 2 unique letters.
3. target is a lowercase letter.

## Thought Process {#thought-process}

1. Linear Scan
   1. Scan from left to right, at anytime we see a character greater than our target, we can return immediately
   2. Else, we can return the first letter
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)
2. Modified Binary Search
   1. We can implement our own binary search, using lo and hi to narrow our search by half every time
   2. When the letter\[mi\] &lt;= target, we set lo = mi + 1, where mi = \(lo + hi\) / 2
   3. Else hi = mi
   4. Time complexity O\(logn\)
   5. Space complexity O\(1\)
3. Binary Search
   1. We add 1 to target and mod 26 to get the "right" target
   2. If the index is equal to the length of list, we return the first element
   3. Time complexity O\(logn\)
   4. Space complexity O\(1\)

## Solution

```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        for (char c : letters) {
            if (c > target) return c;
        }
        return letters[0];
    }
}
```

```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        int lo = 0, hi = letters.length;
        while (lo < hi) {
            int mi = lo + (hi - lo) / 2;
            if (letters[mi] <= target) lo = mi + 1;
            else hi = mi;
        }
        return letters[lo % letters.length];
    }
}
```

```java
class Solution {
    public char nextGreatestLetter(char[] letters, char target) {
        target = (char) ((target + 1 - 'a') % 26 + 'a');
        int i = Arrays.binarySearch(letters, target);
        if (i < 0) i = -(i + 1);
        if (i == letters.length) i = 0;
        return letters[i];
    }
}
```

## Additional {#additional}

