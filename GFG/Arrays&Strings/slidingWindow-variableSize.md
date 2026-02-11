### Smallest window containing all characters
* Genius problem (https://www.geeksforgeeks.org/problems/smallest-window-in-a-string-containing-all-the-characters-of-another-string-1587115621/1)
  Problem to find the smallest substring in s consisting of all the characters (including duplicates) of the string p. Return empty string in case no such substring is present. If there are multiple such substring of the same length found, return the one with the least starting index.

  e.g. Input: s = "timetopractice", p = "toc"
       Output: "toprac"
       Explanation: "toprac" is the smallest substring in which "toc" can be found.
    1. ##### Invariant == Window is valid if it contains all characters of p with their required frequencies.
        So:
  * Define Validity: Clearly state when the window is valid v/s invalid
  * Encode Validity as a number: Track validity as a scalar (formed, matched, violations), not structures
  * Expand -> then repair: Always expand right, and shrink left to restore validity
  * Update answer only at the boundary: _Longest -> after expand right_ | _Smallest -> after shrink left_
    2️⃣ Encode the Invariant Efficiently
        Checking all 26 characters every step is inefficient.
        So reduce validity to a single condition:
          required → number of distinct characters in p
          formed → number of distinct characters currently satisfied
          Now:
          window is valid ⇔ formed == required
        Validity becomes O(1).
    3️⃣ Pointer Strategy (Core Sliding Window Pattern)
        Variable-size sliding window follows one universal structure:
        Expand right
        When window becomes valid → shrink left
        Track best answer while valid
        In short:
          Expand → Repair → Repeat
    4️⃣ Boundary Transitions Matter
        Two transitions control correctness:
        When expanding:
          if have[c] == need[c]:
          formed += 1
        Only increment when equality is reached.
        When shrinking:
          if have[c] < need[c]:
          formed -= 1
        Only decrement when requirement breaks.
    5️⃣ Tracking the Best Window
        When window is valid:
          currentLen = right - left + 1
          if currentLen < bestLen:
            bestLen = currentLen
            bestStart = left
        Do not build substrings during the loop.
        Store indices. Slice once at the end.
    6️⃣ Full Structural Template
        build need[]
        compute required
        left = 0
        formed = 0
        bestStart = -1
        bestLen = infinity
        for right in range(len(s)):
          include s[right] in window
          if requirement satisfied:
            formed += 1
          while formed == required:
            update best window
            remove s[left] from window
            if requirement broken:
              formed -= 1
            left += 1
        return best substring
    7️⃣ What This Experience Teaches
      🔹 Sliding window is not about pointers
        It is about maintaining an invariant efficiently.
      🔹 Validity must be encoded numerically
        Arrays/maps track state.
        A scalar (formed) tracks validity.
      🔹 Never reset state
        Sliding window repairs the window.
        It does not restart it.
      🔹 Debugging = invariant violation detection
        If the answer is wrong, check:
        Did formed change at the correct boundary?
        Did left shrink at the right time?
        Was the answer updated only when valid?
    8️⃣ Generalized Insight
        Algorithms work because they preserve invariants while making monotonic progress.
        Sliding window is just one example of that principle.
        Final One-Line Anchor
        Variable sliding window = monotonic pointers + invariant repair + boundary tracking.

### Longest Subarray with Sum K (positive)
* Mistake: 
  Apparently Sliding window only works for positive numbers, now the question is why did I not think of this question that I am working with an unsolvable method. The GFG problem I was working on (https://www.geeksforgeeks.org/problems/longest-sub-array-with-sum-k0809/1) includes negative number and ther only hashmap and indexing would work.

* 2nd attempt (failed):
*       alfabts = [0]*26
        result = 0
        # lt = 0
        
        for i in range(1, len(s)):
            asci = ord(s[i]) - 97
            if alfabts[asci] != 0:
                # alfabts[asci] += 1
                alfabts = [0]*26
                alfabts[asci] = 1
                result = 1
            elif alfabts[asci] == 0:
                alfabts[asci] += 1
                result += 1
                
        return result

REASON: 
1. I never removed old characters = Once a character appeared, my code never “forgot” it. Sliding window requires removing characters when they cause a conflict.
2. I restarted instead of sliding = When you saw a duplicate, I threw away the whole substring. Sliding window should move the left edge forward, not reset everything.
3. I tracked the string, not the window = I was building a new string (result = result + s[i]). Sliding window tracks positions (left/right), not actual substrings.
4. I didn’t enforce the invariant = The rule was: window must contain unique characters. When the rule broke, I didn’t fix the window — I replaced it.


* 3rd attempt - SUCCEEDED
  (maitaining a window, while keeping the history intact about previously visited character -> it should never exceed count value = 1):

        alfabts = [0]*26
        result = 0
        lt = 0
        
        for i in range(len(s)):
            asci = ord(s[i]) - ord('a')
            alfabts[asci]  += 1
            
            while alfabts[asci]>1 and lt<i:
                check = ord(s[lt]) - ord('a')
                alfabts[check] -= 1
                lt += 1
            
            result = max(result, i-lt+1)
                
        return result

### Length of the longest substring (without repeating characters)
Problem statement: https://www.geeksforgeeks.org/problems/length-of-the-longest-substring3036/1
* Fundamental mistake with concept (not updating the asci array properly):

        alfabts = [0]*26
        result = s[0]
        # lt = 0
        for i in range(1, len(s)):
            asci = ord(s[i]) - 97
            if alfabts[asci] == 0:
                alfabts[asci] += 1
                result = result + s[i]
            else:
                # alfabts[asci] += 1
                result = s[i]
