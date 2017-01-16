## Pacific Atlanic Ocean Follow


Given an m x n matrix of non-negative integers representing the height of each unit cell in a continent, the "Pacific ocean" touches the left and top edges of the matrix and the "Atlantic ocean" touches the right and bottom edges.

Water can only flow in four directions (up, down, left, or right) from a cell to another one with height equal or lower.

Find the list of grid coordinates where water can flow to both the Pacific and Atlantic ocean.

Note:
The order of returned grid coordinates does not matter.
Both m and n are less than 150.
Example:

Given the following 5x5 matrix:
```
  Pacific ~   ~   ~   ~   ~
       ~  1   2   2   3  (5) *
       ~  3   2   3  (4) (4) *
       ~  2   4  (5)  3   1  *
       ~ (6) (7)  1   4   5  *
       ~ (5)  1   1   2   4  *
          *   *   *   *   * Atlantic

Return:

[[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (positions with parentheses in above matrix).
```

### Solution

```python
class Solution(object):
    def pacificAtlantic(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: List[List[int]]
        """
        def fill(ocean, stack):
            while stack:
                r,c = stack.pop()
                if (r,c) in ocean:
                    continue
                ocean.add((r,c))
                stack.extend([[nr, nc] for nr, nc in [[r+1, c], [r-1, c], [r, c + 1], [r, c-1]] if 0 <= nr < m and 0 <= nc < n and matrix[r][c] <= matrix[nr][nc]])


        if not matrix:
            return []
        m, n = len(matrix), len(matrix[0])
        pset, aset = set(), set()
        pstack = [[r,0] for r in range(m)] + [[0,c] for c in range(n)]
        astack = [[m-1, c ] for c in range(n)] + [[r, n-1] for r in range(m)]

        fill(pset, pstack)
        fill(aset, astack)

        return [list(x) for x in pset & aset]

```

```java
public class Solution {
    private int [][] dirs = new int[][] {{1, 0}, {-1,0}, {0, 1}, {0, -1}};

    public List<int[]> pacificAtlantic(int[][] matrix) {
        List<int []> res = new ArrayList<>();


        if(matrix == null || matrix.length == 0  || matrix[0].length == 0)
            return res;

        int m = matrix.length, n = matrix[0].length;
        boolean [][] pacific = new boolean[m][n], atlantic = new boolean[m][n];

        for(int i = 0;i<m;i++) {
            dfs(pacific, matrix, i, 0, m, n, Integer.MIN_VALUE);
            dfs(atlantic, matrix, i, n - 1, m, n, Integer.MIN_VALUE);
        }

        for(int i = 0;i<n;i++) {
            dfs(pacific, matrix, 0, i, m, n, Integer.MIN_VALUE);
            dfs(atlantic, matrix, m - 1, i, m, n, Integer.MIN_VALUE);
        }

        for(int i = 0;i < m;i++)
            for(int j = 0;j<n;j++)
                if(pacific[i][j] && atlantic[i][j])
                    res.add(new int [] {i, j});
        return res;
    }

    public void dfs(boolean [][] visited, int [][] matrix, int i, int j, int m, int n, int height) {
        if(i < 0 || j < 0 || i >= m || j >=n || visited[i][j] || matrix[i][j] < height)
            return;
        visited[i][j] = true;
        for(int [] dir : dirs) {
            dfs(visited, matrix, i + dir[0], j + dir[1], m, n, matrix[i][j]);
        }
    }


}
```
