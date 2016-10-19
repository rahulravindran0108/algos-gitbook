## Longest Consecutive Subsequence

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

For example,
Given `[100, 4, 200, 1, 3, 2]`,
The longest consecutive elements sequence is `[1, 2, 3, 4]`. Return its length: 4.

Your algorithm should run in O(n) complexity.


### Solution

```python
class Solution(object):
    def longestConsecutive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        c, best = set(nums), 0
        for n in c:
            if n -1 not in c:
                m = n+1
                while m in c:
                    m += 1
                best = max(best, m - n)
        return best
```
