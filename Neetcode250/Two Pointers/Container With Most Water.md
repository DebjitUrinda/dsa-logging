### Problem Statement (https://neetcode.io/problems/max-water-container/question?list=neetcode250):
You are given an integer array heights where heights[i] represents the height of the ith bar.

You may choose any two bars to form a container. Return the maximum amount of water a container can store.

====================================================================================

#### INVARIANTS:
**My Invariant**:
- Starting with two pointers one leftmost and one rightmost, after each iteration I must verify and reject the pointer contributing to the smaller bar height but keep track of the area.

**Corrected Invariant**:
After each iteration, the best area so far is stored in max_area, and the shorter bar is discarded because no future container using that bar can improve the answer.

====================================================================================

#### Solution:
    class Solution:
      def maxArea(self, heights: List[int]) -> int:
        left, right = 0, len(heights)-1
        max_area = 0

        while left<right:
            width = right-left
            height = min(heights[left], heights[right])
            area = width * height

            if max_area < area:
                max_area = area

            if heights[left] <= heights[right]:
                left += 1

            elif heights[left] > heights[right]:
                right -= 1
        
        return max_area
