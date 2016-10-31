## Majority Element 1

Given an array of size n, find the majority element. The majority element is the element that appears more than `⌊ n/2 ⌋` times.

You may assume that the array is non-empty and the majority element always exist in the array.

### Solution

```python
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums:
            return 0
        cm, num = 1, nums[0]
        for i in range(1,len(nums)):
            if not cm:
                num = nums[i]
                cm = 1
            elif nums[i] == num:
                cm += 1
            else:
                cm -= 1
        return num
```
