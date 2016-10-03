## Gas Station

There are N gas stations along a circular route, where the amount of gas at station i is gas[i].

You have a car with an unlimited gas tank and it costs cost[i] of gas to travel from station i to its next station (i+1). You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once, otherwise return -1.

### Solution

```python
class Solution(object):
    def canCompleteCircuit(self, gas, cost):
        """
        :type gas: List[int]
        :type cost: List[int]
        :rtype: int
        """
        min_val = min_idx = val = 0
        for i in range(len(gas)):
            val += gas[i] - cost[i]
            if val < min_val:
                min_idx = i + 1
                min_val = val
        if val < 0:
            return -1
        return min_idx
```
