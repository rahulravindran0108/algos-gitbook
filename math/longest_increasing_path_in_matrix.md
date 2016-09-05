## Longest Increasing Path in a Matrix


Given an integer matrix, find the length of the longest increasing path.

From each cell, you can either move to four directions: left, right, up or down. You may NOT move diagonally or move outside of the boundary (i.e. wrap-around is not allowed).

Example 1:
```
nums = [
  [9,9,4],
  [6,6,8],
  [2,1,1]
]
```
Return 4
The longest increasing path is [1, 2, 6, 9].

Example 2:
```
nums = [
  [3,4,5],
  [3,2,6],
  [2,2,1]
]
```
Return 4
The longest increasing path is [3, 4, 5, 6]. Moving diagonally is not allowed.

### Solution

```python
class Solution(object):
    def longestIncreasingPath(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: int
        """
        if not matrix:
            return 0
        m,n = len(matrix), len(matrix[0])
        dis = [[0 for j in xrange(n)] for i in xrange(m)]
        return max([self.dfs(m, n, i, j, matrix, dis) for j in xrange(n) for i in range(m)])

    def dfs(self, m, n, x, y, matrix, dis):
        if dis[x][y]: return dis[x][y]

        for dx, dy in [(1,0),(-1,0),(0,1),(0,-1)]:
            nx, ny = x+dx, y+dy

            if nx >=0 and nx <m and ny >=0 and ny <n and matrix[x][y] < matrix[nx][ny]:
                dis[x][y] = max(dis[x][y], self.dfs( m, n, nx, ny, matrix, dis))
        dis[x][y] += 1
        return dis[x][y]
```
