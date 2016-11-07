## Spiral Matrix

Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

For example,
Given the following matrix:
```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
You should return [1,2,3,6,9,8,7,4,5].
```

### Solution

```python
class Solution(object):
    def spiralOrder(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[int]
        """
        res = []
        if not matrix:
            return res
        i, j, di, dj = 0, 0, 0, 1
        m, n  = len(matrix), len(matrix[0])

        for x in range(m * n):
            res.append(matrix[i][j])
            matrix[i][j] = ""
            if matrix[(i + di) % m][(j + dj) % n] == "":
                di, dj = dj, -di
            i += di
            j += dj
        return res
```
