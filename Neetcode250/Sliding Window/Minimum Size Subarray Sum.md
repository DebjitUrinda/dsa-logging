### Problem Statement (https://neetcode.io/problems/minimum-size-subarray-sum/question?list=neetcode250):
You are given an array of positive integers nums and a positive integer target, return the minimal length of a subarray whose sum is greater than or equal to target. If there is no such subarray, return 0 instead.

A subarray is a contiguous non-empty sequence of elements within an array.

========================================================================================

**INVARIANT**
#### My Invariant:
After each iteration, evaluate for the valid window, start by increasing the size of the window towards right and when it becomes valid, try to make it invalid by shrinking till invalid, keep the latest window size until last valid. Increase the right pointer to increase the size of the array again, and repeat the process.

#### Crisp Invariant:
After each iteration, the current window contains the current subarray sum, and whenever the window becomes valid (window_sum >= target), we shrink it from the left as much as possible while preserving validity.

========================================================================================

### Solution:
**My incorrect version**:

    class Solution:
      def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        left = 0
        minWindow, runSum = float('inf'), 0

        # while left <= right:
        #     runSum = 0
        for right in range(len(nums)):
            runSum += nums[right]
            if runSum >= target:
                window = right - left + 1
                while left < right and runSum >= target:
                    window = right - left + 1
                    runSum -= nums[left]
                    left += 1
                    # window = right - left + 1
                    
                minWindow = min(window, minWindow)

        return 0 if minWindow == float('inf') else minWindow

**Correct solution**:

    class Solution:
      def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        left = 0
        minWindow = float('inf')
        runSum = 0

        for right in range(len(nums)):
            runSum += nums[right]

            while runSum >= target:
                minWindow = min(minWindow, right - left + 1)

                runSum -= nums[left]
                left += 1

        return 0 if minWindow == float('inf') else minWindow
