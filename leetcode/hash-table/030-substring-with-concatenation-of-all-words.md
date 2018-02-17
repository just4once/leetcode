### Question {#question}

You are given a string, **s**, and a list of words, **words**, that are all of the same length. Find all starting indices of substring\(s\) in **s** that is a concatenation of each word in **words** exactly once and without any intervening characters.

**Example:**

```
s: "barfoothefoobarman"
words: ["foo", "bar"]

You should return the indices: [0,9].
```

### Thought Process {#thought-process}

1. Brute Force
   1. We simply break 
2. asd

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

### Additional {#additional}



