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

        def dfs(i, j):
            if not dp[i][j]:
                val = matrix[i][j]
                dp[i][j] = 1 + max(
                    dfs(i - 1, j) if i and val > matrix[i - 1][j] else 0,
                    dfs(i + 1, j) if i < M - 1 and val > matrix[i + 1][j] else 0,
                    dfs(i, j - 1) if j and val > matrix[i][j - 1] else 0,
                    dfs(i, j + 1) if j < N - 1 and val > matrix[i][j + 1] else 0)
            return dp[i][j]

        if not matrix or not matrix[0]: return 0
        M, N = len(matrix), len(matrix[0])
        dp = [[0] * N for i in range(M)]
        return max(dfs(x, y) for x in range(M) for y in range(N))
```

```java
public class Solution {

    public static final int [][] dirs  = {{1, 0}, {-1, 0}, {0, 1}, {0, -1}};

    public int longestIncreasingPath(int[][] matrix) {
        if(matrix.length == 0) return 0;
        int m = matrix.length, n = matrix[0].length;
        int max = 1;
        int [][] cache = new int [m][n];

        for(int i = 0;i<m;i++)
            for(int j = 0;j<n;j++) {
                int len = dfs(matrix, i, j, m , n, cache);
                if(len > max)
                    max = len;
            }
        return max;
    }

    public static int dfs(int [][] matrix, int i, int j, int m, int n, int [][] cache) {
        if(cache[i][j] != 0) return cache[i][j];
        int max = 1;
        for(int [] dir: dirs) {
            int x = i + dir[0], y = j + dir[1];

            if(x < 0 || x >= m || y >= n || y <  0 || matrix[x][y] <= matrix[i][j]) continue;
            int len = 1 + dfs(matrix, x, y, m, n , cache);
            if(len > max)
                max = len;
        }
        cache[i][j] = max;
        return max;
    }
}
```

```java
public class Solution {

    private static int [][] dirs = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};

    public int longestIncreasingPath(int[][] matrix) {
        if(matrix.length == 0) return 0;
        int m = matrix.length, n = matrix[0].length, max = 1;
        int [][] cache = new int[m][n];

        for(int i = 0;i < m;i++)
            for(int j = 0;j<n;j++) {
                int len = dfs(matrix, i, j, m, n, cache);
                max = Math.max(len, max);
            }
        return max;
    }

    public int dfs(int [][] matrix, int i, int j, int m, int n, int [][] cache) {
        if(cache[i][j] != 0) return cache[i][j];
        int max = 1;
        for(int [] dir : dirs) {
            int x = dir[0] + i, y = dir[1] + j;
            if(x < 0 || x >= m || y < 0 || y >= n || matrix[x][y] <= matrix[i][j]) continue;
            int len = 1 + dfs(matrix, x, y, m, n, cache);
            max = Math.max(max, len);
        }

        cache[i][j] = max;
        return max;

    }
}
```
