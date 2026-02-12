## What is a Prefix Sum?
* Take an array: nums = [2, 4, 1, 3]
* Prefix sum just means: At every position, store the total from the start up to that position. That’s it.
* So prefix array becomes: prefix = [2, 6, 7, 10]
* Why do we make this? -> Because now we can get any subarray sum instantly. Instead of adding again and again.
* Example
Find sum of elements from index 1 to 3.
Original array:
[2, 4, 1, 3]
   ↑     ↑
That means:
4 + 1 + 3 = 8
Now look at prefix:
[2, 6, 7, 10]
