## Maximum Subarray

Given an array A={a1,a2,a3,...an} of n elements, find the maximum possible sum of a

- Contiguous subarray
- Non-contiguous (not necessarily contiguous) subarray.

Empty subarrays/subsequences should not be considered.

### Solution

```python
# Enter your code here. Read input from STDIN. Print output to STDOUT

def max_subarray(n):
    if not n:
        print 0, 0
    else:
        nc, c, c_sum = -1000000, -1000000, -1000000
        for i in range(len(n)):
            nc = max(n[i], nc + n[i], nc)
            c_sum = max(n[i], c_sum + n[i])
            c = max(c, c_sum)
        print c, nc

t = int(raw_input())
for i in range(t):
    _ = raw_input()
    n = map(int, raw_input().strip().split(' '))
    max_subarray(n)

```
