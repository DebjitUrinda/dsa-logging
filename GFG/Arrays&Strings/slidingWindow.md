### First Negative in Every Window (Baseline)

- Implemented brute-force solution (O(n*k))
- Focused on correctness and clarity
- Explicitly scans each window and stops at first negative
- 
Why brute-force first:
- Clarifies window boundaries
- Removes ambiguity about "first"
- Acts as ground truth for optimized solutions
#### Brute Force 
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
