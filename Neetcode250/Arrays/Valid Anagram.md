### Problem Statement (https://neetcode.io/problems/is-anagram/question):

Given two strings s and t, return true if the two strings are anagrams of each other, 
otherwise return false.

An anagram is a string that contains the exact same characters as another string, 
but the order of the characters can be different.

============================================================================

Invariant:
After processing the first k characters, 
the hashmap correctly stores the frequency difference (or frequency count) for all characters seen so far.

============================================================================

My wrong approach:

    class Solution:
      def isAnagram(self, s: str, t: str) -> bool:
        s_Map = {}
        t_Map = {}

        for c in s:
            if c not in s_Map:
                s_Map[c] = 1
            elif c in s_Map:
                s_Map[c] += 1

        for ch in t:
            if ch not in t_Map:
                t_Map[ch] = 1
            elif ch in t_Map:
                t_Map[ch] += 1

        for i in s_Map:
            if i in t_Map:
                if s_Map[i] != t_Map[i]:
                    return False

            elif i not in t_Map:
                return False

        return True

    - The problem here is it will calculate all the characters of s in t, but if t has any extra chracters:
      then it will fail

Correct Approach:

    class Solution:
      def isAnagram(self, s: str, t: str) -> bool:
        s_Map = {}
        t_Map = {}

        for c in s:
            if c not in s_Map:
                s_Map[c] = 1
            elif c in s_Map:
                s_Map[c] += 1

        for ch in t:
            if ch not in t_Map:
                t_Map[ch] = 1
            elif ch in t_Map:
                t_Map[ch] += 1

        return s_Map == t_Map
