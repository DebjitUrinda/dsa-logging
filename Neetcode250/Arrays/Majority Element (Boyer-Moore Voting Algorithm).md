### Problem Statement (https://neetcode.io/problems/majority-element/question?list=neetcode250):
Given an array nums of size n, return the majority element.
The majority element is the element that appears more than ⌊n / 2⌋ times in the array. 
You may assume that the majority element always exists in the array.

===============================================

#### Boyer-Moore Voting Algorithm:

Cancellation idea (this is the core)
Pair up: One majority element, One non-majority element. They cancel each other.
Since majority > n/2: It will still remain at the end
🎯 So the real problem is: “Can you identify the element that remains after maximum possible cancellations?”

🔥 Why is this powerful?
Because: You don’t need sorting, You don’t need hashmap, You don’t need extra space
👉 This leads to *Boyer-Moore Voting Algorithm*
🧠 Intuition of optimal solution
   - Maintain: candidate count
    Rules:
    - If count = 0 → pick new candidate
    - If same → increment
    - If different → decrement

My Approach:

      class Solution:
       def majorityElement(self, nums: List[int]) -> int:
        count = 1
        elem = nums[0]

        for i in range(1,len(nums)):
            print("loop start:", count)
            if nums[i] == elem:
                count += 1

            elif nums[i] != elem:
                count -= 1
                if count==0:
                    elem = nums[i]
                    count = 1

            print("loop ends:", count)

        return elem

Cleaner model:

      class Solution:
       def majorityElement(self, nums: List[int]) -> int:
        count = 0
        elem = None

        for i in range(len(nums)):
            # print("loop start:", count)
            if count == 0:
                elem = nums[i]

            if nums[i] == elem:
                count += 1
            else:
                count -= 1

            # print("loop ends:", count)

        return elem
