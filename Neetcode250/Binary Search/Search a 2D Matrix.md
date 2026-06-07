### Problem Statement (https://neetcode.io/problems/search-2d-matrix/question?list=neetcode250):
You are given an m x n 2-D integer array matrix and an integer target.

Each row in matrix is sorted in non-decreasing order.
The first integer of every row is greater than the last integer of the previous row.
Return true if target exists within matrix or false otherwise.

Can you write a solution that runs in O(log(m * n)) time?

==================================================================

### INVARIANT
**My Invariant (Two Binary Search Approach)**:
Implement binary search on column 1 and then the row after finding the row in which it might exist

-------
For my approach:
After each iteration of the row search, all rows eliminated are guaranteed not to contain the target; therefore, if the target exists, it must be in one of the remaining candidate rows.
Then after selecting the row:
If the target exists in that row, it must be in the remaining column interval.

**Correct Invariant (Flattened binary search approach)**:
At the start of every iteration, if the target exists in the matrix, then its flattened index lies within the interval [l, h].
The flattened search is including the entire matrix as one range.

==================================================================

### SOLUTION
*The only difference would be the calculation of row and col using mid*

    class Solution:
      def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        rows, cols = len(matrix), len(matrix[0])
        l, h = 0, rows*cols-1

        while l<=h:
            mid = (l+h)//2

            row = mid//cols
            col = mid%cols

            val = matrix[row][col]

            if val < target:
                l = mid + 1
            elif val > target:
                h = mid - 1

            elif val == target:
                return True
            # else:
            #     return True

        return False
