## Maximum Product Subarray

Find the contiguous subarray within an array (containing at least one number) which has the largest product.

For example, given the array `[2,3,-2,4]`,
the contiguous subarray [2,3] has the largest product = `6`.

### Solution

```python
import sys

class Solution(object):
    def maxProduct(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        neg, pos, max_so_far = 1, 1, -sys.maxint - 1
        for n in nums:
            neg, pos = (min(n, pos * n), neg * n) if n<= 0 else (neg * n, max(pos * n, n))
            print neg, pos
            max_so_far = max(max_so_far, pos)
        return max_so_far

```

```java
public class Solution {
    public int maxProduct(int[] nums) {
        int r = nums[0];
        int imax = nums[0], imin = nums[0];

        for(int i = 1;i < nums.length;i++) {
            if(nums[i] < 0) {
                int temp = imax;
                imax = imin;
                imin = temp;
            }

            imax = Math.max(nums[i] *  imax, nums[i]);
            imin = Math.min(nums[i], nums[i] * imin);
            r = Math.max(r, imax);
        }

        return r;
    }

}
```
