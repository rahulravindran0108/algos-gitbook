## Permutation

Given a collection of distinct numbers, return all possible permutations.

For example,
```
[1,2,3] have the following permutations:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

### Solution

```python
class Solution(object):
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        result = []
        used = [False] * len(nums)
        self.recurse(used, result, [],  nums)
        return result

    def recurse(self, used, result, cur, nums):
        if len(cur) == len(nums):
            result.append(cur + [])
            return
        for i in xrange(len(nums)):
            if not used[i]:
                cur.append(nums[i])
                used[i] = True
                self.recurse(used, result, cur, nums)
                cur.pop()
                used[i] = False

```

```java
public class Solution {
    public List<List<Integer>> permute(int[] nums) {

        List<List<Integer>> result = new ArrayList<>();
        dfs(result,new ArrayList<>(), nums);
        return result;
    }

    public void dfs(List<List<Integer>> result, List<Integer> path, int [] nums) {
        if(path.size() == nums.length) {
            result.add(new ArrayList<>(path));
            return;
        } else {
            for(int x : nums) {
                if(!path.contains(x)) {
                    path.add(x);
                    dfs(result, path, nums);
                    path.remove(path.size() - 1);
                }
            }
        }
    }
}
```
