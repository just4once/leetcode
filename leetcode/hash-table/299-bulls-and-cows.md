# 299-bulls-and-cows

## Question {#question}

[https://leetcode.com/problems/bulls-and-cows/description/](https://leetcode.com/problems/bulls-and-cows/description/)

You are playing the following [Bulls and Cows](https://en.wikipedia.org/wiki/Bulls_and_Cows) game with your friend: You write down a number and ask your friend to guess what the number is. Each time your friend makes a guess, you provide a hint that indicates how many digits in said guess match your secret number exactly in both digit and position \(called "bulls"\) and how many digits match the secret number but locate in the wrong position \(called "cows"\). Your friend will use successive guesses and hints to eventually derive the secret number.

**Example:**

```text
Secret number:  "1807"
Friend's guess: "7810"

Hint: 1 bull and 3 cows. (The bull is 8, the cows are 0, 1 and 7.)
```

Write a function to return a hint according to the secret number and friend's guess, use A to indicate the bulls and B to indicate the cows. In the above example, your function should return "1A3B".

Please note that both secret number and friend's guess may contain duplicate digits, for example:

```text
Secret number:  "1123"
Friend's guess: "0111"
```

In this case, the 1st 1 in friend's guess is a bull, the 2nd or 3rd 1 is a cow, and your function should return "1A1B".

You may assume that the secret number and your friend's guess only contain digits, and their lengths are always equal.

## Thought Process {#thought-process}

1. Hash Table - Two pass
   1. Use two hash table to record the character count from 0 - 9, and another variable to track the number of match
   2. In the second pass, we can compare the count from secret and guess, and the minimum will be the number of cows
   3. Time complexity O\(n\)
   4. Space complexity O\(n\) or O\(1\), depends on if we use extra array to store the character
2. Hash Table - Single pass
   1. Using one hash table to record the count, we need to be smart about the way we record the count
   2. We increase the count, when we see this character from the secret, meaning we have extra left, decrease the count when we see the character from the guess, meaning we used up the extra
   3. Now the cow can be increased when the count for character from secret is negative, because previous encountering of same character from guess desire the extra copy and decrease the count, opposite thing happens for guess
   4. Time complexity O\(n\)
   5. Space complexity O\(n\) or O\(1\), depends on if we use extra array to store character

## Solution

```java
class Solution {
    public String getHint(String secret, String guess) {
        int n = secret.length();
        char[] sc = secret.toCharArray(), gc = guess.toCharArray();
        int bull = 0, cow = 0;
        int[] sCount = new int[10];
        int[] gCount = new int[10];
        for (int i = 0; i < n; i++) {
            if (sc[i] == gc[i]) {
                bull++;
            } else {
                sCount[sc[i] - '0']++;
                gCount[gc[i] - '0']++;
            }
        }
        for (int i = 0; i < sCount.length; i++) {
            cow += Math.min(sCount[i], gCount[i]);
        }
        return bull + "A" + cow + "B";
    }
}
```

```java
class Solution {
    public String getHint(String secret, String guess) {
        int n = secret.length();
        char[] sc = secret.toCharArray(), gc = guess.toCharArray();
        int bull = 0, cow = 0;
        int[] count = new int[10];
        for (int i = 0; i < n; i++) {
            if (sc[i] == gc[i]) {
                bull++;
            } else {
                if (count[sc[i] - '0'] < 0) cow++;
                if (count[gc[i] - '0'] > 0) cow++;
                count[sc[i] - '0']++;
                count[gc[i] - '0']--;
            }
        }
        return bull + "A" + cow + "B";
    }
}
```

## Additional {#additional}

