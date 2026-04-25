### Problem Statement (https://neetcode.io/problems/three-integer-sum/question?list=neetcode250):
Given an integer array nums, 
return all the triplets [nums[i], nums[j], nums[k]] where nums[i] + nums[j] + nums[k] == 0, 
and the indices i, j and k are all distinct.

The output should not contain any duplicate triplets. 
You may return the output and the triplets in any order.

================================================================================

#### Invariant:

**One-line Invariant:**
For each fixed first element, the remaining valid pair—if unseen—still lies within `[l, r]`; 
shrink the window without discarding solutions or repeating triplets.

================================================================================

#### My first solution:
    class Solution:
      def threeSum(self, nums: List[int]) -> List[List[int]]:
        res = []
        for i in range(len(nums)):
            l, r = i+1, len(nums)-1
            target = (-1)*nums[i]
            while l<r:
                if nums[l]+nums[r] == target:
                    res.append([nums[i], nums[l], nums[r]])
                    break
                l += 1
                r -= 1

        return res

#### Problems with my solution:
**Core Idea:**
Transform `a + b + c = 0` into: fix one element `a = nums[i]`, 
then solve `b + c = -a` using two pointers on a sorted array.

**Why Sorting Matters:**
Sorting enables pointer decisions:

* Sum too small → move `l` right
* Sum too large → move `r` left

**What Was Wrong Initially:**

* No sorting
* `l` started at `i` instead of `i + 1`
* Both pointers moved blindly every step
* `break` after first match (misses other valid triplets)
* No duplicate handling

**Correct Duplicate Handling:**
Need to skip duplicates at three levels:

1. `i` → avoid repeating same first element
2. `l` → avoid repeating same second element
3. `r` → avoid repeating same third element

Skipping only `i` is not enough, because duplicates can happen within the same fixed `i`.

**Why Not `break`:**
One fixed first element can have multiple valid pairs.
`break` stops early and misses answers.


#### Correct Solution:
    class Solution:
      def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()
        res = []

        for i in range(len(nums)):
            # to avoid duplicate starting element
            if i>0 and nums[i] == nums[i-1]:
                continue

            l, r = i+1, len(nums)-1
            target = (-1)*nums[i]

            while l<r:
                total = nums[l]+nums[r]
                if total == target:
                    res.append([nums[i], nums[l], nums[r]])
                    l += 1
                    r -= 1

                    # to avoid duplicate second and third elements for the same start element
                    # DO NOT USE break, it skips the other possible triplets for the same start element
                    while l<len(nums) and nums[l]==nums[l-1]:
                        l += 1
                    while r>0 and nums[r]==nums[r+1]:
                        r -= 1
                    
                elif total > target:
                    r -= 1

                elif total < target:
                    l += 1

        return res
