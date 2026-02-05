### Longest Subarray with Sum K (positive)
* Mistake: 
  Apparently Sliding window only works for positive numbers, now the question is why did I not think of this question that I am working with an unsolvable method. The GFG problem I was working on (https://www.geeksforgeeks.org/problems/longest-sub-array-with-sum-k0809/1) includes negative number and ther only hashmap and indexing would work.

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
