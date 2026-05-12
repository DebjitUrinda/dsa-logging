### Problem Statement (https://neetcode.io/problems/contains-duplicate-ii/question?list=neetcode250):
You are given an integer array nums and an integer k, return true if there are two distinct indices i and j in the array such that nums[i] == nums[j] and abs(i - j) <= k, otherwise return false.

================================================================================

#### INVARIANTS
**Set(Window) invariant**:
- After processing nums[i], the set contains the last k elements seen so far (or fewer if fewer than k elements have been processed).

**More precisely:**
The window contains at most k elements.
================================================================================

#### Solution
**My Solution**:
    
    class Solution:
      def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        window = {}
        idx = 0

        for i in nums:
            if i not in window:
                if len(window) < k:
                    window.append(i)
                else:
                    window.pop()
                    window.append(i)
            else:
                idx = index of window[i] - index of i in nums
                return abs(idx) <= k
        
        return False

**Correct Solution**:
    
    class Solution:
      def containsNearbyDuplicate(self, nums: List[int], k: int) -> bool:
        window = set()

        for i in range(len(nums)):
            # If current value is already in the last k elements,
            # we found a duplicate within distance <= k.
            if nums[i] in window:
                return True

            # Add current value to the window.
            window.add(nums[i])

            # Keep only the last k elements.
            if len(window) > k:
                window.remove(nums[i - k])

        return False

