### Problem Statement (https://neetcode.io/problems/reverse-string/question?list=neetcode250):
You are given an array of characters which represents a string s. 
Write a function which reverses a string.

You must do this by modifying the input array in-place with O(1) extra memory.

==============================================================================

“The string should be reversed in-place” is the goal / constraint, not the loop invariant.

Difference
- Goal: What must be true when the algorithm finishes.
- Constraint: Extra rules (here: O(1) memory, modify input directly).
- Invariant: Something that remains true during every iteration of the loop.

For Reverse String (two pointers), a proper invariant is:
- If left starts at the beginning and right at the end, then after each swap:
- All characters before left are already in their final reversed positions.
- All characters after right are already in their final reversed positions.

Only the section between left and right still needs processing.

++ In one line
Invariant: The outside portion is already correctly reversed; only the inside portion remains.

==============================================================================

My Solution:

    class Solution:
      def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        l, r = 0, len(s)-1

        while l<r:
            s[l], s[r] = s[r], s[l]
            l += 1
            r -= 1
            
