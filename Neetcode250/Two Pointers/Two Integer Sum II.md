### Problem Statement (https://neetcode.io/problems/two-integer-sum-ii/question?list=neetcode250):

Given an array of integers numbers that is sorted in non-decreasing order.

Return the indices (1-indexed) of two numbers, [index1, index2], 
such that they add up to a given target number target and index1 < index2. 
Note that index1 and index2 cannot be equal, therefore you may not use the same element twice.

There will always be exactly one valid solution.

Your solution must use O(1) additional space.

======================================================================

#### Why two pointer:
    
    not because index order is important OR    
    (index1 < index2 is easy to satisfy once you choose two different positions).

The real reason two pointers work is:
Sorted order gives you information about how moving a pointer changes the sum.
- If current sum is too small, move left rightward to increase the sum.
- If current sum is too large, move right leftward to decrease the sum.

Without sorting, moving pointers would be blind guessing.

#### Invairant:
My thought: 
keep changing the pointers until the sum target is met inside
That is closer to a process description, not a precise invariant.

#### Clear invariant:
At every step:
- The valid pair (guaranteed to exist) is still within the current search window [left, right].
- Any pair outside that eliminated region has been proven impossible.

======================================================================

#### Solution:
    class Solution:
      def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l, r = 0, len(numbers)-1
        
        while l<r:
            check = numbers[l] + numbers[r]
            
            if check == target:
                return [l+1, r+1]
            
            elif check < target:
                l += 1

            elif check > target:
                r -= 1

        return []
