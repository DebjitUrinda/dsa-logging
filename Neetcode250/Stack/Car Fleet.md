### Problem Statement (https://neetcode.io/problems/car-fleet/question?list=neetcode250)

There are n cars traveling to the same destination on a one-lane highway.

You are given two arrays of integers position and speed, both of length n.

position[i] is the position of the ith car (in miles)
speed[i] is the speed of the ith car (in miles per hour)
The destination is at position target miles.

A car can not pass another car ahead of it. It can only catch up to another car and then drive at the same speed as the car ahead of it.

A car fleet is a non-empty set of cars driving at the same position and same speed. A single car is also considered a car fleet.

If a car catches up to a car fleet the moment the fleet reaches the destination, then the car is considered to be part of the fleet.

Return the number of different car fleets that will arrive at the destination.

========================================================================

### INVARIANT
**My Invariant**:
After each iteration, maintain fleets as separate stacks and determine
which fleet a car belongs to.

_Problem:_Problem:
- This invariant does not constrain how fleet membership is determined.
A naive interpretation leads to checking multiple existing fleets for
each new car, which can degrade to O(n²).

**Correct Invariant:**
After processing each car, the stack contains the arrival times of all
fleets formed so far. The top of the stack represents the fleet
immediately ahead of the current car, which is the only fleet the car
can possibly join.

========================================================================

### SOLUTION
    class Solution:
      def carFleet(self, target: int, position: List[int], speed: List[int]) -> int:
        listOfCars = []

        for i in range(len(position)):
            tup = (position[i], speed[i])
            listOfCars.append(tup)

        listOfCars.sort(reverse=True)

        fleetStack = []

        for c in listOfCars:
            mark = (target - c[0]) / c[1]
            if not fleetStack:
                fleetStack.append(mark)
            else:
                # if mark != fleetStack[-1]:
                if mark > fleetStack[-1]:
                    fleetStack.append(mark)
        
        return len(fleetStack)
