## Unique Paths 2

Follow up for "Unique Paths":

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

For example,
There is one obstacle in the middle of a 3x3 grid as illustrated below.
```
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
```

The total number of unique paths is 2.

### Solution

```python
class Solution(object):
    def uniquePathsWithObstacles(self, obstacleGrid):
        """
        :type obstacleGrid: List[List[int]]
        :rtype: int
        """
        m, n = len(obstacleGrid), len(obstacleGrid[0])
        dp = [[0 for _ in range(n)] for _ in range(m)]

        dp[0][0] = 0 if obstacleGrid[0][0] == 1 else 1

        for i in range(1,m):
            if dp[i-1][0] == 0:
                dp[i][0] = 0
            else:
                dp[i][0] = 1 if obstacleGrid[i][0] == 0 else 0

        for i in range(1,n):
            if dp[0][i-1] == 0:
                dp[0][i] = dp[0][i-1]
            else:
                dp[0][i] = 1 if obstacleGrid[0][i] == 0 else 0
        for i in range(1, m):
            for j in range(1, n):
                if obstacleGrid[i][j] == 0:
                    dp[i][j] = dp[i-1][j] + dp[i][j-1]
        return dp[m-1][n-1]
```
