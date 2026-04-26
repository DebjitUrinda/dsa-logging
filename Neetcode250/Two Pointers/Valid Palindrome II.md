### Problem Statement (https://neetcode.io/problems/valid-palindrome-ii/question?list=neetcode250):
You are given a string s, 
return true if the s can be a palindrome after deleting at most one character from it.

A palindrome is a string that reads the same forward and backward.

Note: Alphanumeric characters consist of letters (A-Z, a-z) and numbers (0-9).

================================================================================

#### Invariants:

My first invariant:
- After every iteration (starting from middle of the string and pointers going outside)
- the inner substring is already in palindrome,
- if after removing a character that inner palindrome breaks, then palindrome not possible

**Correct Invariant:**
Before using the one deletion, all checked outer pairs match; at the first mismatch, 
one of the two resulting inner substrings must be a palindrome.

================================================================================

#### My first solution:
    class Solution:
      def validPalindrome(self, s: str) -> bool:
        l, r = 0, len(s)-1
        
        while l<r:
            if s[l] == s[r]:
                l += 1
                r -= 1
            elif s[l] != s[r]:
                if s[l+1] == s[r] and l+1!=r:
                    lt = l+1
                    rt = r
                    while lt<rt:
                        if s[lt] == s[rt]:
                            lt += 1
                            rt -= 1
                        else:
                            return False
                else:
                    lt = l
                    rt = r-1
                    while lt<rt:
                        if s[lt] == s[rt]:
                            lt += 1
                            rt -= 1
                        else:
                            return False

        return True

*Problems:*
### Valid Palindrome II – Why My Initial Approach Failed

**Core Idea Was Correct:**
Use two pointers, and on first mismatch try deleting one side.

**Why the Implementation Failed:**

1. **No pointer progress after mismatch check**
   After validating a skipped substring, the main `l` and `r` were never updated or returned, so the outer loop could repeat forever on the same mismatch.

2. **Greedy branch choice was unsafe**
   Used immediate check like `s[l+1] == s[r]` to decide which side to delete.
   This can choose the wrong branch because local character match does not guarantee the whole remaining substring is palindrome.

3. **Should test both valid options**
   At first mismatch, only two legal moves exist:

* skip left character
* skip right character

Need to verify whether either remaining substring is palindrome.

4. **Extra adjacency condition was unnecessary**
   Checks like `l+1 != r` can reject valid short cases and complicate logic.

**Counterexample Pattern:**
A string may have `s[l+1] == s[r]`, but deleting left still fails later, while deleting right succeeds. Local match is not enough; full substring validation is required.

**Correct Strategy:**
On first mismatch, return:
`isPalindrome(l+1, r) or isPalindrome(l, r-1)`

**One-line Learning:**
When one deletion is allowed, never choose based on immediate neighbors alone—validate the full remaining substring.



**NOTE:**
Correct Solution is you have to use the stack approach as you need to verify each substring
with the valid palindrome logic.

#### Solution:
    class Solution:
      def validPalindrome(self, s: str) -> bool:
        def is_pal(l, r):
            while l < r:
                if s[l] != s[r]:
                    return False
                l += 1
                r -= 1
            return True

        l, r = 0, len(s) - 1

        while l < r:
            if s[l] == s[r]:
                l += 1
                r -= 1
            else:
                return is_pal(l + 1, r) or is_pal(l, r - 1)

        return True
