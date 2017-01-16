## Course Schedule

There are a total of n courses you have to take, labeled from 0 to n - 1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

For example:

`2, [[1,0]]`

There are a total of 2 courses to take. To take course 1 you should have finished course 0. So it is possible.

`2, [[1,0],[0,1]]`

There are a total of 2 courses to take. To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.
### Solution

```python
class Solution(object):
    def canFinish(self, numCourses, prerequisites):
        """
        :type numCourses: int
        :type prerequisites: List[List[int]]
        :rtype: bool
        """
        graph = [[] for _ in xrange(numCourses)]
        visit = [0 for _ in xrange(numCourses)]
        for x,y in prerequisites:
            graph[x].append(y)
        def dfs(i):
            if visit[i] == -1:
                return False
            if visit[i] == 1:
                return True
            visit[i] = -1
            for j in graph[i]:
                if not dfs(j):
                    return False
            visit[i] = 1
            return True
        for i in xrange(numCourses):
            if not dfs(i):
                return False
        return True
```

```java
public class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        int [][] matrix = new int[numCourses][numCourses];
        int [] inDegree = new int[numCourses];

        for(int [] p : prerequisites) {
            int course = p[0], pre = p[1];

            if(matrix[pre][course] == 0)
                inDegree[course] ++;
            matrix[pre][course] = 1;
        }

        int count = 0;
        Queue<Integer> q = new LinkedList();

        for(int i = 0;i< inDegree.length;i++)
            if(inDegree[i] == 0) q.offer(i);

        while(!q.isEmpty()) {
            int cur = q.poll();
            count += 1;

            for(int i = 0;i<numCourses;i++) {
                if(matrix[cur][i] != 0) {
                    if(--inDegree[i] == 0)
                        q.offer(i);
                }
            }
        }

        return count == numCourses;
    }
}
```
