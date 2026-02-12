## What is a Prefix Sum?
* Take an array: nums = [2, 4, 1, 3]
* Prefix sum just means: At every position, store the total from the start up to that position. That’s it.
* So prefix array becomes: prefix = [2, 6, 7, 10]
* Why do we make this? -> Because now we can get any subarray sum instantly. Instead of adding again and again.
* Example
Find sum of elements from index 1 to 3.
Original array:
[2, 4, 1, 3]
That means:
4 + 1 + 3 = 8
Now look at prefix:
[2, 6, 7, 10]


#### Range Sum Query – Immutable (https://leetcode.com/problems/range-sum-query-immutable/description/)
* ##### Invariant:
  prefixSum[i] always stores the sum of elements from index 0 to i. That must always be true. For every i.

* Code:

  class NumArray:
    def __init__(self, nums: List[int]):
        self.prefixSum = [0]*len(nums)
        self.prefixSum[0] = nums[0]
        for i in range(1, len(nums)):
            self.prefixSum[i] = self.prefixSum[i-1] + nums[i]
    def sumRange(self, left: int, right: int) -> int:
        if left == 0:
            return self.prefixSum[right]
        return self.prefixSum[right] - self.prefixSum[left-1]
