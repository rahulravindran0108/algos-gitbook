## Hackerank Fibonacci Modified

The problem statement can be found here:
https://www.hackerrank.com/challenges/fibonacci-modified

### Solution

```python
a,b,n = map(int, raw_input().strip().split(' '))
for i in xrange(3, n+1):
    c = b * b + a
    a,b = b, c
print c
```