## Game of Life

### Solution

```python
class Solution(object):
    def gameOfLife(self, board):
        """
        :type board: List[List[int]]
        :rtype: void Do not return anything, modify board in-place instead.
        """
        m = len(board)
        n = len(board[0]) if m else 0

        for i in range(m):
            for j in range(n):
                count = 0
                for I in range(max(i-1, 0), min(i + 2, m)):
                    for J in range(max(j-1, 0), min(j+2, n)):
                        count += board[I][J] & 1

                if (board[i][j] and count == 4) or count == 3:
                    board[i][j] |= 2

        for i in range(m):
            for j in range(n):
                board[i][j] >>= 1
```
