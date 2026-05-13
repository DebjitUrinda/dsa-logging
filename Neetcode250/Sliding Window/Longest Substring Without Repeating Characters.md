### Problem Statement (https://neetcode.io/problems/longest-substring-without-duplicates/question?list=neetcode250):
Given a string s, find the length of the longest substring without duplicate characters.

A substring is a contiguous sequence of characters within a string.

=================================================================================

**INVARIANTS**:
#### My invariant:
After each iteration, the current window contains no duplicate characters, and left is the smallest index that makes the window valid.

=================================================================================

**Solution**:

    class Solution:
      def lengthOfLongestSubstring(self, s: str) -> int:
        last_seen = {}
        left = 0
        longest = 0

        for right in range(len(s)):
            ch = s[right]

            if ch in last_seen:
                left = max(left, last_seen[ch] + 1)

            last_seen[ch] = right
            longest = max(longest, right - left + 1)

        return longest
