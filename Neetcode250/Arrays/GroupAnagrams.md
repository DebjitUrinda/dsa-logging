Problem statement: (https://neetcode.io/problems/anagram-groups/question?list=neetcode250)
Given an array of strings strs, group all anagrams together into sublists. You may return the output in any order.
An anagram is a string that contains the exact same characters as another string, but the order of the characters can be different.

This is basically a key creation and hashmap generation problem, where it is asking whether we can create a key for every word in the list and map it to the hashmap.
Two ways to create keys: 1. create a frquency counter array, 2. use sorted() to sort the letter of each word which becomes the key.

This pattern shows up everywhere:
Grouping problems,
Hashing tricks,
Frequency counting,
Data normalization
