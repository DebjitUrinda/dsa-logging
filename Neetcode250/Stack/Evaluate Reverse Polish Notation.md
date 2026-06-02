### Problem Statement (https://neetcode.io/problems/evaluate-reverse-polish-notation/question?list=neetcode250):
You are given an array of strings tokens that represents a valid arithmetic expression in Reverse Polish Notation.

Return the integer that represents the evaluation of the expression.

The operands may be integers or the results of other operations.
The operators include '+', '-', '*', and '/'.
Assume that division between integers always truncates toward zero.

===========================================================================

### INVARIANT
**My Invariant (Sounds more like a solution)**:
Push operands to the stack, and for every operator encountered:
pop the TOS two times and push the result again

**Correct Invariant**:
After processing each token, the stack contains exactly the intermediate results
and operands needed to evaluate the remaining expression.

===========================================================================

### Solution:
    class Solution:
      def evalRPN(self, tokens: List[str]) -> int:
        stack = []

        for t in tokens:
            if t not in ["+", "-", "*", "/"]:
                stack.append(t)
            else:
                if t == "+":
                    a = int(stack.pop())
                    b = int(stack.pop())
                    stack.append(a+b)
                elif t == "-":
                    a = int(stack.pop())
                    b = int(stack.pop())
                    stack.append(b-a)
                elif t == "*":
                    a = int(stack.pop())
                    b = int(stack.pop())
                    stack.append(a*b)
                elif t == "/":
                    a = int(stack.pop())
                    b = int(stack.pop())
                    stack.append(int(b/a))

        return int(stack.pop())
