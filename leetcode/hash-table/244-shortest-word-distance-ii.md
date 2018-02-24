### Question {#question}

[https://leetcode.com/problems/shortest-word-distance-ii/description/](https://leetcode.com/problems/shortest-word-distance-ii/description/)

This is a **follow up **of [Shortest Word Distance](https://leetcode.com/problems/shortest-word-distance). The only difference is now you are given the list of words and your method will be called \_repeatedly \_many times with different parameters. How would you optimize it?

Design a class which receives a list of words in the constructor, and implements a method that takes two words \_word1 \_and \_word2 \_and return the shortest distance between these two words in the list.

**Example:**

```
Assume that words = ["practice", "makes", "perfect", "coding", "makes"].

Given word1 = “coding”, word2 = “practice”, return 3.
Given word1 = "makes", word2 = "coding", return 1.
```

**Note:  
**

You may assume that word1 does not equal to word2, and word1 and word2 are both in the list.

### Thought Process {#thought-process}

1. Hash Table
   1. Save the index to the array list and loop through both arrays to find the shortest distance
   2. Time complexity O\(m + n\) for shortest function
   3. Space complexity O\(n\)

### Solution

```java
class WordDistance {
    Map<String, List<Integer>> str2id;

    public WordDistance(String[] words) {
        str2id = new HashMap<>();
        for (int i = 0; i < words.length; i++) {
            if (!str2id.containsKey(words[i])) str2id.put(words[i], new ArrayList<>());
            str2id.get(words[i]).add(i);
        }
    }

    public int shortest(String word1, String word2) {
        List<Integer> l1 = str2id.get(word1), l2 = str2id.get(word2);
        int i = 0, j = 0;
        int m = l1.size(), n = l2.size();
        int min = Integer.MAX_VALUE;
        while (i < m && j < n) {
            int id1 = l1.get(i), id2 = l2.get(j);
            min = Math.min(min, Math.abs(id1 - id2));
            if (id1 < id2) i++;
            else j++;
        }
        return min;
    }
}

/**
 * Your WordDistance object will be instantiated and called as such:
 * WordDistance obj = new WordDistance(words);
 * int param_1 = obj.shortest(word1,word2);
 */
```

### Additional {#additional}



