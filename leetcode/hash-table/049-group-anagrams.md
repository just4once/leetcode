### Question {#question}

Given an array of strings, group anagrams together.

**Example:**

```
For example, given: ["eat", "tea", "tan", "ate", "nat", "bat"], 
Return:

[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

### Thought Process {#thought-process}

1. Sort the character in Key
   1. Time complexity O\(n w logw\), where n is number of words, and w is the average length of w
   2. Space complexity O\(n\)
2. Key Hashing using Prime
   1. We

### Solution

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> res = new ArrayList<>();
        Map<String, List<String>> map = new HashMap<>();
        for (String str : strs) {
            char[] chars = str.toCharArray();
            Arrays.sort(chars);
            map.computeIfAbsent(String.valueOf(chars), k -> new ArrayList<>()).add(str);
        }
        res.addAll(map.values());
        return res;
    }
}
```

```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        int[] primes = {2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37, 41, 43, 47, 53, 59, 61, 67, 71, 73, 79, 83, 89, 97, 101};
        List<List<String>> res = new ArrayList<>();
        Map<Integer, List<String>> map = new HashMap<>();
        for (String str : strs) {
            int key = 1;
            for (char c : str.toCharArray()) {
                key *= primes[c - 'a'];
            }
            if (!map.containsKey(key)) map.put(key, new ArrayList<>());
            map.get(key).add(str);
        }
        res.addAll(map.values());
        return res;
    }
}
```

### Additional {#additional}



