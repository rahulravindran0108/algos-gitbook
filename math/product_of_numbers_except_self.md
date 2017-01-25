## Product of Numbers Except self

Given an array of n integers where n > 1, nums, return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

Solve it without division and in O(n).

For example, given `[1,2,3,4]`, return `[24,12,8,6].`

### Solution

```python
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        output = [1] * len(nums)
        left, right = 1, 1
        for i in range(len(nums) - 1):
            left *= nums[i]
            output[i + 1] = left

        for i in range(len(nums) - 1, 0, -1):
            right *= nums[i]
            output[i-1] *= right
        return output
```

```java
public class Solution {
    public int[] productExceptSelf(int[] nums) {

        int n = nums.length;
        int [] res = new int[n];

        res[0] = 1;

        for(int i = 1;i<n;i++)
            res[i] = res[i-1] * nums[i - 1];

        int right = 1;

        for(int i = n - 1; i >=0; i--) {
            res[i] = res[i] * right;
            right *= nums[i];
        }

        return res;
    }
}
```
