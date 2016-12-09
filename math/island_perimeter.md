## Island Permiter


### Solution

```java
public class Solution {
    public int islandPerimeter(int[][] grid) {
        int numberOfIslands = 0, nb = 0;

        for(int i = 0;i < grid.length; i ++)
            for(int j = 0; j < grid[0].length;j++) {
                if(grid[i][j] == 1) {
                    numberOfIslands ++;
                    if(i <  grid.length - 1 && grid[i+1][j] == 1) nb += 1;
                    if(j < grid[i].length - 1 && grid[i][j+1] == 1) nb += 1;
                }
            }

        return numberOfIslands * 4 - nb * 2;
    }
}
```
