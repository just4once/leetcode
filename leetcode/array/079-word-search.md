# 079-word-search

## Question {#question}

[https://leetcode.com/problems/word-search/description/](https://leetcode.com/problems/word-search/description/)

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example:**

```text
Given board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
word = "ABCCED", -> returns true,
word = "SEE", -> returns true,
word = "ABCB", -> returns false.
```

## Thought Process {#thought-process}

1. Typical DFS, we can either use an array of boolean to indicate whether we have visited this cell or marked directly on the input
2. Time complexity O\(mnw\), where m is number of rows, n is number of columns, and w is length of word
3. Space complexity O\(mn\) or O\(1\) depends on separate array is used to track whether a cell is visited

## Solution

```java
class Solution {
    private int[][] dirs = { { -1, 0 }, { 1, 0 }, { 0, -1 }, { 0, 1 } };
    public boolean exist(char[][] board, String word) {
        if(board == null || word == null) return false;
        char[] chars = word.toCharArray();
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[i].length; j++){
                if(match(board, i, j, chars, 0)){
                    return true;
                }
            }
        }
        return false;
    }

    public boolean match(char[][] board, int i, int j, char[] chars, int index){
        if (index == chars.length) return true;
        if (i < 0 || i >= board.length || j < 0 || j >= board[i].length || board[i][j] != chars[index]) return false;
        board[i][j] = 0;
        boolean result = false;
        for (int[] dir : dirs) {
            result |= match(board, i + dir[0], j + dir[1], chars, index + 1);
            if (result) break;
        }
        board[i][j] = chars[index];
        return result;
    }
}
```

## Additional {#additional}

