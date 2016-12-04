## All Duplicates in Array

Given an array of integers, 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements that appear twice in this array.

Could you do it without extra space and in O(n) runtime?

Example:
```
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]
```

### Solution

```python
class Solution(object):
    def findDuplicates(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """
        result = []
        for i in range(len(nums)):
            index = abs(nums[i]) - 1
            if nums[index] < 0:
                result.append(index + 1)
            else:
                nums[index] = - nums[index]
        return result
```

```java
public class Solution {
    public List<Integer> findDuplicates(int[] nums) {
        ArrayList<Integer> result = new ArrayList<Integer>();

        for(int i: nums) {
            int index = Math.abs(i) - 1;
            if(nums[index] < 0)
                result.add(index + 1);
            else
                nums[index] = -nums[index];
        }

        return result;
    }
}
```
