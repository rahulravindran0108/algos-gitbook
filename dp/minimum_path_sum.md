## Minimum Path Sum

Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

### Solution

```python
class Solution(object):
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        if not grid:
            return 0

        m, n = len(grid), len(grid[0])

        for i in range(1,m):
            grid[i][0] += grid[i-1][0]

        for j in range(1,n):
            grid[0][j] += grid[0][j-1]


        for i in range(1,m):
            for j in range(1,n):
                grid[i][j] = min(grid[i-1][j], grid[i][j-1]) + grid[i][j]

        return grid[m-1][n-1]
```

```java
public class Solution {
    public int minPathSum(int[][] grid) {
        int row = grid.length, col = grid[0].length;
        int [][] dp = new int[row][col];
        dp[0][0] = grid[0][0];

        // first row
        for(int i = 1;i<col;i++)
            dp[0][i] = grid[0][i] + dp[0][i-1];

        // first col
        for(int i = 1;i<row;i++)
            dp[i][0] = grid[i][0] + dp[i-1][0];

        for(int i = 1;i<row;i++)
            for(int j = 1;j<col;j++)
                dp[i][j] = Math.min(grid[i][j] + dp[i - 1][j], grid[i][j] + dp[i][j - 1]);

        return dp[row- 1][col - 1];
    }
}
```
