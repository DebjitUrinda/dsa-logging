## Invariant: slow = last valid index, fast = scanner

### q1. Remove Duplicates Sorted Array (https://www.geeksforgeeks.org/problems/remove-duplicate-elements-from-sorted-array/1)
Initial attempt used a slow pointer and a separate list but had two issues: (look at the Gfg submissions)

1. `uniq` was incorrectly initialized as an integer instead of a list.
2. Logic was more complex than necessary for a sorted array.

Observation:
Since the array is sorted, duplicates are always adjacent.
We only need to compare each element with its previous one.

Refactored solution to:
- Remove unnecessary slow pointer
- Compare arr[i] with arr[i-1]
- Append only when value changes

Time Complexity: O(n)
Space Complexity: O(n) (for new list)

Also noted in-place two-pointer variant for optimal space.
#### Insight
Sorted array ⇒ duplicates are adjacent.
Only compare current element with previous element.
No extra memory structures needed.


### q2. Move all Zeroes to End of Array (https://www.geeksforgeeks.org/problems/move-all-zeroes-to-end-of-array0751/1)
refactor: replace incorrect zero-shifting attempts with stable two-pointer invariant

Previous attempts:
- Used adjacent swaps (bubble-style) based on arr[i-1] == 0
  → Inefficient movement of zeroes (one step at a time)
  → No clear invariant for `slow`
  → Conceptually unstable logic

- Tried reverse traversal pushing zeros from end
  → Broke relative order of non-zero elements
  → Violated problem stability requirement

Final solution:
- Implemented fast/slow pointer pattern
- Invariant: [0..slow) always contains non-zero elements in original order
- Single pass, O(n) time, O(1) space
- Maintains stability correctly
