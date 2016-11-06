## Valid Sudoku

Determine if a Sudoku is valid, according to: Sudoku Puzzles - The Rules.

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

### Solution

```python
class Solution(object):
    def isValidSudoku(self, board):
        """
        :type board: List[List[str]]
        :rtype: bool
        """
        res = set()
        for row in range(len(board)):
            for col in range(len(board[0])):
                if board[row][col] == ".":
                    continue
                num = board[row][col]

                if (row, 'row', num) in res:
                    return False
                else:
                    res.add((row, 'row', num))

                if (col,'col',num) in res:
                    return False
                else: res.add((col, 'col', num))

                if (row//3, col//3, num) in res:
                    return False
                else:
                    res.add((row//3, col//3,num))
        return True
```
