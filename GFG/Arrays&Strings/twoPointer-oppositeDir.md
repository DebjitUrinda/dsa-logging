## 9th Jan 2026
### 1. Pair with given sum in a sorted array:
_Why two pointer in different direction and not the same direction:_
**Problem Type**:
Two pointers (opposite direction)
Counting index pairs, not just finding existence
Sorted array with duplicates allowed

**Invariants**:
Array is sorted
lt < rt
All pairs with indices:
< lt or > rt are already processed
Pointer movement never revisits indices
When sum == target:
All combinations using current values are counted before moving pointers
If any of these break → logic is wrong.

**Mistakes I made**:
1. Assumed “one match = one pair”
When arr[lt] + arr[rt] == target, I incremented count by 1
This ignores duplicate elements
Result: undercounting valid index pairs

2. Moved pointers blindly after a match
Did:
lt += 1
rt -= 1
when arr[lt] + arr[rt] == target
This skips multiple valid combinations involving duplicates
Pointer movement was correct for existence problems, not for counting problems

4. Didn’t distinguish between value-level pairs and index-level pairs
Problem counts (i, j) index pairs
I was implicitly counting unique value pairs
These are not the same thing when duplicates exist

**Key Question to Ask Before Coding**
“Am I finding a pair, or counting how many index pairs exist?”

**Fix**:
Core Fix
When arr[lt] + arr[rt] == target, count how many indices are represented, not just one pair.
There are two cases:
_Case 1_: arr[lt] != arr[rt]
Let:
left_count = number of times arr[lt] repeats
right_count = number of times arr[rt] repeats
Number of pairs contributed:
left_count * right_count
Move pointers by entire groups, not by 1

_Case 2_: arr[lt] == arr[rt]
All elements between lt and rt are equal
Let:
k = rt - lt + 1
Number of valid pairs:
k * (k - 1) / 2
Done — break the loop


Time spent: 2 hours
Similar problems: Reverse array in groups


### 2. Trapping Rain Water:
_Why two pointer in different direction and not the same direction:_
**Problem Type**:
Two pointers (opposite direction)
Pointer movement is invariant-driven, not comparison driven.

**Invariants**:
Core Invariant: The side with the smaller max boundary can be safely resolved.

**Mistakes I made**:
1. Thought of two pointers in same direction given the array: [3, 0, 1, 0, 4, 0 2]. But it will fail if array is [5, 2, 1, 0, 4]

**Formula grounding the solution:**
water[i] = min(max_left, max_right) - height


Time spent: 50 mins
Revise this from the chat in ChatGPT, go over the mistakes and the max boundary part
