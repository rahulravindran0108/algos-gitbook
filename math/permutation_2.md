## Permutations 2

Given a collection of numbers that might contain duplicates, return all possible unique permutations.

```
For example,
[1,1,2] have the following unique permutations:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```

### Solution

```java
public class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> res = new ArrayList<>();
        if(nums == null || nums.length == 0) return res;
        boolean [] used = new boolean[nums.length];
        List<Integer> list = new ArrayList<>();

        Arrays.sort(nums);
        dfs(nums, used, list, res);

        return res;
    }

    public void dfs(int [] nums, boolean [] used, List<Integer> list, List<List<Integer>> res) {
        if(list.size() == nums.length) {
            res.add(new ArrayList<>(list));
            return;
        }

        for(int i = 0; i< nums.length;i++) {
            if(used[i]) continue;
            if(i > 0 && nums[i] == nums[i-1] && !used[i - 1]) continue;
            list.add(nums[i]);
            used[i] = true;
            dfs(nums, used, list, res);
            used[i] = false;
            list.remove(list.size() -1);
        }
    }
}
```

```java
public class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        Arrays.sort(nums);
        dfs(result,new ArrayList<>(), nums, new boolean[nums.length]);
        return result;
    }

    public void dfs(List<List<Integer>> result, List<Integer> path, int [] nums, boolean [] visited) {
        if(path.size() == nums.length) {
            result.add(new ArrayList<>(path));
            return;
        } else {
            for(int i = 0;i<nums.length;i++) {
                if(visited[i]) continue;
                if(i>0 &&nums[i-1]==nums[i] && !visited[i-1]) continue;
                path.add(nums[i]);
                visited[i] = true;
                dfs(result, path, nums, visited);
                path.remove(path.size() - 1);
                visited[i] = false;
            }
        }
    }
}
```
