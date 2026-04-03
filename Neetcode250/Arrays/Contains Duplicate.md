Problem Statement (https://neetcode.io/problems/duplicate-integer/question?list=neetcode250): Given an integer array nums, return true if any value appears more than once in the array, otherwise return false.

What are we actually trying to solve?
At its core: ❓ “Is there any repetition in this data?”
This is not about arrays. This is about: 🔥 Detecting duplicates efficiently

Solution:
1.
class Solution:

    def hasDuplicate(self, nums: List[int]) -> bool:
    
        hashMap = {}

        for i in nums:
            if i in hashMap:
                return True

            hashMap[i] = 1

        return False

2. Another way is to sort the array.
