### Question {#question}

[https://leetcode.com/problems/unique-word-abbreviation/description/](https://leetcode.com/problems/unique-word-abbreviation/description/)

An abbreviation of a word follows the form &lt;first letter&gt;&lt;number&gt;&lt;last letter&gt;. Below are some examples of word abbreviations:

**Example:**

```
a) it                      --> it    (no abbreviation)

     1
b) d|o|g                   --> d1g

              1    1  1
     1---5----0----5--8
c) i|nternationalizatio|n  --> i18n

              1
     1---5----0
d) l|ocalizatio|n          --> l10n
```

Assume you have a dictionary and given a word, find whether its abbreviation is unique in the dictionary. A word's abbreviation is unique if no other word from the dictionary has the same abbreviation.

```
Given dictionary = [ "deer", "door", "cake", "card" ]

isUnique("dear") -> false
isUnique("cart") -> true
isUnique("cane") -> false
isUnique("make") -> true
```

### Thought Process {#thought-process}

1. Two Map
   1. Use one map to store the abbreviation and one to store the uniqueness
   2. Time complexity O\(nw\), where n is number of string and w is the average length of the word
   3. Space complexity O\(n\)

### Solution

```java
class ValidWordAbbr {
    Map<String, String> map = new HashMap<>();

    public ValidWordAbbr(String[] dictionary) {
        for (String word : dictionary) {
            String key = abbreviate(word);
            if (!map.containsKey(key)) map.put(key, word);
            else if (!map.get(key).equals(word)) map.put(key, "");
        }
    }
    
    public boolean isUnique(String word) {
        String key = abbreviate(word);
        return !map.containsKey(key) || map.get(key).equals(word);
    }
    
    private String abbreviate(String word) {
        if (word.length() <= 2) return word;
        return "" + word.charAt(0) + (word.length() - 2) + word.charAt(word.length() - 1);
    }
}

/**
 * Your ValidWordAbbr object will be instantiated and called as such:
 * ValidWordAbbr obj = new ValidWordAbbr(dictionary);
 * boolean param_1 = obj.isUnique(word);
 */
```

### Additional {#additional}



