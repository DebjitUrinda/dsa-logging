Problem Statement: (https://neetcode.io/problems/concatenation-of-array/question?list=neetcode250)
You are given an integer array nums of length n. Create an array ans of length 2n where ans[i] == nums[i] and ans[i + n] == nums[i] for 0 <= i < n (0-indexed).

Specifically, ans is the concatenation of two nums arrays.

Return the array ans.

Understanding:
This problem is to understand the concept of how indexing works. This problem is to test Index-mapping and Array construction.

Later you’ll see this in harder problems like:
circular arrays
next greater element (circular)
rotation problems

Initial solution: The error will be 'list-index out of range'
class Solution:
    def getConcatenation(self, nums: List[int]) -> List[int]:
        size = len(nums)
        # from array import array
        ans = [0]*size
        for i in range(size):
            ans[i], ans[i+size] = nums[i], nums[i]
        return ans

Final corrected solution:
class Solution:
    def getConcatenation(self, nums: List[int]) -> List[int]:
        size = len(nums)
        # from array import array
        ans = [0]*2*size
        for i in range(size):
            ans[i], ans[i+size] = nums[i], nums[i]
        return ans
