## Increasing Subsequence

Given an integer array, your task is to find all the different possible increasing subsequences of the given array, and the length of an increasing subsequence should be at least 2 .

```
Example:

Input: [4, 6, 7, 7]
Output: [[4, 6], [4, 7], [4, 6, 7], [4, 6, 7, 7], [6, 7], [6, 7, 7], [7,7], [4,7,7]]
Note:
The length of the given array will not exceed 15.
The range of integer in the given array is [-100,100].
The given array may contain duplicates, and two equal integers should also be considered as a special case of increasing sequence.
```

### Solution

```java
public class Solution {
    public List<List<Integer>> findSubsequences(int[] nums) {
    	List<List<Integer>> res = new ArrayList<>();
    	helper(res, new ArrayList<Integer>(), nums, 0);
    	return res;
    }

    private void helper(List<List<Integer>> res, List<Integer> list, int[] nums, int id) {
    	if (list.size() > 1) res.add(new ArrayList<Integer>(list));
    	List<Integer> unique = new ArrayList<Integer>();
    	for (int i = id; i < nums.length; i++) {
    		if (id > 0 && nums[i] < nums[id-1]) continue; // skip non-increase
    		if (unique.contains(nums[i])) continue; // skip duplicate
    		unique.add(nums[i]);
    		list.add(nums[i]);
    		helper(res, list, nums, i+1);
    		list.remove(list.size()-1);
    	}
    }
}
```
