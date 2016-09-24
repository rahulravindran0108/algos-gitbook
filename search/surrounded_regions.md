## Surrounded Regions

Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

For example,
```
X X X X
X O O X
X X O X
X O X X
```

After running your function, the board should be:
```
X X X X
X X X X
X X X X
X O X X
```

### Solution

```python
class Solution(object):
    def solve(self, board):
        """
        :type board: List[List[str]]
        :rtype: void Do not return anything, modify board in-place instead.
        """
        if not any(board): return
        m, n = len(board), len(board[0])
        save = [ij for k in range(m+n) for ij in ((k, 0), (m-1,k), (0, k), (k,n-1))]
        while save:
            i, j = save.pop()
            if 0 <= i < m and 0 <= j < n  and board[i][j] == 'O':
                board[i][j] = 'S'
                save += (i-1, j), (i+1, j), (i, j-1), (i,j+1)
        board[:] = [['XO'[c == 'S'] for c in row] for row in board]
```
