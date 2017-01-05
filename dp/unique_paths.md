## Unique Paths

A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

### Solution

```python
class Solution(object):
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        if m == 1 or n == 1:
            return 1

        dp = [[0 for _ in range(n)] for _ in range(m)]

        for i in range(m):
            dp[i][0] = 1
        for i in range(n):
            dp[0][i] = 1

        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i-1][j] + dp[i][j-1]
        return dp[m-1][n-1]
```

```java
public class Solution {
    public int uniquePaths(int m, int n) {
        int [][] dp = new int[m][n];
        for(int i = 0;i<m;i++)
            dp[i][0] = 1;

        for(int j = 0;j<n;j++)
            dp[0][j] = 1;

        for(int i = 1;i<m;i++)
            for(int j = 1;j<n;j++)
                dp[i][j] = dp[i-1][j] + dp[i][j-1];

        return dp[m - 1][n - 1];
    }
}
```
