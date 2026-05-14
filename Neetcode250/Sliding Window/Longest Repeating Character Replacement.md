### Problem Statement (https://neetcode.io/problems/longest-repeating-substring-with-replacement/question?list=neetcode250):
You are given a string s consisting of only uppercase english characters and an integer k. You can choose up to k characters of the string and replace them with any other uppercase English character.

After performing at most k replacements, return the length of the longest substring which contains only one distinct character.

==========================================================================================

**INVARIANTS**

#### My invariant (wrong)
After each iteration the window is valid only if it has one distinct character

#### Correct Invariant
After each iteration, the current window s[left:right+1] satisfies: (right - left + 1) - max_frequency <= k

==========================================================================================

**My solution**:

    class Solution:
      def characterReplacement(self, s: str, k: int) -> int:
        left = 0
        freq = {}
        max_length = 0
        check = 0

        for right in range(len(s)):
            if s[right] not in freq:
                freq[s[right]] = 1
            else:
                freq[s[right]] += 1
                for ch in s[:right+1]:
                    temp = freq[ch]
                    if max_length < temp:
                        max_length = temp
                check = (right - left + 1)
                if check - max_length > k:
                    left += 1
        
        return check

**Correct Solution**

    class Solution:
      def characterReplacement(self, s: str, k: int) -> int:
        left = 0
        freq = {}
        max_freq = 0      # highest frequency in the current window
        max_length = 0    # best answer found so far

        for right in range(len(s)):
            # Add current character to the window
            if s[right] not in freq:
                freq[s[right]] = 1
            else:
                freq[s[right]] += 1

            # Update max frequency in the window
            if freq[s[right]] > max_freq:
                max_freq = freq[s[right]]

            # Shrink window until it becomes valid
            while (right - left + 1) - max_freq > k:
                freq[s[left]] -= 1
                left += 1

            # Update the best answer
            if right - left + 1 > max_length:
                max_length = right - left + 1

        return max_length
