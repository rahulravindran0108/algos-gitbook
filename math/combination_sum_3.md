## Combination Sum 3

Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

```
Example 1:

Input: k = 3, n = 7

Output:

[[1,2,4]]

Example 2:

Input: k = 3, n = 9

Output:

[[1,2,6], [1,3,5], [2,3,4]]
```

### Solution

```python
class Solution(object):
    def combinationSum3(self, k, n):
        """
        :type k: int
        :type n: int
        :rtype: List[List[int]]
        """
        res = []
        self.dfs(xrange(1,10), k, n, 0, [], res)
        return res

    def dfs(self, nums, k, n , index, path, res):
        if k < 0 or n < 0:
            return
        if k == 0 and n == 0:
            res.append(path)
        for i in xrange(index, len(nums)):
            self.dfs(nums, k - 1, n - nums[i], i + 1, path + [nums[i]], res)
```
