## Maximum Subarray

Find the contiguous subarray within an array (containing at least one number) which has the largest sum.

For example, given the array `[-2,1,-3,4,-1,2,1,-5,4]`,
the contiguous subarray `[4,-1,2,1]` has the largest `sum = 6`.

### Solution

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        max_sum, temp = nums[0], 0
        for i in range(0, len(nums)):
            temp = max(nums[i], nums[i] + temp)
            if temp > max_sum:
                max_sum = temp
        return max_sum
```

```java
public class Solution {
    public int maxSubArray(int[] nums) {
        int maxEndingHere = nums[0], maxSoFar = nums[0];

        for(int i = 1;i<nums.length;i++) {
            maxEndingHere = Math.max(maxEndingHere + nums[i], nums[i]);
            maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }

        return maxSoFar;

    }
}
```
