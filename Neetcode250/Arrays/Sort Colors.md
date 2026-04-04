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

Edge Cases (My first try would fail for most of these edge cases):
1. Empty / Single element
2. Already sorted
3. Reverse sorted.
4. All same values

Verbal explanation:
1. Problem understanding (10–15 sec)
“We are given an array with only 0, 1, and 2. The goal is to sort it in-place so that all 0s come first, then 1s, then 2s.”
2. Key observation (this is where you stand out)
“Since there are only 3 distinct values, we don’t need general sorting. We can partition the array into three regions.”
3. Approach (core idea)
“I’ll use a three-pointer approach:
low → next position for 0
mid → current element
high → next position for 2
We iterate while mid <= high.”
4. Invariants (THIS is the real signal of understanding)
“At any point:
Elements before low are all 0
Elements after high are all 2
Elements between low and mid are 1s
Remaining are unprocessed”
5. Transitions (cases)
“If:
nums[mid] == 0 → swap with low, move both
nums[mid] == 1 → just move mid
nums[mid] == 2 → swap with high, move high only (don’t move mid because we need to re-evaluate)”
6. Complexity
“Time complexity is O(n) since we process each element at most once. Space complexity is O(1) since it’s in-place.”
7. Edge case mention (quick)
“This handles edge cases like all same elements, reverse order, and cases like [2,0,1] where re-evaluation is required.”
