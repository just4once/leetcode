### Question {#question}

Given two words \(beginWordandendWord\), and a dictionary's word list, find all shortest transformation sequence\(s\) frombeginWordtoendWord, such that:

1. Only one letter can be changed at a time
2. Each transformed word must exist in the word list. Note that beginWord is not a transformed word.

**Example:**

```
Given:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log","cog"]

Return
  [
    ["hit","hot","dot","dog","cog"],
    ["hit","hot","lot","log","cog"]
  ]
```

**Note:**

* Return an empty list if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume beginWord and endWord are non-empty and are not the same.

### Thought Process {#thought-process}

1. Since question ask for the shortest transformation, we need to do a breadth-first search on the word
2. For each word in the begin word set \(initially there is only one word, the beginWord\), we generate its neighbor that is valid, if it's the endWord, we finish the search
3. Otherwise continue the search, because the question wants all the possible route, we need to track of the progress using a separate array, a backtrack is useful here to retract when the word is not leading to the endWord
4. 
### Solution

```java

```

### Additional {#additional}



