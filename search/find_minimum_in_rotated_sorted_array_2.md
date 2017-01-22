## Find Minimum in Rotated Sorted Array 2

Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., 0 1 2 4 5 6 7 might become 4 5 6 7 0 1 2).

Find the minimum element.

The array may contain duplicates.

### Solution

```java
public class Solution {
    public int findMin(int[] nums) {
        int l = 0, r = nums.length - 1;

        while(l < r) {
            int mid = (l + r) / 2;

            if(nums[mid] < nums[r])
                r = mid;
            else if(nums[mid] > nums[r])
                l = mid + 1;
            else
                r --;
        }

        return nums[l];
    }
}
```
