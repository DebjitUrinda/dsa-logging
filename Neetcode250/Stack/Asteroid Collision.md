### Problem Statement (https://neetcode.io/problems/asteroid-collision/question?list=neetcode250):
You are given an array asteroids of integers representing asteroids in a row. The indices of the asteriod in the array represent their relative position in space.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

======================================================================================

### INVARIANT
**My Invaraint**:
After each iteration, the stack must only consist of non-exploded asteroids

**Correct Invariant:**
After processing each asteroid,
the stack contains exactly the surviving asteroids seen so far,
in order, with all collisions among them fully resolved.

======================================================================================

A collision can only happen when:
    
    stack[-1] > 0 and a < 0

### SOLUTION
    class Solution:
      def asteroidCollision(self, asteroids: List[int]) -> List[int]:
        stack = []

        for a in asteroids:
            alive = True

            while alive and stack and stack[-1] > 0 and a < 0:

                if abs(stack[-1]) < abs(a):
                    stack.pop()

                elif abs(stack[-1]) == abs(a):
                    stack.pop()
                    alive = False

                else:
                    alive = False

            if alive:
                stack.append(a)

        return stack
