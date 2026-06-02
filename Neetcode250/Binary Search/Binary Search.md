### Problem Statement (https://neetcode.io/problems/binary-search/question?list=neetcode250):
You are given an array of distinct integers nums, sorted in ascending order, and an integer target.

Implement a function to search for target within nums. If it exists, then return its index, otherwise, return -1.

Your solution must run in O(logn) time.

================================================================================

### INVARIANT:
**My Invariant**:
After each iteration, the array for consideration must be the region that satisfies the condition where the target must lie

================================================================================

### Solution
    class Solution:
      def search(self, nums: List[int], target: int) -> int:
        l, h = 0, len(nums)-1

        while l <= h:
            mid = (l+h)//2
            if nums[mid]<target:
                l = mid+1
            elif nums[mid]>target:
                h = mid-1
            else:
                return mid

        return -1
