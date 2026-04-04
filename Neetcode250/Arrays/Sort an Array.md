Problem Statement (https://neetcode.io/problems/sort-an-array/question?list=neetcode250):

You are given an array of integers nums, sort the array in ascending order and return it.
NOTE: You must solve the problem without using any built-in functions in O(nlog(n)) time complexity and with the smallest space complexity possible.

What are we actually trying to solve?
The real question is:
❓ “Can you implement an efficient general-purpose sorting algorithm from scratch?”

🔑 Core insight
This problem is asking:
“Can you perform divide and conquer efficiently?”

They eliminate easy options:
❌ Bubble / Selection / Insertion sort
O(n²) → too slow
❌ Using sorted() / .sort()
Not allowed
So you're forced into:
✅ Advanced sorting algorithms
🧠 What this problem is really testing
1. Do you know core sorting algorithms?
You should recognize:
1. Merge Sort: Time: O(n log n) ✅; Space: O(n) ❌ (extra array)
2. Quick Sort: Time: O(n log n) average ✅; Space: O(log n) (recursion) ✅; In-place ✅
3. Heap Sort: Time: O(n log n) ✅; Space: O(1) ✅; Harder to implement


Chatgpt solution:
    
    class Solution:
        def sortArray(self, nums: List[int]) -> List[int]:
          def quicksort(l, r):
            if l >= r:
                return
            
            pivot = nums[r]
            p = l

            for i in range(l, r):
                if nums[i] < pivot:
                    nums[p], nums[i] = nums[i], nums[p]
                    p += 1

            nums[p], nums[r] = nums[r], nums[p]

            quicksort(l, p - 1)
            quicksort(p + 1, r)

        quicksort(0, len(nums) - 1)
        return nums

This approach fails for worst case, as we have taken pivot to be the rightmost element. The worst case scenarios are:
1. Worst-case time complexity
    With this partition scheme, if the pivot ends up being the smallest or largest element repeatedly (e.g., already sorted input), you get O(n^2) time.
    Mitigation: choose a random pivot (or shuffle first) to get average O(n log n) behavior.
2. Depth of recursion on large inputs
    Python recursion depth can blow up for large n in worst-case scenarios.
    Mitigation: either implement an iterative version, or switch to a more robust quicksort variant (e.g., introsort) or ensure the recursion depth stays         manageable with randomized pivot.

Correct solution is to use a random pivot:

    import random
    from typing import List

    class Solution:
      def sortArray(self, nums: List[int]) -> List[int]:
        def quicksort(l, r):
            if l >= r:
                return
            # Random pivot to avoid worst-case behavior
            pivot_index = random.randint(l, r)
            nums[pivot_index], nums[r] = nums[r], nums[pivot_index]

            pivot = nums[r]
            p = l
            for i in range(l, r):
                if nums[i] < pivot:
                    nums[p], nums[i] = nums[i], nums[p]
                    p += 1

            nums[p], nums[r] = nums[r], nums[p]

            quicksort(l, p - 1)
            quicksort(p + 1, r)

        quicksort(0, len(nums) - 1)
        return nums


Time: average O(n log n); worst-case O(n^2) (mitigated by random pivot).
Space: O(log n) due to recursion stack (best possible for in-place quicksort in most cases).
If you want to guarantee better worst-case performance and still avoid builtin sorts, you could implement a hybrid (introsort) or switch to a non-recursive/iterative approach.


Edge cases:

Verbal explanation:
