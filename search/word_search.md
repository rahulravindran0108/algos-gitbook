## Word Search

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

For example,
Given board =
```
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]
```
word = `"ABCCED"`, -> returns `true`,
word = `"SEE"`, -> returns `true`,
word = `"ABCB"`, -> returns `false`.

### Solution

```python
class Solution(object):
    def exist(self, board, word):
        """
        :type board: List[List[str]]
        :type word: str
        :rtype: bool
        """
        if not word:
            return True
        if not board:
            return False

        for i in range(len(board)):
            for j in range(len(board[0])):
                if self.exist_helper(board, word, i, j):
                    return True
        return False

    def exist_helper(self, board, word, i, j):
        if board[i][j] == word[0]:
            if not word[1:]:
                return True
            board[i][j] = " "
            if i > 0 and self.exist_helper(board, word[1:], i - 1, j):
                return True
            if i < (len(board) - 1) and self.exist_helper(board, word[1:], i + 1, j):
                return True
            if j < (len(board[0]) - 1) and self.exist_helper(board, word[1:], i, j + 1):
                return True
            if j > 0 and self.exist_helper(board, word[1:], i, j - 1):
                return True
            board[i][j] = word[0]
            return False

        else:
            return False


```

```java
public class Solution {
    public boolean exist(char[][] board, String word) {
        for(int i = 0;i<board.length;i++)
            for(int j = 0;j<board[0].length;j++) {
                if(board[i][j] == word.charAt(0))
                    if(isValid(board, i, j, word, 0)) return true;
            }
        return false;
    }

    boolean isValid(char [][] board, int i, int j, String word, int start) {
        if(start >= word.length()) return true;

        if(i >= board.length || i < 0 || j < 0 || j >= board[0].length)
            return false;

        if(board[i][j] == word.charAt(start++)) {
            char c = board[i][j];
            board[i][j] = '#';
            boolean res = isValid(board, i + 1, j, word, start) || isValid(board, i, j + 1, word, start) ||isValid(board, i - 1, j, word, start) || isValid(board, i, j - 1, word, start);
            board[i][j] = c;
            return res;
        }

        return false;
    }
}
```
