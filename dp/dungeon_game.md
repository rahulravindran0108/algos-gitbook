## Dungeon Game


The demons had captured the princess (P) and imprisoned her in the bottom-right corner of a dungeon. The dungeon consists of M x N rooms laid out in a 2D grid. Our valiant knight (K) was initially positioned in the top-left room and must fight his way through the dungeon to rescue the princess.

The knight has an initial health point represented by a positive integer. If at any point his health point drops to 0 or below, he dies immediately.

Some of the rooms are guarded by demons, so the knight loses health (negative integers) upon entering these rooms; other rooms are either empty (0's) or contain magic orbs that increase the knight's health (positive integers).

In order to reach the princess as quickly as possible, the knight decides to move only rightward or downward in each step.


Write a function to determine the knight's minimum initial health so that he is able to rescue the princess.

For example, given the dungeon below, the initial health of the knight must be at least 7 if he follows the optimal path `RIGHT-> RIGHT -> DOWN -> DOWN.`

### Solution

```python
import sys

class Solution(object):
    def calculateMinimumHP(self, dungeon):
        """
        :type dungeon: List[List[int]]
        :rtype: int
        """
        m, n = len(dungeon), len(dungeon[0])
        dp = [sys.maxint for _ in range(n)]
        dp[-1] = 0 if dungeon[-1][-1] > 0 else -dungeon[-1][-1]

        for i in range(m-1,-1,-1):
            for j in range(n-1,-1,-1):
                if j == n-1 and i == m-1:
                    continue
                right = dp[j+1] if j + 1 < n else sys.maxint
                down = dp[j]
                dp[j] = 0 if dungeon[i][j] - min(right, down) >= 0 else -dungeon[i][j] + min(right, down)
        # print dp
        return dp[0]+1

```

```java
public class Solution {
    public int calculateMinimumHP(int[][] dungeon) {
        int row = dungeon.length;
        int col = dungeon[0].length;

        int [][] dp = new int[row][col];

        dp[row - 1][col-1]  = dungeon[row - 1][col - 1] < 0 ? 1 - dungeon[row - 1][col - 1] : 1;


        // last column
        for(int i = row - 2; i>=0;i--)
            dp[i][col - 1] = compute(dungeon[i][col-1], dp[i+1][col - 1]);

        // last row
        for(int j = col - 2; j >=0; j--)
            dp[row-1][j] = compute(dungeon[row - 1][j], dp[row-1][j + 1]);

        // compute for the rest
        for(int i = row - 2;i >=0;i--)
            for(int j = col - 2;j>=0;j--)
                dp[i][j] = Math.min(compute(dungeon[i][j], dp[i+1][j]), compute(dungeon[i][j], dp[i][j+1]));

        return dp[0][0];
    }

    public int compute(int cur, int pre) {
        if(cur == 0)
            return pre;
        if(cur > 0 && cur >= pre)
            return 1;
        return pre - cur;
    }
}
```
