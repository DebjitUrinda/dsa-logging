### Problem Statement (https://neetcode.io/problems/string-encode-and-decode/question):

Design an algorithm to encode a list of strings to a string. 
The encoded string is then sent over the network and is decoded back to the original list of strings.

Machine 1 (sender) has the function:
    
    string encode(vector<string> strs) {
      // ... your code
      return encoded_string;
    }

Machine 2 (receiver) has the function:

    vector<string> decode(string s) {
      //... your code
      return strs;
    }
So Machine 1 does:

    string encoded_string = encode(strs);
    and Machine 2 does:

    vector<string> strs2 = decode(encoded_string);
    strs2 in Machine 2 should be the same as strs in Machine 1.

Implement the encode and decode methods.

=======================================================================================

My Approach:

    class Solution:
      def encode(self, strs: List[str]) -> str:
        encoded = ""
        for s in strs:
            l = len(s)
            encoded = encoded + str(l) + "#" + s

        print(encoded)
        return encoded

      def decode(self, s: str) -> List[str]:
        strs = []
        size = ""
        while i < len(s):
            size = size + s[i]
            strs.append(s[i+1:size+1])
            i += size+1
            print(i)

        print(strs)
        return strs

The problem with this approach was:
There was no way to segregate strings of size with double digits, only single digit long strings could be decoded.

So the solution was to add a "#" after each length calculations:
  
    class Solution:
      def encode(self, strs: List[str]) -> str:
        encoded = ""
        for s in strs:
            l = len(s)
            encoded = encoded + str(l) + "#" + s
        return encoded

      def decode(self, s: str) -> List[str]:
        strs = []
        i=0
        while i < len(s):
            # find the delimiter '#'
            j = i
            while s[j] != '#':
                j += 1
            length = int(s[i:j])
            start = j + 1
            end = start + length
            strs.append(s[start:end])
            i = end  # move to the start of the next encoded part
        return strs
