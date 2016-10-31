## Contains Duplicate 2

Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that nums[i] = nums[j] and the difference between i and j is at most k.

### Solution

```python
class Solution(object):
    def containsNearbyDuplicate(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: bool
        """
        lookup = dict()
        for idx, value in enumerate(nums):
            if value not in lookup:
                lookup[value] = idx
            else:
                if idx - lookup[value] <= k:
                    return True
                lookup[value] = idx
        return False
```
