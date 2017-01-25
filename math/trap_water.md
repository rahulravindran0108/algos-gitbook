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

```java
public class Solution {
    public int trap(int[] height) {

        if(height.length < 3) return 0;

        int l = 0, r = height.length - 1, ans = 0;
        while(l < r && height[l] <= height[l+1]) l ++;
        while(l < r && height[r] <= height[r - 1]) r--;

        while(l < r) {
            int left = height[l], right = height[r];

            if(left <= right) {
                while(l < r && left >= height[++l])
                    ans += left - height[l];
            } else {
                while(l < r && right >= height[--r])
                    ans += right - height[r];
            }
        }
        return ans;

    }
}
```
