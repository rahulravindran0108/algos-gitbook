## Trap Water

Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

For example,
Given `[0,1,0,2,1,0,1,3,2,1,2,1]`, return `6`.
### Solution

```python
class Solution(object):
    def trap(self, height):
        """
        :type height: List[int]
        :rtype: int
        """
        l, r = 0, len(height) - 1
        level, water = 0, 0
        while l < r:
            lower = height[l] if height[l] < height[r] else height[r]
            if height[l] < height[r]:
                l+=1
            else:
                r-=1
            level = max(level, lower)
            water += level - lower
        return water
```
