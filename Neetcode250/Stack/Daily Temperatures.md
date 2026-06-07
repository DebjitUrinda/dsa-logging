### Problem Statement (https://neetcode.io/problems/daily-temperatures/question?list=neetcode250):
You are given an array of integers temperatures where temperatures[i] represents the daily temperatures on the ith day.

Return an array result where result[i] is the number of days after the ith day before a warmer temperature appears on a future day. If there is no day in the future where a warmer temperature will appear for the ith day, set result[i] to 0 instead.

====================================================================================

### INVARIANT

After processing day i:

1. The stack contains exactly the indices whose next warmer day
   has not yet been found.

2. Temperatures at those indices are in decreasing order.

3. For every index not in the stack, the answer has already been computed.

====================================================================================

### SOLUTION

    class Solution:
      def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        result = [0] * len(temperatures)
        stack = []  # stores indices

        for i, temp in enumerate(temperatures):

            while stack and temp > temperatures[stack[-1]]:
                prev_day = stack.pop()
                result[prev_day] = i - prev_day

            stack.append(i)

        return result
