### Problem Statement (https://neetcode.io/problems/valid-sudoku/question?list=neetcode250):
You are given a 9 x 9 Sudoku board board. A Sudoku board is valid if the following rules are followed:

Each row must contain the digits 1-9 without duplicates.
Each column must contain the digits 1-9 without duplicates.
Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without duplicates.
Return true if the Sudoku board is valid, otherwise return false

Note: A board does not need to be full or be solvable to be valid.

==============================================================================

What is this problem really testing?
- This is not about Sudoku.
- It’s testing:
  1. Can you track constraints across dimensions?
      You need to monitor:
      - row-wise
      - column-wise
      - subgrid-wise
    👉 simultaneously
2. Can you map positions → groups?
    This is the key insight:
    For a cell (r, c):
      box_id = (r // 3, c // 3)

Edge cases:
1. Empty board -> valid
2. Duplicate in a row -> invalid
3. Duplicate in a column -> invalid
4. Duplicate in a sub-grid -> invalid
5. Partially full, but still valid

Verbal explanation:


==============================================================================

My approach:
