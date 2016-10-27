## Minimum Size Subarray Sum

Given an array of n positive integers and a positive integer s, find the minimal length of a subarray of which the sum ≥ s. If there isn't one, return 0 instead.

For example, given the array [2,3,1,2,4,3] and s = 7,
the subarray [4,3] has the minimal length under the problem constraint.

## Solution

```python
class Solution(object):
    def minSubArrayLen(self, s, nums):
        """
        :type s: int
        :type nums: List[int]
        :rtype: int
        """
        count, i, j, res = 0, 0, 0, float("inf")
        for j in range(len(nums)):
            count += nums[j]
            while i <= j and count >= s:
                res, count, i = min(res, j - i + 1), count - nums[i], i + 1
        return res if res < float("inf") else 0
```
