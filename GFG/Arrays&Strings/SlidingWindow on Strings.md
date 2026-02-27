## Core Insight
Sliding window must always follow this order:
Expand right pointer
Shrink left pointer until invariant is restored
Measure result only when window is valid
This guarantees:
Correctness
True O(n) complexity (each pointer moves at most n times)
Key Invariant
At every measurement step, the window contains only unique characters.

### q1. Longest Substring Without Repeating Characters (https://www.geeksforgeeks.org/problems/longest-distinct-characters-in-string5848/1)
Initial Approach Issues  
  While implementing the sliding window solution for Longest Substring Without Repeating Characters, the following logical mistakes were present:
  Used if instead of while
  The window was shrunk only once when a duplicate was detected.
  This failed in cases where multiple removals were required to restore validity.
    Violated the invariant:
&emsp All characters inside the window must have frequency ≤ 1.  
Incorrect frequency decrement  
  Used counter[left] -= 1
  This incorrectly treated left as a character index (0–25).
  Correct approach requires:
&emspch = ord(s[left]) - ord('a')
&emspcounter[ch] -= 1  
Updated max length during invalid window  
  Length was computed inside the shrinking loop.
  This measured substrings while the window was still invalid.
  Sliding window requires measuring only after invariant restoration.  
Unnecessary substring slicing  
  Used temp = s[left:i]
  This introduced unnecessary O(n) operations.
  Replaced with length calculation:
    i - left + 1
