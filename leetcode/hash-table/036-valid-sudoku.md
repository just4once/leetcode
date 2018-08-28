# 036-valid-sudoku

## Question {#question}

[https://leetcode.com/problems/valid-sudoku/description/](https://leetcode.com/problems/valid-sudoku/description/)

Determine if a Sudoku is valid, according to: [Sudoku Puzzles - The Rules](http://sudoku.com.au/TheRules.aspx).

The Sudoku board could be partially filled, where empty cells are filled with the character`'.'`.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Follow the rule
   1. We simply follow the rule of the Sudoku, where we check all the row, column and boxes
   2. Time complexity O\(n^2\), where n = 9 for common Sudoku
   3. Space complexity O\(1\)

## Solution

```java
class Solution {
    public boolean isValidSudoku(char[][] board) {
        for (int i = 0; i < 9; i++) {
        if (!isValid(board, i, i, 0, 8)) return false;
        if (!isValid(board, 0, 8, i, i)) return false;
        if (!isValid(board, (i / 3) * 3, (i / 3) * 3 + 2, (i % 3) * 3, (i % 3) * 3 + 2)) return false;
    }
    return true;
    }

    public boolean isValid(char[][] board, int rStart, int rEnd, int cStart, int cEnd){
        boolean[] contain = new boolean[9];
        for (int row = rStart; row <= rEnd; row++) {
            for (int col = cStart; col <= cEnd; col++) {
                char c = board[row][col];
                if(c != '.'){
                    if(contain[c - '1']) return false;
                    else contain[c - '1'] = true;
                }
            }
        }
        return true;
    }
}
```

## Additional {#additional}

