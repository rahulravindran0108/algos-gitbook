## Min Stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.
```
push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
getMin() -- Retrieve the minimum element in the stack.
Example:
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

### Solution

```python
class MinStack:

    def __init__(self):
        self.q = []

    # @param x, an integer
    # @return an integer
    def push(self, x):
        curMin = self.getMin()
        if curMin == None or x < curMin:
            curMin = x
        self.q.append((x, curMin));

    # @return nothing
    def pop(self):
        self.q.pop()


    # @return an integer
    def top(self):
        if len(self.q) == 0:
            return None
        else:
            return self.q[len(self.q) - 1][0]


    # @return an integer
    def getMin(self):
        if len(self.q) == 0:
            return None
        else:
            return self.q[len(self.q) - 1][1]
```

```java
public class MinStack {

    private long min;
    Stack<Long> stack;

    /** initialize your data structure here. */
    public MinStack() {
        stack = new Stack<>();
    }

    public void push(int x) {
        if(stack.isEmpty()) {
            stack.push(0L);
            min = x;
        } else {
            stack.push(x - min);
            if(x < min) min = x;
        }
    }

    public void pop() {
        if(stack.isEmpty()) return;
        long pop = stack.pop();
        if(pop < 0)
            min = min - pop;

    }

    public int top() {
        long top = stack.peek();
        if (top>0){
            return (int)(top+min);
        }else{
           return (int)(min);
        }
    }

    public int getMin() {
        return (int) min;
    }
}

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(x);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
 ```
