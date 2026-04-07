### Problem Statement (https://neetcode.io/problems/longest-common-prefix/question?list=neetcode250):
  You are given an array of strings strs. Return the longest common prefix of all the strings.
  If there is no longest common prefix, return an empty string "".

🧠 What are we actually trying to solve?
At the core:
❓ “What is the longest starting sequence shared by all strings?”

🧠 What are we actually trying to solve?
At the core:
❓ “What is the longest starting sequence shared by all strings?”
  1. Can you compare multiple inputs character by character?
  2. Can you handle multiple inputs cleanly? [This is not pairwise comparison.]
  3. Can you stop early? [As soon as mismatch happens.]

Edge Cases:
1. No common prefix, return ""
2. Empty list, return ""
3. Only one string: ["alone"], return "alone"
4. One empty string: ["", "alone"], return ""
5. All same strings

Verbal explanation:
- Using the shrink until valid strategy!!!

My approach:

    class Solution:
      def longestCommonPrefix(self, strs: List[str]) -> str:
        
        prefix = strs[0]

        for s in strs[1:]:
            while prefix not in s:
                prefix = prefix[:-1]
                if prefix == "":
                    return ""

        return prefix

Problem with this approach:
  prefix not in s
  This checks:❓ “Is prefix anywhere inside the string?”

Correct solution is:

    class Solution:
      def longestCommonPrefix(self, strs: List[str]) -> str:
        
        prefix = strs[0]

        for s in strs[1:]:
            while not s.startswith(prefix):
                prefix = prefix[:-1]
                if prefix == "":
                    return ""

        return prefix
