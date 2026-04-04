### Problem Statement (https://neetcode.io/problems/sort-colors/question?list=neetcode250): 
You are given an array nums consisting of n elements where each element is an integer representing a color:

0 represents red
1 represents white
2 represents blue
Your task is to sort the array in-place such that elements of the same color are grouped together and arranged in the order: red (0), white (1), and then blue (2).

You must not use any built-in sorting functions to solve this problem.

What are we actually trying to solve?
At a deeper level:
❓ “Can you efficiently partition an array into categories in a single pass?”
This is not general sorting
This is classification + grouping

My first try:

    lt, rt = 0, len(nums)-1

        for i in range(len(nums)):
            if nums[i]==0:
                nums[lt], nums[i] = nums[i], nums[lt]
                lt += 1
            elif nums[i]==2:
                nums[rt], nums[i] = nums[i], nums[rt]
                rt -= 1

        print(nums)

I did a mistake here, as it will fail for [2, 0, 1] because the 1 is not tracked, I am only using left and right pointer to track 0 and 2, but what about 1?

Correct solution (track with only mid pointer):

    class Solution:
      def sortColors(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        low, mid, high = 0, 0, len(nums)-1

        while mid<=high:
            if nums[mid] == 0:
                nums[low], nums[mid] = nums[mid], nums[low]
                mid += 1
                low += 1

            elif nums[mid] == 1:
                mid += 1

            else:
                nums[high], nums[mid] = nums[mid], nums[high]
                high -= 1

Edge Cases:

Verbal explanation:
