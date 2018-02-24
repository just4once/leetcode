### Question {#question}

[https://leetcode.com/problems/group-shifted-strings/description/](https://leetcode.com/problems/group-shifted-strings/description/)

Given a string, we can "shift" each of its letter to its successive letter, for example: "abc" -&gt; "bcd". We can keep "shifting" which forms the sequence:

"abc" -&gt; "bcd" -&gt; ... -&gt; "xyz"

Given a list of strings which contains only lowercase alphabets, group all strings that belong to the same shifting sequence.

**Example:**

```
For example, given: ["abc", "bcd", "acef", "xyz", "az", "ba", "a", "z"], 
A solution is:
[
  ["abc","bcd","xyz"],
  ["az","ba"],
  ["acef"],
  ["a","z"]
]
```

### Thought Process {#thought-process}

1. Hash Table - Normalized Key
   1. Using the first character as gauge and make the first character 'a', and normalize the rest of characters accordingly
   2. Time complexity O\(nw\), where n is number of word, w is the average width of the word
   3. Space complexity O\(nw\)

### Solution

```java
class Solution {
    public List<List<String>> groupStrings(String[] strings) {
        List<List<String>> res = new ArrayList<>();
        if (strings == null || strings.length == 0) return res;
        Map<String, List<String>> map = new HashMap<>();
        for (String str : strings) {
            String key = normalize(str);
            if (!map.containsKey(key)) map.put(key, new ArrayList<>());
            map.get(key).add(str);
        }
        res.addAll(map.values());
        return res;
    }

    private String normalize(String s) {
        if (s.length() == 0 || s.charAt(0) == 'a') return s;
        char[] chars = s.toCharArray();
        int diff = chars[0] - 'a';
        for (int i = 0; i < chars.length; i++) {
            chars[i] -= diff;
            if (chars[i] < 'a') chars[i] += 26;
        }
        return String.valueOf(chars);
    }
}
```

### Additional {#additional}



