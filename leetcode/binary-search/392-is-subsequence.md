### Question {#question}

[https://leetcode.com/problems/is-subsequence/description/](https://leetcode.com/problems/is-subsequence/description/)

Given a string s and a string t, check if s is subsequence of t.

You may assume that there is only lower case English letters in both s and t. t is potentially a very long \(length ~= 500,000\) string, and s is a short string \(&lt;=100\).

A subsequence of a string is a new string which is formed from the original string by deleting some \(can be none\) of the characters without disturbing the relative positions of the remaining characters. \(ie, "ace" is a subsequence of "abcde" while "aec" is not\).

**Example:**

```
s = "abc", t = "ahbgdc"
Return true.

s = "axc", t = "ahbgdc"
Return false.
```

### Thought Process {#thought-process}

1. Bucket and Binary Search
   1. Using character buckets to store all the indices for its occurence
   2. As we loop through each character of s, we do binary search on the buckets
   3. If the return index is greater than or equal to the bucket length, that means we cannot find a valid index for current character
   4. We save this index our key search for next character
   5. Time complexity O\(m + nlogm\)
   6. Space complexity O\(m\)
2. Two Pointers and Greedy
   1. We main a pointer of i and j for s and t respectively
   2. When we match a character from t, we move i pointer forward
   3. If i is able to reach the end, we know s is subsequence of t
   4. Time complexity O\(m\)
   5. Space complexity O\(1\)
3. Build-int IndexOf function
   1. Time complexity O\(m\)
   2. Space complexity O\(1\)

### Solution

```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        List<Integer>[] bucket = new List[256];
        for (int i = 0; i < t.length(); i++) {
            char c = t.charAt(i);
            if (bucket[c] == null) bucket[c] = new ArrayList<>();
            bucket[c].add(i);
        }
        int prev = 0;
        for (char c : s.toCharArray()) {
            if (bucket[c] == null) return false;
            int j = Collections.binarySearch(bucket[c], prev);
            j = j < 0 ? -(j + 1) : j;
            if (j == bucket[c].size()) return false;
            prev = bucket[c].get(j) + 1;
        }
        return true;
    }
}
```

```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        int i = 0, j = 0;
        while (i < s.length() && j < t.length()) {
            if (s.charAt(i) == t.charAt(j)) {
                i++;
            }
            j++;
        }
        return i == s.length();
    }
}
```

```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        int prev = -1;
        for (int i = 0; i < s.length(); i++) {
            prev = t.indexOf(s.charAt(i), prev + 1);
            if (prev == -1) return false;
        }
        return true;
    }
}
```

### Additional {#additional}



