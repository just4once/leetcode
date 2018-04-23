### Question {#question}

[https://leetcode.com/problems/ransom-note/description/](https://leetcode.com/problems/ransom-note/description/)

Given an arbitrary ransom note string and another string containing letters from all the magazines, write a function that will return true if the ransom note can be constructed from the magazines ; otherwise, it will return false.

Each letter in the magazine string can only be used once in your ransom note.

**Example:**

```
canConstruct("a", "b") -> false
canConstruct("aa", "ab") -> false
canConstruct("aa", "aab") -> true
```

### Thought Process {#thought-process}

1. Map
   1. Use separate map to store the frequency of all characters
   2. Any time we run into character that has count == 0, we know we can't construct the note
   3. Time complexity O\(n\)
   4. Space complexity O\(256\) or O\(1\)

### Solution

```java

```

### Additional {#additional}



