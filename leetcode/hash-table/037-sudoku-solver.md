# 037-sudoku-solver

## Question {#question}

[https://leetcode.com/problems/sudoku-solver/description/](https://leetcode.com/problems/sudoku-solver/description/)

Write a program to solve a Sudoku puzzle by filling the empty cells.

Empty cells are indicated by the character`'.'`.

You may assume that there will be only one unique solution.

**Example:**

```text

```

## Thought Process {#thought-process}

1. Trial by Error and Backtrack
   1. Time complexity O\(9^m\), where m is number of blank cells
   2. Space complexity O\(m\)

## Solution

```java
class Solution {
    public void solveSudoku(char[][] board) {
        if (board == null || board.length != 9) return;
        solve(board);
    }

    private boolean solve(char[][] board) {
        for (int r = 0; r < 9; r++) {
            for (int c = 0; c < 9; c++) {
                if (board[r][c] == '.') {
                    for (char i = '1'; i <= '9'; i++) {
                        if (isValid(board, r, c, i)) {
                            board[r][c] = i;
                            if (solve(board)) return true;
                            else board[r][c] = '.';
                        }
                    }
                    return false;
                }
            }
        }
        return true;
    }

    private boolean isValid(char[][] board, int r, int c, char i) {
        for (int j = 0; j < 9; j++) {
            if (board[r][j] != '.' && board[r][j] == i) return false;
            if (board[j][c] != '.' && board[j][c] == i) return false;
            if (board[(r / 3) * 3 + j / 3][(c / 3) *3 + j % 3] != '.' && board[(r / 3) * 3 + j / 3][(c / 3) *3 + j % 3] == i) return false;
        }
        return true;
    }
}
```

## Additional {#additional}

