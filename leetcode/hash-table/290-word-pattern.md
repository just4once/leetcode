### Question {#question}

[https://leetcode.com/problems/word-pattern/description/](https://leetcode.com/problems/word-pattern/description/)

Given a pattern and a string str, find if str follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

**Example:**

```
pattern = "abba", str = "dog cat cat dog" should return true.
pattern = "abba", str = "dog cat cat fish" should return false.
pattern = "aaaa", str = "dog cat cat dog" should return false.
pattern = "abba", str = "dog dog dog dog" should return false.
```

### Thought Process {#thought-process}

1. Hash Table
   1. Use two hash table to store the index of each character and word mapping
   2. At any time if the index are different for the same word, we know the pattern and string don't match
   3. We can take advantage of the return value of put function for java Hashmap, where it return value of the old mapping or null when the key is new
   4. Time complexity O\(n\)
   5. Space complexity O\(n\)

### Solution

```java
class Solution {
    public boolean wordPattern(String pattern, String str) {
	char[] chars = pattern.toCharArray();
	String[] strs = str.split(" ");
	if (chars.length != strs.length) return false;
	Map<Character, Integer> cmap = new HashMap<>();
	Map<String, Integer> smap = new HashMap<>();
	for (Integer i = 0; i < chars.length; i++) {
		if (cmap.put(chars[i], i) != smap.put(strs[i], i)) return false;
	}
	return true;
    }
}
```

### Additional {#additional}



