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
