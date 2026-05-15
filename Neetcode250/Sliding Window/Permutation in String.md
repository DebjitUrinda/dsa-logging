### Problem Statement (https://neetcode.io/problems/permutation-string/question?list=neetcode250):
You are given two strings s1 and s2.

Return true if s2 contains a permutation of s1, or false otherwise. That means if a permutation of s1 exists as a substring of s2, then return true.

Both strings only contain lowercase letters.

=============================================================================

**INVARIANTS**

#### My Invariant:
After each iteration, the current window contains at most len(s1) characters, and its frequency map exactly reflects the characters inside the window. If the window size is len(s1) and the frequency map matches s1, then a permutation exists.

=============================================================================

### SOLUTION
**My solution**:

    class Solution:
      def checkInclusion(self, s1: str, s2: str) -> bool:
        freq_s1 = {}
        freq_s2 = {}
        left = 0

        for c in s1:
            if c not in freq_s1:
                freq_s1[c] = 1
            else:
                freq_s1[c] += 1

        for right in range(len(s2)):
            char = s2[right]
            if char not in freq_s2:
                freq_s2[char] = 1
            else:
                freq_s2[char] += 1

            if (right-left+1) == len(s1):
                if freq_s1 == freq_s2:
                    return True
                else:
                    left = right+1
            
        return False


**Correct solution**:
    
    class Solution:
      def checkInclusion(self, s1: str, s2: str) -> bool:
        freq_s1 = {}
        freq_s2 = {}
        left = 0

        for c in s1:
            if c not in freq_s1:
                freq_s1[c] = 1
            else:
                freq_s1[c] += 1

        for right in range(len(s2)):
            char = s2[right]
            if char not in freq_s2:
                freq_s2[char] = 1
            else:
                freq_s2[char] += 1

            # If window size exceeds len(s1), remove leftmost character
            if (right - left + 1) > len(s1):
                left_char = s2[left]
                freq_s2[left_char] -= 1

                if freq_s2[left_char] == 0:
                    del freq_s2[left_char]

                left += 1

            if (right-left+1) == len(s1):
                if freq_s1 == freq_s2:
                    return True
            
        return False

