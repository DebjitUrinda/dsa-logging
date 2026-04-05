What are we actually trying to solve?
At the core:
❓ “From a dataset, how do I efficiently extract the top k most important items?”

Core patterns behind this problem
This problem is a mix of:
✅ HashMap (counting)
✅ Heap OR Bucket Sort (selection)

Clean explanation:
“First, I compute the frequency of each element using a hashmap.
Then, instead of sorting, I use bucket sort where indices represent frequency.
Finally, I iterate from highest frequency to lowest and collect k elements.”

🧪 Edge cases
1. All elements same
[5,5,5,5], k=1
2. All unique
[1,2,3,4], k=2
3. k = 1
👉 Just max frequency
4. k = number of unique elements
👉 return all

What I was trying to do:
👉 “Give me all elements whose frequency is ≥ k”

    class Solution:
      def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        countMap = {}
        output = []

        for i in nums:
            if i not in countMap:
                countMap[i] = 1
            else:
                countMap[i] += 1

        for j in countMap:
            if countMap[j]>=k:
                output.append(j)

        return output

🧠 But the problem is asking:
❓ “Give me the top k most frequent elements”

    class Solution:
      def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        countMap = {}

        for i in nums:
            if i not in countMap:
                countMap[i] = 1
            else:
                countMap[i] += 1

        sorted_items = sorted(countMap.items(), key=lambda x: x[1], reverse=True)

        output = [item[0] for item in sorted_items[:k]]

        return output
