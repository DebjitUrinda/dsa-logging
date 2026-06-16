### Problem Statement (https://neetcode.io/problems/capacity-to-ship-packages-within-d-days/question?list=neetcode250):
A conveyor belt has packages that must be shipped from one port to another within days days.

The ith package on the conveyor belt has a weight of weights[i]. Each day, we load the ship with packages on the conveyor belt (in the order given by weights). It is not allowed to load weight more than the maximum weight capacity of the ship.

Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within days days.

================================================================================

### INVARIANT
**Invariant:**
After each binary-search iteration, the remaining search interval must still contain the minimum feasible capacity.

================================================================================

### SOLUTION
    class Solution:
      def shipWithinDays(self, weights: List[int], days: int) -> int:
        low = max(weights)      # minimum possible capacity
        high = sum(weights)     # maximum possible capacity

        while low < high:
            mid = (low + high) // 2

            if self.canShip(weights, mid, days):
                high = mid
            else:
                low = mid + 1

        return low

      def canShip(self, weights, capacity, days):
        days_used = 1
        current_load = 0

        for weight in weights:
            if current_load + weight <= capacity:
                current_load += weight
            else:
                days_used += 1
                current_load = weight

        return days_used <= days
