# 017-letter-combinations-of-a-phone-number

## Question {#question}

[https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/](https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/)

Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters \(just like on the telephone buttons\) is given below.

**Example:**

```text
Input:Digit string "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

## Thought Process {#thought-process}

1. Permutation
   1. 

## Solution

```java
class Solution {
    public List<String> letterCombinations(String digits) {
    LinkedList<String> result = new LinkedList<String>();
    if (digits == null || digits.length() == 0) return result;
    String[] map = {"0", "1", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    result.add("");
    result.add("");
    char[] chars = digits.toCharArray();
    for (int i = 0; i < chars.length; i++) {
        while (result.peek().length() == i) {
            String top = result.poll();
            String letters = map[chars[i] - '0'];
            for (char c : letters.toCharArray()) {
                result.add(top + c);
            }
        }
    }
    return result;
    }
}
```

## Additional {#additional}

