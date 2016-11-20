## Summary Ranges

Given a sorted integer array without duplicates, return the summary of its ranges.

For example, given [0,1,2,4,5,7], return ["0->2","4->5","7"].

### Solution

```python
class Solution(object):
    def summaryRanges(self, nums):
        """
        :type nums: List[int]
        :rtype: List[str]
        """
        if not nums:
            return []
        prev,init, res = nums[0], nums[0], []
        for i in range(1, len(nums)):
            if nums[i] != prev + 1:
                if prev == init:
                    res.append( str(init) if prev == init else str(init)+"->"+str(prev) )
                init = nums[i]
            prev = nums[i]
        # process last one
        res.append(str(init) + "->" + str(nums[-1]) if init != nums[-1] else str(nums[-1]))
        return res

```
