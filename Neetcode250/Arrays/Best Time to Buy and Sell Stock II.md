### Problem Statement (https://neetcode.io/problems/best-time-to-buy-and-sell-stock-ii/question?list=neetcode250):
You are given an integer array prices where prices[i] is the price of a given stock on the ith day.

On each day, you may decide to buy and/or sell the stock. 
However, you can buy it then immediately sell it on the same day. 
Also, you are allowed to perform any number of transactions but can hold 
at most one share of the stock at any time.

Find and return the maximum profit you can achieve.

=====================================================================

Greeedy Solution:

    class Solution:
      def maxProfit(self, prices: List[int]) -> int:
        profit = 0
        for i in range(len(prices)-1):
            if prices[i+1] > prices[i]:
                profit += prices[i+1] - prices[i]

        return profit
