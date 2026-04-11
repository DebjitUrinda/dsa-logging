### Problem Statement (https://neetcode.io/problems/range-sum-query-2d-immutable/question?list=neetcode250):

You are given a 2D matrix matrix, handle multiple queries of the following type:
- Calculate the sum of the elements of matrix inside the rectangle defined by
  its upper left corner (row1, col1) and lower right corner (row2, col2).

Implement the NumMatrix class:
- NumMatrix(int[][] matrix) Initializes the object with the integer matrix matrix.
- int sumRegion(int row1, int col1, int row2, int col2)
  Returns the sum of the elements of matrix inside the rectangle defined by its upper left corner (row1, col1) and lower right corner (row2, col2).

*You must design an algorithm where sumRegion works on O(1) time complexity.*

================================================================================================

My Approach:

    class NumMatrix:
      def __init__(self, matrix: List[List[int]]):
        self.prefix_matrix = matrix
        rows = len(matrix)
        cols = len(matrix[0])

        for i in range(rows):
            prefixSum = 0
            for j in range(cols):
                prefixSum += self.prefix_matrix[i][j]
                self.prefix_matrix[i][j] = prefixSum

      def sumRegion(self, row1: int, col1: int, row2: int, col2: int) -> int:
        result = 0
        print(self.prefix_matrix)
        
        for i in range(row1, row2+1):
                if col1!=0:
                    result += self.prefix_matrix[i][col2] - self.prefix_matrix[i][col1-1]
                
                else:
                    result += self.matrix[i][col2]


The code had an issue that prevented it from working correctly:
- Time Complexity: While the logic now correctly calculates the sum using row-level prefix sums, it currently runs in O(R) time (where R is the number of rows).
- However, the problem requirement asks for O(1) time complexity for sumRegion. To achieve true O(1), a 2D Prefix Sum (Inclusion-Exclusion Principle) is typically required.


Correct Approach is to use inclusion-exclusion principle for 2D Prefix Sum instead of 1D
