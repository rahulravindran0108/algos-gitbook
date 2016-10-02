## Jump Game

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

For example:
A = [2,3,1,1,4], return true.

A = [3,2,1,0,4], return false.

### Solution

```python
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        ldx = ndx = 0
        while ndx < len(nums) - 1:
            ldx, ndx = ndx, max(i + nums[i] for i in range(ldx, ndx + 1))
            if ldx == ndx:
                return False
        return True
```
