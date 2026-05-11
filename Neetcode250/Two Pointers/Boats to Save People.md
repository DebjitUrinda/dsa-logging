### Problem Statement (https://neetcode.io/problems/boats-to-save-people/question?list=neetcode250):
You are given an integer array people where people[i] is the weight of the ith person, and an infinite number of boats where each boat can carry a maximum weight of limit. Each boat carries at most two people at the same time, provided the sum of the weight of those people is at most limit.

Return the minimum number of boats to carry every given person.

================================================================================

#### INVARIANTS
**Correct Invariant**:
- After each iteration, all people outside the range people[left:right+1] have already been assigned to boats using the minimum possible number of boats, and boats stores exactly that minimum count.
  *-NOTE-*: We need to sort the array for this

**My other thinking**:
Hashmap instead of sorting. But this won't work because:
* Hash map is designed for exact key lookup, but this problem requires finding the largest available weight `<= limit - current_weight`.
* No inherent ordering, so efficiently locating the best valid partner is difficult.
* May require scanning multiple candidate weights for each person.
* Using a `visited` array can lead to repeated scans of already-checked elements.
* Worst-case time complexity can degrade to `O(n²)`.
* More complex bookkeeping for counts and visited states.
* Harder to reason about and prove optimality compared with sorted two-pointer approach.
* Sorted two-pointer solution directly uses the lightest and heaviest remaining people, yielding a simple `O(n log n)` algorithm (sorting dominates).

================================================================================

#### Solution:
**My solution**:
    
    class Solution:
      def numRescueBoats(self, people: List[int], limit: int) -> int:
        people.sort()
        light, heavy = 0, len(people)-1
        counter = 0
        print(people)
        while light <= heavy:
            max_weight = people[light] + people[heavy]
            if max_weight <= limit:
                counter += 1
                light += 1
                heavy -= 1
            elif max_weight > limit:
                if people[heavy] <= limit:
                    counter += 1
                heavy -= 1

        return counter

**Simplified Solution**: Heavy always has to go irrespective of whether we find a pair or not, this ensures that counter += 1 in every loop.

    class Solution:
      def numRescueBoats(self, people: List[int], limit: int) -> int:
        people.sort()
        light, heavy = 0, len(people)-1
        counter = 0
        
        while light <= heavy:
            if people[light] + people[heavy] <= limit:
                light += 1
            heavy -= 1
            counter += 1

        return counter
