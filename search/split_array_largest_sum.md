## Split Array Largest Sum

Given an array which consists of non-negative integers and an integer m, you can split the array into m non-empty continuous subarrays. Write an algorithm to minimize the largest sum among these m subarrays.

Note:
If n is the length of array, assume the following constraints are satisfied:

1 ≤ n ≤ 1000
1 ≤ m ≤ min(50, n)

```
Examples:

Input:
nums = [7,2,5,10,8]
m = 2

Output:
18


Explanation:
There are four ways to split nums into two subarrays.
The best way is to split it into [7,2,5] and [10,8],
where the largest sum among the two subarrays is only 18.
```

### Solution

```java
public class Solution {
    public int splitArray(int[] nums, int m) {
        long sum = 0;
        int max = 0;
        for(int num: nums){
            max = Math.max(max, num);
            sum += num;
        }
        return (int)binarySearch(nums, max, sum, m);
    }

    public long binarySearch(int [] nums, long low, long high, int m) {
        long mid = 0;
        while(low < high) {
            mid = (low + high) / 2;
            if(valid(nums, mid, m))
                high = mid;
            else
                low = mid + 1;
        }
        return high;
    }

    public boolean valid(int [] nums, long max, int m) {
        int cur = 0, count = 1;
        for(int num: nums) {
            cur += num;

            if(cur > max) {
                count ++;
                cur = num;
                if(count > m)
                    return false;
            }
        }

        return true;
    }
}
```
