##  Best Time to Buy and Sell Stock

Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.
```
Example 1:
Input: [7, 1, 5, 3, 6, 4]
Output: 5
max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
```

Example 2:
```
Input: [7, 6, 4, 3, 1]
Output: 0
```

In this case, no transaction is done, i.e. max profit = 0.

### Solution

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if not prices or len(prices) == 1:
            return 0
        min_p, profit = prices[0], 0
        for i in range(1,len(prices)):
            profit = max(profit, prices[i] - min_p)
            min_p = min(min_p, prices[i])
        return profit
```

```java
public class Solution {
    public int maxProfit(int[] prices) {
        if(prices.length <2)
            return 0;

        int maxProfit = 0, minPrice = prices[0];
        for(int i = 1;i< prices.length;i++) {
            maxProfit = Math.max(maxProfit, prices[i] - minPrice);
            minPrice = Math.min(minPrice, prices[i]);
        }

        return maxProfit;
    }
}
```
