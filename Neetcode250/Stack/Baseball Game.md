### Problem Statement (https://neetcode.io/problems/baseball-game/question?list=neetcode250):
You are keeping the scores for a baseball game with strange rules. At the beginning of the game, you start with an empty record.

Given a list of strings operations, where operations[i] is the ith operation you must apply to the record and is one of the following:

An integer x: Record a new score of x.
'+': Record a new score that is the sum of the previous two scores.
'D': Record a new score that is the double of the previous score.
'C': Invalidate the previous score, removing it from the record.
Return the sum of all the scores on the record after applying all the operations.

Note: The test cases are generated such that the answer and all intermediate calculations fit in a 32-bit integer and that all operations are valid.

====================================================================================

**INVARIANTS**

#### My Invariants:
* After processing each operation, `record` contains exactly the valid scores so far,
in chronological order, and `record[-1]` is the most recent valid score.

====================================================================================

### Solution
**Python Truthiness issue**: For input ["0", "D", "+", "C"], the condition `if record[-1]` evaluated to
False when `record[-1] == 0`, so the doubled score was not appended.

    class Solution:
      def calPoints(self, operations: List[str]) -> int:
        import re
        record = []

        for op in operations:
            if re.fullmatch(r"-?\d+", op):
                record.append(int(op))
            elif re.fullmatch(r"\+", op):
                record.append(record[-1] + record[-2])
            elif op == "C":
                record.pop()
            elif op == "D":
                if record[-1]:
                    push = 2 * record[-1]
                    record.append(push)

        return sum(record)

**Correct Solution (with regex):**

    class Solution:
      def calPoints(self, operations: List[str]) -> int:
        import re
        record = []

        for op in operations:
            if re.fullmatch(r"-?\d+", op):
                record.append(int(op))
            elif re.fullmatch(r"\+", op):
                record.append(int(record[-1]) + int(record[-2]))
            elif op == "C":
                record.pop()
            elif op == "D":
                push = 2*int(record[-1])
                record.append(push)

        return sum(record)

**Without regex**:
    
    class Solution:
      def calPoints(self, operations: List[str]) -> int:
        record = []

        for op in operations:
            if op == "+":
                record.append(record[-1] + record[-2])
            elif op == "D":
                record.append(2 * record[-1])
            elif op == "C":
                record.pop()
            else:
                record.append(int(op))

        return sum(record)
