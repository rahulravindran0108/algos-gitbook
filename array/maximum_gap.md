## Maximum Gap

### Solution

```python
class Solution(object):
    def maximumGap(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums)<2:
            return 0
        max_num = max(nums)
        min_num = min(nums)
        max_gap = (max_num - min_num) // (len(nums) - 1)
        b_size = max_gap + 1
        buckets = [[] for _ in range((max_num-min_num)//b_size+1)]
        for n in nums:
            buckets[(n-min_num)//b_size].append(n)
        # print buckets
        buckets = [b for b in buckets if b]
        max_gap = 0
        if len(buckets) >= 1:
            max_gap = max(buckets[0]) - min(buckets[0])

        for i in range(1,len(buckets)):
            max_gap = max(max_gap, min(buckets[i]) - max(buckets[i-1]))
        return max_gap
            
```
