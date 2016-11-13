## 4 Sum

Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.

Note: The solution set must not contain duplicate quadruplets.

For example, given array S = [1, 0, -1, 0, -2, 2], and target = 0.
```
A solution set is:
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

### Solution

```python
class Solution(object):
    def fourSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        nums.sort()
        res = []
        for i in range(len(nums) - 3):
            if nums[i] > target/4.0:
                break
            if i > 0 and nums[i] == nums[i-1]:
                continue
            target2 = target - nums[i]
            for j in range(i+1,len(nums) - 2):
                if nums[j] > target2/3.0:
                    break
                if j >i + 1 and nums[j] == nums[j-1]:
                    continue
                k, l = j+1, len(nums) -1
                target3 = target2 - nums[j]
                if nums[k] > target3/2.0:
                    continue
                if nums[l] < target3/2.0:
                    continue
                while k < l:
                    s = nums[k] + nums[l]
                    if s == target3:
                        res.append([nums[i], nums[j], nums[k], nums[l]])
                        kk = nums[k]
                        k += 1
                        while k<l and nums[k] == kk:
                            k += 1

                        ll = nums[l]
                        l -= 1
                        while k<l and nums[l] == ll:
                            l -= 1
                    elif s < target3:
                        k += 1
                    else:
                        l -= 1
        return res

```
