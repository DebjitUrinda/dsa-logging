### Problem Statement (https://neetcode.io/problems/remove-element/question?list=neetcode250):
You are given an integer array nums and an integer val. 
Your task is to remove all occurrences of val from nums in-place.
After removing all occurrences of val, 
return the number of remaining elements, say k, such that the first k elements of nums do not contain val.

Note:
The order of the elements which are not equal to val does not matter.
It is not necessary to consider elements beyond the first k positions of the array.
To be accepted, the first k elements of nums must contain only elements not equal to val.
Return k as the final result.

==========================================================

🧠 What are we actually trying to solve?
We are trying to:
Filter out a value from an array in-place and report how many valid elements remain.

Real-world analogy
Imagine:
You have a list of employees
You want to remove all interns (val)
You don’t create a new list
You just move full-time employees to the front

Edge cases:


My approach:

    class Solution:
      def removeElement(self, nums: List[int], val: int) -> int:
        ptr = 0
        for i in range(len(nums)):
            if nums[i] == val:
                ptr = i
                break

        for j in range(ptr+1, len(nums)):
            if nums[j] != val:
                nums[j], nums[ptr] = nums[ptr], nums[j]
                for l in range(ptr+1, j):
                    if nums[l] == val:
                        ptr = l

        return len(nums[:ptr])


What is wrong here?
  - 1. ❗ You don’t have a stable invariant
          A good algorithm always maintains something like:
          “Everything before index X is already correct”
          In your code:
          ptr moves unpredictably
          After swap, you search again for next val
          👉 So at any point, you don’t clearly know which part is clean
  - 2. ❗ You re-scan the array (O(n²) behavior)
            for l in range(ptr+1, j):
              if nums[l] == val:
                ptr = l
            This inner loop:
            Runs repeatedly
            Makes your solution inefficient
          👉 You’re losing the biggest advantage of this problem: linear pass
  - 3. ❗ You are over-managing state
          You’re trying to track:
            first occurrence
            next occurrence
            swapping positions
          👉 Too many moving parts = bugs + complexity

Correct Solution:
1. Swapping:

       class Solution:
        def removeElement(self, nums: List[int], val: int) -> int:
          i = 0
          n = len(nums)

          while i < n:
            if nums[i] == val:
                nums[i] = nums[n - 1]  # swap with last
                n -= 1                # shrink array
            else:
                i += 1

          return n

2. Without Swapping:

       class Solution:
        def removeElement(self, nums: List[int], val: int) -> int:
          k = 0  # position to place next valid element

          for i in range(len(nums)):
            if nums[i] != val:
                nums[k] = nums[i]
                k += 1

          return k

   Example:
   nums = [3,2,2,3], val = 3
   
   | i | nums[i] | action    | nums      | k |
   | - | ------- | --------- | --------- | - |
   | 0 | 3       | skip      | [3,2,2,3] | 0 |
   | 1 | 2       | nums[0]=2 | [2,2,2,3] | 1 |
   | 2 | 2       | nums[1]=2 | [2,2,2,3] | 2 |
   | 3 | 3       | skip      | [2,2,2,3] | 2 |

   Return 2
