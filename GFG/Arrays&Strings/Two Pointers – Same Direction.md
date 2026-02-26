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
