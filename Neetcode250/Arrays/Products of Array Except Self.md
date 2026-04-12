
# -NOTE-: I am very weak at index solving and creating loops for 1-d and 2-d arrays

### Problem Statement (https://neetcode.io/problems/products-of-array-discluding-self/question):

Given an integer array nums, return an array output where output[i] is the product of all the elements of nums except nums[i].

Each product is guaranteed to fit in a 32-bit integer.

Follow-up: Could you solve it in O(n) time without using the division operation?

===================================================================================================

My first approach was to use division, but that will fail in case of division by 0.

My correct approach:

    class Solution:
      def productExceptSelf(self, nums: List[int]) -> List[int]:
        size = len(nums)

        prefixList = [1] * size
        suffixList = [1] * size
        output = [1] * size

        # Build prefix products
        for i in range(1, size):
            prefixList[i] = prefixList[i - 1] * nums[i - 1]

        # Build suffix products
        for i in range(size - 2, -1, -1):
            suffixList[i] = suffixList[i + 1] * nums[i + 1]

        # Combine
        for i in range(size):
            output[i] = prefixList[i] * suffixList[i]

        return output
