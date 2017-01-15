## Combinations

Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

For example,
```
If n = 4 and k = 2, a solution is:

[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```

### Solution

```python

class Solution(object):
    def combine(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: List[List[int]]
        """
        result = []
        self.combine_recurse(range(1, n+1), k, [], result)
        return result

    def combine_recurse(self, nums, k, intermediate, result):
        if k == 0:
            result.append(list(intermediate))
            return
        if len(nums) >= k:
            for i in xrange(len(nums)):
                self.combine_recurse(nums[i+1:], k - 1, intermediate + [nums[i]], result)
        return

```

```java
public class Solution {
    public List<List<Integer>> combine(int n, int k) {
        List<List<Integer>> result = new ArrayList<>();

        dfs(result, new ArrayList<>(), 1, n, k);
        return result;
    }

    public void dfs(List<List<Integer>> result, List<Integer> path, int start, int n, int k) {
        if(k == 0) {
            result.add(new ArrayList<>(path));
            return;
        } else {
            for(int i = start;i<=n;i++) {
                path.add(i);
                dfs(result, path, i  + 1, n, k - 1);
                path.remove(path.size() - 1);
            }
        }
    }
}
```
