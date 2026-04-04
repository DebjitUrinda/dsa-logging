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
Merge Sort: Time: O(n log n) ✅; Space: O(n) ❌ (extra array)
Quick Sort: Time: O(n log n) average ✅; Space: O(log n) (recursion) ✅; In-place ✅
Heap Sort: Time: O(n log n) ✅; Space: O(1) ✅; Harder to implement

Edge cases:

Verbal explanation:
