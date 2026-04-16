### Problem Statement (https://neetcode.io/problems/subarray-sum-equals-k/question):

You are given an array of integers nums and an integer k, 
return the total number of subarrays whose sum equals to k.

A subarray is a contiguous non-empty sequence of elements within an array.

========================================================================

One liner invariant:
History first, lookup second, store current third.

--------------------

My first Approach:

    class Solution:
      def subarraySum(self, nums: List[int], k: int) -> int:
        count, prefixSum = 0, 0

        for num in nums:
            prefixSum += num
            if prefixSum == k:
                count += 1
                prefixSum = 0

        return count

I treated the running sum like this:
- Keep accumulating.
- When sum becomes k, count one answer and reset.

Issue: Misses overlapping / alternate starting positions.
Fix: Track frequencies of all previous prefix sums; each prefix-k match gives a valid subarray.

#### Don’t reset the sum | store the history of sums.

--------------------

My second approach:

    class Solution:
      def subarraySum(self, nums: List[int], k: int) -> int:
        count, prefixSum = 0, 0
        oldPrefix = 0

        for i in range(len(nums)):
            prefixSum += nums[i]
            if prefixSum == k or prefixSum-k == oldPrefix:
                count += 1
                oldPrefix = prefixSum

        return count

Why It Still Fails: Because there is not just one earlier prefix.

There can be:
- many earlier prefix sums
- same prefix appearing multiple times
- multiple valid subarrays ending at the same index
- I need all previous prefixes, not the latest one.

---------------------

Correct approach:

    class Solution:
      def subarraySum(self, nums: List[int], k: int) -> int:
        freq = {0:1}
        prefix = 0
        count = 0

        for num in nums:
            prefix += num
            count += freq.get(prefix - k, 0)
            freq[prefix] = freq.get(prefix, 0) + 1

        return count

  Deeper intuition:
  - The algorithm does not search subarrays directly.
  - It counts pairs of prefix sums whose difference is k
