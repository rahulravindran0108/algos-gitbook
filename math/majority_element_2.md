## Majority Element 2

Given an integer array of size n, find all elements that appear more than `⌊ n/3 ⌋` times. The algorithm should run in linear time and in O(1) space.

### Solution

```python
class Solution(object):
    def majorityElement(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        counts = [0, 0]
        cd = [0, 0]
        for num in nums:
            if num in cd:
                counts[cd.index(num)] += 1
            elif 0 in counts:
                cd[counts.index(0)] = num
                counts[counts.index(0)] = 1
            else:
                counts[:] = [c - 1 for c in counts]
        return [r for r in set(cd) if nums.count(r) > len(nums) // 3]
```
