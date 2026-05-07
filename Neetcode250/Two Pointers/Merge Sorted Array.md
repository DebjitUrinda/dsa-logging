### Problem Statment (https://neetcode.io/problems/merge-sorted-array/question?list=neetcode250):
You are given two integer arrays nums1 and nums2, both sorted in non-decreasing order, along with two integers m and n, where:

m is the number of valid elements in nums1,
n is the number of elements in nums2.
The array nums1 has a total length of (m+n), with the first m elements containing the values to be merged, and the last n elements set to 0 as placeholders.

Your task is to merge the two arrays such that the final merged array is also sorted in non-decreasing order and stored entirely within nums1.
You must modify nums1 in-place and do not return anything from the function.

==================================================================================

#### Invariant:
**My Invariant** : the resultant array must have all the elements from both the first and second array and in correct order of non-decreasing elements

**Tighter Invariant**: After each iteration, elements in nums1[k+1 ... m+n-1] are the largest (m+n-1 - k) elements from the union of both arrays, in sorted order.

**Mental shortcut**: “I am filling nums1 from the back, and whatever I’ve filled is already perfect.”

==================================================================================

#### Solution:
  
    class Solution:
      def merge(self, nums1: List[int], m: int, nums2: List[int], n: int) -> None:
        """
        Do not return anything, modify nums1 in-place instead.
        """
        k = m+n-1
        i = m-1
        j = n-1

        while j >= 0:
            if i>=0 and nums1[i] >= nums2[j]:
                nums1[k] = nums1[i]
                i -= 1
            else:
                nums1[k] = nums2[j]
                j -= 1
            print(nums1)
            k -= 1
