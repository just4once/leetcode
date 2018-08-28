# 125-valid-palindrome

## Question {#question}

[https://leetcode.com/problems/valid-palindrome/description/](https://leetcode.com/problems/valid-palindrome/description/)

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

**Example:**

```text
"A man, a plan, a canal: Panama" is a palindrome.
"race a car" is not a palindrome.
```

## Thought Process {#thought-process}

1. Two Pointers
   1. Having two pointer at the ends of the string, we can compare character by character
   2. Time complexity O\(n\)
   3. Space complexity O\(1\)

## Solution

```java
class Solution {
    public boolean isPalindrome(String s) {
        int i = 0, j = s.length() - 1;
        while (i < j){
            if (!Character.isLetterOrDigit(s.charAt(i))){
                i++;
            } else if (!Character.isLetterOrDigit(s.charAt(j))){
                j--;
            } else {
                if (Character.toLowerCase(s.charAt(i)) 
                    != Character.toLowerCase(s.charAt(j))) return false;
                i++;
                j--;
            }
        }
        return true;
    }
}
```

## Additional {#additional}

