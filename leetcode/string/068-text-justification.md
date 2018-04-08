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
class Solution {
    public List<String> fullJustify(String[] words, int maxWidth) {
        List<String> res = new LinkedList<>();
        int i = 0, len = 0, space = -1;
        while (i < words.length) {
            if (len + space <= maxWidth) {
                space++;
                len += words[i].length();
                i++;
            } else {
                addLine(res, words, i - space - 1, i - 2, maxWidth, len - words[i - 1].length(), space - 1);
                i--;
                len = 0;
                space = -1;
            }  
        }
        // System.out.println("second last");
        if (len + space > maxWidth) {
            addLine(res, words, i - space - 1, i - 2, maxWidth, len - words[i - 1].length(), space - 1);
            addLine(res, words, i - 1, i - 1, maxWidth, words[i - 1].length(), 1);
        } else {
            addLine(res, words, i - space - 1, i - 1, maxWidth, len, maxWidth- len);
        }
        return res;
    }
    
    private void addLine(List<String> res, String[] words, int lo, int hi, int maxWidth, int len, int space) {
        // System.out.println("lo = " + lo + ", hi = " + hi +", len = " + len + ", space = " + space);
        if (lo > hi) return;
        if (space < 1) space = 1;
        int pad = (maxWidth - len) / space;
        int extra = (maxWidth - len) % space;
        StringBuilder sb = new StringBuilder(words[lo++]);
        while (lo <= hi) {
            for (int i = 0; i < pad; i++) sb.append(' ');
            if (extra-- > 0) sb.append(' ');
            sb.append(words[lo++]);
        }
        while (sb.length() < maxWidth) sb.append(' ');
        res.add(sb.toString());
    }
}
```

### Additional {#additional}



