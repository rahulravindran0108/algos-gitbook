## Search For A Range

Given a sorted array of integers, find the starting and ending position of a given target value.

Your algorithm's runtime complexity must be in the order of O(log n).

If the target is not found in the array, return [-1, -1].

For example,
```
Given [5, 7, 7, 8, 8, 10] and target value 8,
return [3, 4].
```

### Solution

```java
public class Solution {
    public int[] searchRange(int[] nums, int target) {
        int l = 0, r = nums.length - 1;
        int [] res = {-1, -1};

        while(nums[l] < nums[r]) {
            int mid = l + (r - l) / 2;
            if(nums[mid] > target)
                r = mid - 1;
            else if(nums[mid] < target)
                l = mid + 1;
            else {
                if(nums[l] == nums[mid])
                    r --;
                else
                    l ++;
            }
        }

        if(nums[l] == nums[r] && nums[l] == target) {
            res[0] = l;
            res[1] = r;
        }

        return res;
    }
}
```
