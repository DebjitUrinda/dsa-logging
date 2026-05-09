### Problem Statement (https://neetcode.io/problems/merge-strings-alternately/question?list=neetcode250):
You are given two strings, word1 and word2. Construct a new string by merging them in alternating order, starting with word1 — take one character from word1, then one from word2, and repeat this process.

If one string is longer than the other, append the remaining characters from the longer string to the end of the merged result.

Return the final merged string.

====================================================================================

#### INVARIANTS
**My Invariant**: 
- After each iteration my resultant string will have the merged alternate characters from the left.

**Better Invariant**:
- After each iteration, the result string contains the first i characters of word1 and the first j characters of word2, merged in alternating order starting with word1.

====================================================================================

#### Solution:
    class Solution:
      def mergeAlternately(self, word1: str, word2: str) -> str:
        l, r = 0, 0
        len1 = len(word1)
        len2 = len(word2)
        res = ""

        while l<len1 and r<len2:
            res = res + word1[l] + word2[l]
            l += 1
            r += 1

        if l == len1:
            res += word2[r:]
        else:
            res += word1[l:]

        return res 
