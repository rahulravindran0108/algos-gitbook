## Find Kth Largest Number

Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

For example,
```
Given [3,2,1,5,6,4] and k = 2, return 5.
```

### Solution

```python
class Solution(object):
    def findKthLargest(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: int
        """
        l = [float("-inf")] * k
        for n in nums:
            heapq.heappushpop(l, n)
        return l[0] if l[0] != float("-inf") else max(l)
```
