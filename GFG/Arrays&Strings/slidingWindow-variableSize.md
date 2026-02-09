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


* 3rd attempt (maitaining a window, while keeping the history intact about previously visited character -> it should never exceed count value = 1):
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
