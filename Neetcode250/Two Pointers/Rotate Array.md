### Problem Statement (https://neetcode.io/problems/rotate-array/question?list=neetcode250):
You are given an integer array nums, rotate the array to the right by k steps, where k is non-negative.

=====================================================================================

#### INVARIANTS
**My Invariant (Wrong)**:
- You need to have two pointer, one pointing at the element towards the end of the array that needs to be swapped and another pointer to the left that will be marker of the swap position.
Now, after each iteration the elements before the left pointer are already having rotated elements.

Correct Thinking:
- If an element is currently at index i, where should it go after rotating right by k?

**Correct Invariant**:
After processing the first i indices, every processed element nums[p] has been placed into rotated[(p + k) % n], and those positions contain their final values.

**Mental Shortcut**:
“Each element knows exactly where it belongs: (i + k) % n.”

=====================================================================================

#### Solution:
    class Solution:
      def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        size = len(nums)
        rotated = [0]*size

        for i in range(size):
            rotated[(i+k)%size] = nums[i]

        nums[:] = rotated[:]
        
