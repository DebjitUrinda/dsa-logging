### Problem Statement (https://neetcode.io/problems/validate-parentheses/question?list=neetcode250):
You are given a string s consisting of the following characters: '(', ')', '{', '}', '[' and ']'.

The input string s is valid if and only if:

Every open bracket is closed by the same type of close bracket.
Open brackets are closed in the correct order.
Every close bracket has a corresponding open bracket of the same type.
Return true if s is a valid string, and false otherwise.

===========================================================================================

### INVARIANT:
**My invariant**:
After every stack operation, it must pop only if it matches the TOS

**Correct Invariant**:
After processing the first i characters of the string,
the stack contains exactly the unmatched opening brackets.

The top of the stack is the most recent unmatched opening bracket,
which is the next bracket that must be closed for the string to remain valid.

===========================================================================================

### Solution
**My Solution**:

    class Solution:
      def isValid(self, s: str) -> bool:
        stack = []
        hashMap = {
            "(": ")",
            "{": "}",
            "[": "]"
            }

        for ch in s:
            if not stack or ch in ["(", "{", "["]:
                stack.append(ch)
            elif hashMap[stack[-1]] == ch:
                    stack.pop()
        
        return len(stack) == 0

- Works, but there are some unhandled stack invariants like no entry of closing brackets in stack.
- Basically this doesn't clearly segregate the opening and closing brackets properly.              

**Correct Solution**:

    class Solution:
      def isValid(self, s: str) -> bool:
        stack = []

        hashMap = {
            "(": ")",
            "{": "}",
            "[": "]"
        }

        for ch in s:
            if ch in hashMap:  # opening bracket
                stack.append(ch)
            else:              # closing bracket
                if not stack:
                    return False

                if hashMap[stack[-1]] == ch:
                    stack.pop()
                else:
                    return False

        return len(stack) == 0
