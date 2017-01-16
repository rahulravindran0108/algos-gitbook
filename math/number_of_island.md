## Number of Island

Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:
```
11110
11010
11000
00000
```
Answer: 1

Example 2:
```
11000
11000
00100
00011
```
Answer: 3

## Solution

```python
class Solution(object):
    def numIslands(self, grid):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        if not grid:
            return 0

        m,n = len(grid), len(grid[0])
        visited, count = [[0 for _ in range(n)] for _ in range(m)], 0
        for i in range(m):
            for j in range(n):
                if grid[i][j] == "1" and visited[i][j] == 0:
                    count += 1
                    self.dfs(grid, i, j, visited, m, n)
        return count

    def dfs(self, grid, row, col, visited, m, n):
        visited[row][col] = 1
        for dx, dy in [(1,0),(-1,0), (0,1), (0,-1)]:
            nx, ny = row + dx, col + dy
            if nx >= 0 and nx < m and ny >= 0 and ny < n and grid[nx][ny] == "1" and visited[nx][ny] == 0:
                self.dfs(grid, nx, ny, visited, m, n)
```

```java
public class Solution {

    private int [][] dirs = new int[][] {{1,0}, {-1,0}, {0, 1}, {0,-1}};

    public int numIslands(char[][] grid) {
        if(grid == null || grid.length == 0)
            return 0;

        int m = grid.length, n = grid[0].length;
        int count = 0;

        for(int i = 0;i<m;i++)
            for(int j = 0;j<n;j++)
                if(grid[i][j] == '1') {
                    count += 1;
                    dfs(grid, i, j , m, n);
                }
        return count;
    }

    public void dfs(char [][] grid, int i, int j, int m, int n) {

        if(i < 0 || j < 0 || i >= m || j >= n || grid[i][j] == '0')
            return;

        grid[i][j] = '0';

        for(int [] dir : dirs) {
            dfs(grid, i + dir[0], j + dir[1], m, n);
        }
    }
    
}
```
