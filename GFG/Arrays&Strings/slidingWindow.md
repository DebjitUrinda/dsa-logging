### 1. First Negative in Every Window 

(Baseline)
- Implemented brute-force solution (O(n*k))
- Focused on correctness and clarity
- Explicitly scans each window and stops at first negative
- 
Why brute-force first:
- Clarifies window boundaries
- Removes ambiguity about "first"
- Acts as ground truth for optimized solutions
### Brute Force 
        negArr = []
        
        for i in range(0, len(arr)-k+1):
            negFlag = True
            for j in range(i, i+k):
                if arr[j]<0:
                    negArr.append(arr[j])
                    negFlag = False
                    break
            
            if negFlag:
                negArr.append(0)
                
        return negArr
Known limitation:
- Recomputes overlapping window work
- Will TLE for large inputs

#### Planned changes:
- Replace repeated scanning with sliding window approach
- Maintain memory of negative elements across windows
- Remove negatives when they fall out of window
- Reduce time complexity from O(n*k) to O(n)


### Sliding Window Logic
For window starting at i:
- window_end = i + k - 1

Expire old negatives
 while p < len(negIdx) and negIdx[p] < i:
    p += 1

Decide answer
 if p < len(negIdx) and negIdx[p] <= window_end:
    result.append(arr[negIdx[p]])
 else:
    result.append(0)

Invariant
 p always points to the first negative index inside the current window.

Complexity
Time: O(n)
Space: O(n)

Lesson
Sliding window optimization works by remembering candidates and discarding them only when they exit the window.


### 2. Count Occurrences of Anagrams

##### Problem Statement (https://www.geeksforgeeks.org/problems/count-occurences-of-anagrams5839/1)
Given a string txt and a pattern string pat, count how many substrings of txt are anagrams of pat.

An anagram means:
Same characters
Same frequency
Order does not matter

##### Core Idea
This problem is solved using the Sliding Window technique with fixed window size.
Key observations:
Only contiguous substrings are considered
Anagram checking depends on character frequency, not order
The window size is always len(pat)
Instead of recomputing frequencies for every substring, we:
Build frequency data once
Slide the window
Update only the characters that enter and leave the window

##### Why No Dictionary?
The constraints specify:
Only lowercase English letters
So we use:
A fixed-size array of length 26
Each index represents a character (a → z)
This gives:
Faster access than dictionaries
Constant space complexity

##### Algorithm Steps
1. Edge Case Check
If len(pat) > len(txt), return 0
2. Initialize
patCount[26] → frequency of characters in pat
windowCount[26] → frequency of characters in current window
3. Build First Window
Populate windowCount using the first k = len(pat) characters
4. Compare First Window
If windowCount == patCount, increment result
5. Slide the Window
Remove the leftmost character
Add the next character on the right
Compare again
6. Repeat until the end of txt
