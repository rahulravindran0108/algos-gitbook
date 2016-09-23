## Find Minimum in Rotated Sorted Array

Suppose a sorted array is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

You may assume no duplicate exists in the array.

### Solution

```python
class Solution(object):
    def findMin(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        return self.binary_search(nums, 0 , len(nums) - 1)

    def binary_search(self, nums, l, r):
        if l == r:
            return nums[l]
        if r - l == 1:
            return min(nums[l], nums[r])

        mid = l + (r - l) / 2

        if nums[l] < nums[r]:
            return nums[l]
        elif nums[mid] > nums[l]:
            return self.binary_search(nums, mid, r)
        else:
            return self.binary_search(nums, l, mid)
```
