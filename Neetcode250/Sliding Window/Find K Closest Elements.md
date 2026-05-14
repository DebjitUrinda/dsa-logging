### Problem Statement (https://neetcode.io/problems/find-k-closest-elements/question?list=neetcode250):
You are given a sorted integer array arr, two integers k and x, return the k closest integers to x in the array. The result should also be sorted in ascending order.

An integer a is closer to x than an integer b if:

|a - x| < |b - x|, or
|a - x| == |b - x| and a < b

===========================================================================================

**INVARIANTS**

#### My invariant:
After every iteration with a window size maximum of k there should exist all the elements inside the window that satisfies the condition: |a - x| < |b - x|, or |a - x| == |b - x| and a < b, based on the end elements of the window

#### Better invariant:
When the window grows to size k + 1, one boundary element is removed because it is less preferable than the other boundary.

===========================================================================================

**Solution**

#### My solution
    class Solution:
      def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        left = 0
        window = []

        for right in range(len(arr)):
            window.append(arr[right])

            if len(window) > k:
                a = window[left]
                b = window[right]

                diff1 = abs(a-x)
                diff2 = abs(b-x)

                if diff1 < diff2:
                    return window[:k]
                elif diff1 == diff2:
                    if a < b:
                        return window[:k]
                    else:
                        left += 1

        return window[left:left+k]

  #### Correct Solution (I was returning too early)
    class Solution:
      def findClosestElements(self, arr: List[int], k: int, x: int) -> List[int]:
        left = 0
        window = []

        for right in range(len(arr)):
            window.append(arr[right])

            if len(window) > k:
                a = window[0]
                b = window[-1]

                diff1 = abs(a-x)
                diff2 = abs(b-x)

                if diff1 < diff2 or (diff1 == diff2 and a < b):
                    window.pop()       # remove last element
                else:
                    window.pop(0)

        return window
