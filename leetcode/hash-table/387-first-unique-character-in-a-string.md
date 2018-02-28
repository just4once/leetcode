### Question {#question}

Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

**Example:**

```
s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
```

### Thought Process {#thought-process}

1. Hash Map
   1. Store the count for each character
   2. When we first encounter a character that has 1 count, w return the index
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)
2. String index of
   1. Use indexOf and lastIndexOf function from string, if the index is the same and not -1, we know there is exactly one count for this character
   2. Time complexity O\(1\)
   3. Space complexity O\(1\)

### Solution

```java
class Solution {
    public int firstUniqChar(String s) {
        int[] counts = new int[256];
        char[] chars = s.toCharArray();
        for (int i = 0; i < chars.length; i++) {
            counts[chars[i]]++;
        }
        for (int i = 0; i < chars.length; i++) {
            if (counts[chars[i]] == 1) return i;
        }
        return -1;
    }
}
```

```java
class Solution {
    public int firstUniqChar(String s) {
        int res = s.length();
        for (char c = 'a'; c <= 'z'; c++) {
            int id = s.indexOf(c);
            if (id != -1 && id == s.lastIndexOf(c)) {
                res = Math.min(id, res);
            }
        }
        return res == s.length() ? -1 : res;
    }
}
```

### Additional {#additional}



