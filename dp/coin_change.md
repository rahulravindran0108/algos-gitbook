## Coin Change


You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

Example 1:
```
coins = [1, 2, 5], amount = 11
return 3 (11 = 5 + 5 + 1)

Example 2:
coins = [2], amount = 3
return -1.
```

Note:
You may assume that you have an infinite number of each kind of coin.

### Solution

```python
class Solution(object):
    def coinChange(self, coins, amount):
        """
        :type coins: List[int]
        :type amount: int
        :rtype: int
        """
        need = [0] + [amount + 1] * amount
        for c in coins:
            for i in range(c, amount + 1):
                need[i] = min(need[i], need[i-c] + 1)
        return -1 if need[-1] > amount else need[-1]

```

```java
public class Solution {
    public int coinChange(int[] coins, int amount) {
        int [] dp = new int[amount +1];
        Arrays.fill(dp, Integer.MAX_VALUE);
        dp[0] = 0;

        for(int i = 1;i<=amount;i++) {
            for(int c : coins) {
                if(c <= i && dp[i - c] != Integer.MAX_VALUE)
                    dp[i] = Math.min(dp[i], 1 + dp[i - c]);
            }
        }

        return dp[amount] == Integer.MAX_VALUE ? -1 : dp[amount];
    }
}
```
