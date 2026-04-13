### Problem Statement (https://neetcode.io/problems/longest-consecutive-sequence/question?list=neetcode250):
Given an array of integers nums, return the length of the longest consecutive sequence of 
elements that can be formed.

A consecutive sequence is a sequence of elements in which each element is 
exactly 1 greater than the previous element. The elements do not have to be consecutive in the original array.

You must write an algorithm that runs in O(n) time.

==================================================================

What are we really detecting?
- We want to identify:
  Where a sequence starts. Then count how long it continues

What is an invariant?
An invariant is something that remains true while your algorithm runs.
It’s the rule you rely on so the logic stays correct.
Think of it as:
“No matter where I am in the loop, this fact is still true.”

In this problem, the key invariant is:
We only start counting from the beginning of a sequence.

Meaning:
    
    num - 1 not in set
    
If true, then num is the first number in that streak.
So every sequence is counted exactly once.

==================================================================

My current approach:

    class Solution:
      def longestConsecutive(self, nums: List[int]) -> int:
        size = len(nums)
        hashSet = set(nums)
        visited = [0]*size

        sequence = 0

        for i in range(size):
            search = nums[i]
            while search-1 in hashSet and visited[i]!=1:
                sequence += 1
                visited[i] = 1
                search -= 1
                if i+1 == size:
                    return sequence

        return sequence

  What I did:
  
    I chose every element and searched backward:
      while search - 1 in hashSet

    Implicit idea:
    “If smaller numbers exist, they are connected.”
    That part is reasonable.
    But there’s no stable rule for when to start or when to stop counting globally.
    You start from many positions, including middle elements.
    Example:
      From 4 you count backward to 1
      From 3 you again count backward to 1
      Same sequence processed multiple times.


  Mental Model
    My version says:
    Let me inspect every house and walk backward to find where the street begins.
  Correct version says:
    Only houses with no house on the left can be street starts.


Correct Solution:

    class Solution:
      def longestConsecutive(self, nums: List[int]) -> int:
        hashSet = set(nums)
        longest = 0

        for i in hashSet:
            if i-1 not in hashSet:
                sequence = 1
                while i+sequence in hashSet:
                    sequence += 1
                longest = max(longest, sequence)

        return longest
