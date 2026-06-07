### Problem Statement(https://neetcode.io/problems/online-stock-span/question?list=neetcode250):
Design an algorithm that collects daily price quotes for some stock and returns the span of that stock's price for the current day.

The span of the stock's price in one day is the maximum number of consecutive days (starting from that day and going backward) for which the stock price was less than or equal to the price of that day.

For example, if the prices of the stock in the last four days is [7,2,1,2] and the price of the stock today is 2, then the span of today is 4 because starting from today, the price of the stock was less than or equal 2 for 4 consecutive days.
Also, if the prices of the stock in the last four days is [7,34,1,2] and the price of the stock today is 8, then the span of today is 3 because starting from today, the price of the stock was less than or equal 8 for 3 consecutive days.
Implement the StockSpanner class:

StockSpanner() Initializes the object of the class.
int next(int price) Returns the span of the stock's price given that today's price is price.

==============================================================================

### INVARIANTS
**My Invariant**:
After each iteration, the stack should represent the unprocessed stock price in order of the input array. By unprocessed stock price we mean we couldn't find any stock price greater than or equal to that TOS stock price. And for calculation we check the TOS and compare the last processed element to compute the result

**Better Invariant (is to store the price and span in pairs)**:
After processing each price:
The stack contains pairs (price, span).
Prices in the stack are strictly decreasing from bottom to top.
For each pair (p, s), s represents the span of p.

==============================================================================

### SOLUTION
    class StockSpanner:

      def __init__(self):
        self.stack = []

      def next(self, price: int) -> int:
        if not self.stack:
            span = 1
            self.stack.append((price, span))

        else:
            tos = self.stack[-1]
            span = 1

            if price<tos[0]:
                self.stack.append((price, span))
                return span

            else:
                while self.stack and price>=tos[0]:
                    days = self.stack.pop()
                    span += days[1]
                    if self.stack:
                        tos = self.stack[-1]

            self.stack.append((price, span))

        return self.stack[-1][1]
