### Question {#question}

[https://leetcode.com/problems/substring-with-concatenation-of-all-words/description/](https://leetcode.com/problems/substring-with-concatenation-of-all-words/description/)

You are given a string, **s**, and a list of words, **words**, that are all of the same length. Find all starting indices of substring\(s\) in **s** that is a concatenation of each word in **words** exactly once and without any intervening characters.

**Example:**

```
s: "barfoothefoobarman"
words: ["foo", "bar"]

You should return the indices: [0,9].
```

### Thought Process {#thought-process}

1. Brute Force
   1. We simply break the string at different point to make the substring the length of total length of words
   2. Time complexity O\(nmw\), where n is length of string, m is number of words, and w is length of word
   3. Space complexity O\(mw\)
2. Split based on Word length
   1. If we observed closely, we have done a lot of repeated word check
   2. There are only w possible cut on the string, meaning the 0th to \(w - 1\)th position, where w is the length of the word
   3. Time complexity O\(n\)
   4. Space complexity O\(n\)

### Solution

```java
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        // this question is very similiar to slinding window for single letter, we
        // can see the entire word as one letter and slide the window appropiately
        List<Integer> res = new ArrayList<>();
        if (s == null || words == null || words.length == 0) return res;
        int n = s.length(), m = words.length, w = words[0].length();
        int totalLen = m * w;
        if (n < totalLen) return res;
        // record the count for each word
        Map<String, Integer> counts = new HashMap<>();
        for (String word : words) {
            counts.put(word, counts.getOrDefault(word, 0) + 1);
        }
        for (int i = 0; i <= n - totalLen; i++) {
            String sub = s.substring(i, i + totalLen);
            int lo = i , hi = i + totalLen - w;
            Map<String, Integer> map = new HashMap<>(counts);
            while (lo <= hi) {
                String word = s.substring(lo, lo + w);
                if (map.getOrDefault(word, 0) <= 0) break;
                else map.put(word, map.get(word) - 1);
                lo += w;
            }
            if (lo == i + totalLen) res.add(i);
        }
        return res;
    }
}
```

```java
class Solution {
    public List<Integer> findSubstring(String s, String[] words) {
        // this question is very similiar to slinding window for single letter, we
        // can see the entire word as one letter and slide the window appropiately
        List<Integer> res = new ArrayList<>();
        if (s == null || words == null || words.length == 0) return res;
        int n = s.length(), m = words.length, w = words[0].length();
        int totalLen = m * w;
        if (n < totalLen) return res;
        // record the count for each word
        Map<String, Integer> counts = new HashMap<>();
        for (String word : words) {
            counts.put(word, counts.getOrDefault(word, 0) + 1);
        }
        // There are only w position to cut t
        for (int i = 0; i < w; i++) {
            int left = i, right = i;
            int window = 0;
            // while we still have enough characters for string
            while (left + (m - window) * w <= n && right + w <= n) {
                String cur = s.substring(right, right + w);
                if (counts.containsKey(cur)) {
                    int count = counts.get(cur);
                    window++;
                    if (count > 0) {
                        counts.put(cur, count - 1);
                    } else {
                        String removed = s.substring(left, left + w);
                        while (!removed.equals(cur)) {
                            counts.put(removed, counts.get(removed) + 1);
                            left += w;
                            window--;
                            removed = s.substring(left, left + w);
                        }
                        left += w;
                        window--;
                    }
                    if (window == m) res.add(left);
                // reset if we dont have such word
                } else {
                    while (left < right) {
                        String removed = s.substring(left, left + w);
                        counts.put(removed, counts.get(removed) + 1);
                        left += w;
                        window--;
                    }
                    left += w;
                }
                right += w;
            }
            while (left < right) {
                String removed = s.substring(left, left + w);
                counts.put(removed, counts.get(removed) + 1);
                left += w;
            }
        }
        return res;
    }
}
```

### Additional {#additional}



