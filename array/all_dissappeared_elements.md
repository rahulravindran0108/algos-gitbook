## Find All Numbers Disappeared in an Array
Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements of [1, n] inclusive that do not appear in this array.

Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

Example:
```
Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]
```

### Solution

```python
class Solution(object):
    def findDisappearedNumbers(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        for i in range(len(nums)):
            index = abs(nums[i]) - 1
            nums[index] = -nums[index] if nums[index] > 0 else nums[index]

        result = []
        for i in range(len(nums)):
            if nums[i] > 0:
                result.append(i + 1)
        return result
```

```java
public class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        ArrayList<Integer> result = new ArrayList<Integer>();

        for(int i: nums) {
            int index = Math.abs(i) - 1;
            nums[index] = nums[index] > 0 ? -nums[index] : nums[index];
        }

        for(int i=0;i < nums.length;i++) {
            if(nums[i] > 0)
                result.add(i+1);
        }
        return result;
    }
}
```
