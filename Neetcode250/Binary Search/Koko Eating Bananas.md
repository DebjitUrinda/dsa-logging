### Problem Statement (https://neetcode.io/problems/eating-bananas/question?list=neetcode250):
You are given an integer array piles where piles[i] is the number of bananas in the ith pile. You are also given an integer h, which represents the number of hours you have to eat all the bananas.

You may decide your bananas-per-hour eating rate of k. Each hour, you may choose a pile of bananas and eats k bananas from that pile. If the pile has less than k bananas, you may finish eating the pile but you can not eat from another pile in the same hour.

Return the minimum integer k such that you can eat all the bananas within h hours.

====================================================================================

### INVARIANT:
**Correct Invariant**:
At the start of each iteration, the first True in the implicit array 1..max(piles) lies within the current search interval [low, high].

====================================================================================

### SOLUTION:
    class Solution:
      import math
      def minEatingSpeed(self, piles: List[int], h: int) -> int:
        low, high = 1, max(piles)
        rate = 1

        while low <= high:
            mid = (low + high) // 2
            # flag = self.canFinish(piles, mid, h)
            if self.canFinish(piles, mid, h):
                high = mid - 1
            else:
                low = mid + 1

            rate = low

        return rate

      def canFinish(self, piles: List[int], k, h) -> bool:
        hours = sum(math.ceil(pile/k) for pile in piles)
        if hours <= h:
            return True

        return False
