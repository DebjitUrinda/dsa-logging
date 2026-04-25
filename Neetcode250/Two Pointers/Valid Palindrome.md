### Problem Statement (https://neetcode.io/problems/is-palindrome/question?list=neetcode250):

Given a string s, return true if it is a palindrome, otherwise return false.

A palindrome is a string that reads the same forward and backward. 
It is also case-insensitive and ignores all non-alphanumeric characters.

Note: Alphanumeric characters consist of letters (A-Z, a-z) and numbers (0-9).

==============================================================================

#### Invariant:
-your invariant should track what has already been proven, not just what is compared next.-
All valid mirrored characters outside [l, r] have already been matched; 
only the substring between l and r remains unresolved.

==============================================================================

#### My first solution (takes too much time):
    class Solution:
      def isPalindrome(self, s: str) -> bool:
        # regex = [a-zA-Z0-9]
        s_alnum = ""

        for c in s:
            if c.isalnum():
                if c.isalpha():
                    s_alnum += c.lower()
                else:
                    s_alnum += c

        l, r = 0, len(s_alnum)-1
        while l<r:
            if s_alnum[l] != s_alnum[r]:
                return False
            l += 1
            r -= 1

        return True

#### Solution without any extra space:
    class Solution:
      def isPalindrome(self, s: str) -> bool:
        l, r = 0, len(s) - 1

        while l < r:
            while l < r and not s[l].isalnum():
                l += 1

            while l < r and not s[r].isalnum():
                r -= 1

            if s[l].lower() != s[r].lower():
                return False

            l += 1
            r -= 1

        return True
