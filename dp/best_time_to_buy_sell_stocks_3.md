## Best Time to Buy Sell Stocks 3

Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note:
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

### Solution

```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        if len(prices) == 0:
            return 0

        left = [0 for i in range(len(prices))]
        right = [0 for i in range(len(prices))]
        mi, ma = prices[0], prices[-1]

        for i in range(1, len(prices)):
            mi = min(mi, prices[i])
            left[i] = max(left[i-1], prices[i] - mi)

        for i in range(len(prices) - 2, -1, -1):
            ma = max(ma, prices[i])
            right[i] = max(right[i+1], ma - prices[i])

        profit = 0
        for i in range(len(prices)):
            profit = max(profit, left[i] + right[i])
        return profit
```
