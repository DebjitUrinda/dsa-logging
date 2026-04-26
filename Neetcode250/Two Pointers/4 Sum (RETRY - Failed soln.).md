### Problem Statement (https://neetcode.io/problems/4sum/question?list=neetcode250):
You are given an integer array nums of size n, 
return an array of all the unique quadruplets [nums[a], nums[b], nums[c], nums[d]] such that:

0 <= a, b, c, d < n
a, b, c, and d are distinct.
nums[a] + nums[b] + nums[c] + nums[d] == target
You may return the answer in any order.

**Note**: [1,0,3,2] and [3,0,1,2] are considered as same quadruplets.

=================================================================================

*I did not understand the invariant properly*
For 4Sum, think of it as the natural extension of 3Sum.
- 2Sum → fix 0 numbers, solve 2 with pointers
- 3Sum → fix 1 number, solve remaining 2 with pointers
- 4Sum → fix 2 numbers, solve remaining 2 with pointers

**Correct Invariant**
Outer loops (i, j)
After each iteration:
- All unique quadruplets whose first two indices come before the current (i, j) have already been processed.

=================================================================================

#### My first failed solution:
    class Solution:
      def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        nums.sort()
        res = []

        l, r = 0, len(nums)-1

        while l < r and l < r-3:
            leftPair = nums[l] + nums[l+1]
            rightPair = nums[r] + nums[r-1]
            total = leftPair + rightPair

            if total == target:
                res.append([nums[l], nums[l+1], nums[r-1], nums[r]])

            elif total > target:
                r -= 1
            
            elif total < target:
                l += 1

        return res

#### My second failed solution:
    class Solution:
      def fourSum(self, nums: List[int], target: int) -> List[List[int]]:
        nums.sort()
        res = []

        l, r = 0, len(nums)-1

        while l < r:
            while nums[l+1] == nums[l] and l<r:
                l += 1
            while nums[r-1] == nums[r] and l<r:
                r -= 1
                
            newT = target - nums[l] - nums[r]

            i = l+1
            j = r-1

            while i<j:
                total = newT - nums[i] - nums[j]
                if total == 0:
                    res.append([nums[l], nums[i], nums[j], nums[r]])
                elif total > 0:
                    j -= 1
                elif total < 0:
                    i += 1

            l += 1
            r -= 1

        return res

=================================================================================

#### Correct solution:
