## Sliding Window in One Page

### Two Pointers
* Two indices used to navigate the array.
* Elements between them may not matter.

### Sliding Window
* A special case of two pointers.
* The entire range `[left, right]` matters.
* This range is your current candidate.

---

## Valid Window
> A valid window is any window that satisfies the problem’s condition.
You decide what “valid” means based on the problem.

Examples:
* No duplicates.
* At most `k` distinct elements.
* Contains all required characters.
* Contains only the last `k` elements.

---

## Invalid Window
> A window that violates the condition.

When invalid:
* Move `left` to shrink the window until it becomes valid again.

---

## Core Pattern
1. Expand window (`right += 1`)
2. Update state
3. If invalid, shrink (`left += 1`)
4. Use the valid window to update the answer

---

## Invariant
> A condition that is always true during the algorithm.

Example:
* “The window always contains the last `k` elements.”
* “The window always has no duplicates.”

---

## Main Insight
> In sliding window, **you define what makes the window valid**, and the algorithm maintains that condition throughout execution.
