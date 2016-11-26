## Sort Colors

Given an array with n objects colored red, white or blue, sort them so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

### Solution

```python
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: void Do not return anything, modify nums in-place instead.
        """
        l, r = 0, len(nums) - 1
        i = 0
        while i <= r:
            while nums[i] == 2 and i < r:
                nums[i], nums[r] = nums[r], nums[i]
                r -= 1
            while nums[i] == 0 and i > l:
                nums[i], nums[l] = nums[l], nums[i]
                l += 1
            i += 1
```
