## Contains Duplicate 3

Given an array of integers, find out whether there are two distinct indices i and j in the array such that the difference between nums[i] and nums[j] is at most t and the difference between i and j is at most k.

### Solution

```python
class Solution(object):
    def containsNearbyAlmostDuplicate(self, nums, k, t):
        """
        :type nums: List[int]
        :type k: int
        :type t: int
        :rtype: bool
        """
        bucket = {}
        for i, v in enumerate(nums):
            bucket_num, offset = (v / t, 1) if t else (v, 0)
            print bucket_num
            for idx in xrange(bucket_num - offset, bucket_num + offset + 1):
                if idx in bucket and abs(bucket[idx] - nums[i]) <= t:
                    return True

            bucket[bucket_num] = nums[i]

            if len(bucket) > k:
                del bucket[nums[i-k] / t if t else nums[i-k]]
        return False


```
