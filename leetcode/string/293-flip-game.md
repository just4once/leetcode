### Question {#question}

[https://leetcode.com/problems/flip-game/description/](https://leetcode.com/problems/flip-game/description/)

You are playing the following Flip Game with your friend: Given a string that contains only these two characters: + and -, you and your friend take turns to flip two consecutive "++" into "--". The game ends when a person can no longer make a move and therefore the other person will be the winner.

Write a function to compute all possible states of the string after one valid move.

**Example:**

```
given s = "++++", after one move, it may become one of the following states:

[
  "--++",
  "+--+",
  "++--"
]

If there is no valid move, return an empty list [].
```

### Thought Process {#thought-process}

1. Check Character Pair
   1. Starting from index 1, we need to make sure the current character and previous character are both '+'
   2. We flip and add the result to the list, then reset
   3. Time complexity O\(n\)
   4. Space complexity O\(1\)

### Solution

```java
class Solution {
    public List<String> generatePossibleNextMoves(String s) {
        List<String> res = new ArrayList<>();
        char[] path = s.toCharArray();
        for (int i = 1; i < path.length; i++) {
            if (path[i - 1] == '+' && path[i] == '+') {
                path[i - 1] = path[i] = '-';
                res.add(String.valueOf(path));
                path[i - 1] = path[i] = '+';
            }
        }
        return res;
    }
}
```

### Additional {#additional}



