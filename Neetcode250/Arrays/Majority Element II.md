### Problem Statement (https://neetcode.io/problems/majority-element-ii/question?list=neetcode250):
You are given an integer array nums of size n, find all elements that appear more than ⌊ n/3 ⌋ times. 
You can return the result in any order.

===========================================================================

What I was trying:
Form fixed subgroups/triplets of size 3 and use local counts to eliminate noise.
Example:
[1,1,2,3,1,2,1] → fixed groups:
[1,1,2]
[3,1,2]
[1]
This can hide the global winner because grouping depends on positions.
Why that idea matters:
A true element occurring > n/3 times cannot be fully removed by repeatedly cancelling groups of 3 distinct elements.
What should actually be done:
Use dynamic triplet cancellation (Extended Boyer-Moore Voting).
Instead of fixed groups, whenever three different values compete, cancel one of each.
Example:
[1,2,3,1,2,1,1]
Cancel (1,2,3) → remaining influence: [1,2,1,1]
Then 1 survives as dominant.
Rules:
At most 2 elements can appear more than n/3
Keep 2 candidates + 2 counts
Match candidate → increment
Empty slot → assign candidate
Third different value while both active → decrement both counts
Final Step:
Run a second pass to verify real counts.
Core Insight:
My idea = explicit fixed triplets by index.
Correct idea = implicit dynamic cancellations across the whole array so heavy hitters survive.

===========================================================================

Solution:

    class Solution:
      def majorityElement(self, nums: List[int]) -> List[int]:
        cand1 = cand2 = None
        count1 = count2 = 0

        for num in nums:
            if num == cand1:
                count1 += 1
            elif num == cand2:
                count2 += 1
            elif count1 == 0:
                cand1 = num
                count1 += 1
            elif count2 == 0:
                cand2 = num
                count2 += 1
            else:
                count1 -= 1
                count2 -= 1

        # verify
        res = []
        for c in [cand1, cand2]:
            if c is not None and nums.count(c) > len(nums)//3:
                if c not in res:
                    res.append(c)

        return res

Manual verification is not working correctly:

        res = []
        if count1 > n // 3:
            res.append(cand1)

        if cand2 != cand1 and count2 > n // 3:
            res.append(cand2)
