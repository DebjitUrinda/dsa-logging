### Problem Statement (https://neetcode.io/problems/minimum-stack/question?list=neetcode250):
Design a stack class that supports the push, pop, top, and getMin operations.

MinStack() initializes the stack object.
void push(int val) pushes the element val onto the stack.
void pop() removes the element on the top of the stack.
int top() gets the top element of the stack.
int getMin() retrieves the minimum element in the stack.
Each function should run in O(1) time.

====================================================================================

**INVARIANTS**
#### My invariant
After each iteration, the stack should represent all the elements according to the stack operations, also we must decide the minimum element after each push to keep a track of the minimum element.

#### Correct invariant
we need to keep a min_stack instead of one min element because the min_stack keeps track of the minimum element at each stack depth. So the Invariant becomes:
- After each iteration, the stack should represent all the elements according to the stack operations, also we must decide the minimum element after each push to keep a track of the minimum element.

====================================================================================

**Solution**

    class MinStack:

      def __init__(self):
        # Main stack stores all values.
        self.stack = []

        # min_stack[i] stores the minimum value among self.stack[0:i+1].
        self.min_stack = []

      def push(self, val: int) -> None:
        # Push the value onto the main stack.
        self.stack.append(val)

        # Push the minimum so far onto min_stack.
        if not self.min_stack:
            self.min_stack.append(val)
        else:
            self.min_stack.append(min(val, self.min_stack[-1]))

      def pop(self) -> None:
        # Pop from both stacks to keep them aligned.
        self.stack.pop()
        self.min_stack.pop()

      def top(self) -> int:
        # Return the top element.
        return self.stack[-1]

      def getMin(self) -> int:
        # The current minimum is always on top of min_stack.
        return self.min_stack[-1]
