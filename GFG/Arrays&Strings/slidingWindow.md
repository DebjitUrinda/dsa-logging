#### First Negative in Every Window (Baseline)

- Implemented brute-force solution (O(n*k))
- Focused on correctness and clarity
- Explicitly scans each window and stops at first negative

Why brute-force first:
- Clarifies window boundaries
- Removes ambiguity about "first"
- Acts as ground truth for optimized solutions

Known limitation:
- Recomputes overlapping window work
- Will TLE for large inputs

#### Planned changes:
- Replace repeated scanning with sliding window approach
- Maintain memory of negative elements across windows
- Remove negatives when they fall out of window
- Reduce time complexity from O(n*k) to O(n)
