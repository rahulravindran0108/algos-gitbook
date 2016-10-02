## Jump Game 2

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

For example:
Given array A = `[2,3,1,1,4]`

The minimum number of jumps to reach the last index is `2`. (Jump 1 step from index 0 to 1, then 3 steps to the last index.)

### Solution

```python
class Solution(object):
    def jump(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) <= 1:
            return 0
        ans = l_idx = n_idx = 0
        while n_idx < len(nums) - 1:
            ans += 1
            l_idx, n_idx = n_idx, max(i + nums[i] for i in range(l_idx, n_idx+1))
        return ans

```
