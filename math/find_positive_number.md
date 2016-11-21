## Find Positive Number

### Solution

```python
class Solution(object):
    def firstMissingPositive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        i, n = 0, len(nums)
        while i < n:
            if nums[i] >= 0 and nums[i] < n and nums[nums[i]] != nums[i]:
                nums[nums[i]], nums[i] = nums[i], nums[nums[i]]
            else:
                i += 1

        k = 1
        while k < n and nums[k] == k:
            k += 1

        if n == 0 or k < n:
            return k
        else:
            return k + 1 if nums[0] == k else k
```
