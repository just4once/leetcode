### Question {#question}

[https://leetcode.com/problems/text-justification/description/](https://leetcode.com/problems/text-justification/description/)

Given an array of words and a length L, format the text such that each line has exactly L characters and is fully \(left and right\) justified.

You should pack your words in a greedy approach; that is, pack as many words as you can in each line. Pad extra spaces ' ' when necessary so that each line has exactly L characters.

Extra spaces between words should be distributed as evenly as possible. If the number of spaces on a line do not divide evenly between words, the empty slots on the left will be assigned more spaces than the slots on the right.

For the last line of text, it should be left justified and no extra space is inserted between words.

**Example:**

```
words: ["This", "is", "an", "example", "of", "text", "justification."]
L: 16.

Return the formatted lines as:
[
   "This    is    an",
   "example  of text",
   "justification.  "
]
```

### Thought Process {#thought-process}

1. Char Array
   1. For every line, we try to accommodate as many string as possible
   2. Then we count the total length of the words and use desired length to get the correct spacing
   3. Using L - totalLength / \(numberOfWords - 1\), we can determine how much space we need to add to each spacing
   4. Time complexity O\(n\)
   5. Space complexity O\(mL\), where m is the maxWidth, L is number of lines and approximately equals to nw / 16

### Solution

```java

```

### Additional {#additional}



