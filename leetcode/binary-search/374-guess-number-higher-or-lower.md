# 374-guess-number-higher-or-lower

## Question {#question}

[https://leetcode.com/problems/guess-number-higher-or-lower/description/](https://leetcode.com/problems/guess-number-higher-or-lower/description/)

We are playing the Guess Game. The game is as follows:

I pick a number from 1 to n. You have to guess which number I picked.

Every time you guess wrong, I'll tell you whether the number is higher or lower.

You call a pre-defined API guess\(int num\) which returns 3 possible results \(-1, 1, or 0\):

```text
-1 : My number is lower
 1 : My number is higher
 0 : Congrats! You got it!
```

**Example:**

```text
n = 10, I pick 6.

Return 6.
```

## Thought Process {#thought-process}

1. Binary Search
   1. Very Typical binary search, where we return when we get 0, search the lower half when we got -1 \(the solution is lower\), otherwise we search the higher half
   2. Time complexity O\(nlogn\)
   3. Space complexity O\(1\)

## Solution

```java
/* The guess API is defined in the parent class GuessGame.
   @param num, your guess
   @return -1 if my number is lower, 1 if my number is higher, otherwise return 0
      int guess(int num); */

public class Solution extends GuessGame {
    public int guessNumber(int n) {
        int lo = 0, hi = n;
        int mid;
        while (lo <= hi) {
            mid = lo + (hi - lo)/2;
            int g = guess(mid);
            if (g == 0) return mid;
            else if (g > 0) lo = mid + 1;
            else hi = mid - 1;
        }
        return -1;
    }
}
```

## Additional {#additional}

