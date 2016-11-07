## Spiral Matrix 2

Given an integer n, generate a square matrix filled with elements from 1 to n2 in spiral order.

```
For example,
Given n = 3,

You should return the following matrix:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

### Solution

```python
class Solution(object):
    def generateMatrix(self, n):
        """
        :type n: int
        :rtype: List[List[int]]
        """
        if not n:
            return []
        matrix = [[-1000 for _ in range(n)] for _ in range(n)]
        i, j, di, dj  = 0, 0, 0, 1
        for x in range(1, n * n + 1):
            matrix[i][j] = x
            if matrix[(i + di) % n][(j + dj) % n] != -1000:
                di, dj = dj, -di
            i += di
            j += dj
        return matrix

```
