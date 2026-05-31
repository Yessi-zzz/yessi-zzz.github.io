---
date: 2025-10-30
tags:
  - DP
  - tools
---
1. Identify if it is a Dynamic programming problem.
2. Decide a state expression with the Least parameters.
3. Formulate state and transition relationship.
4. Apply tabulation or memorization.

### Step 1: How to classify a problem as a Dynamic Programming Problem? (见 Introduction to DP)

- Typically, all the problems that require **maximizing or minimizing** certain quantities or counting problems that say to count the arrangements under certain conditions or certain probability problems can be solved by using Dynamic Programming.
- **All** dynamic programming problems satisfy the *overlapping subproblems* property and **most of the classic** Dynamic programming problems also satisfy the *optimal substructure* property. Once we observe these properties in a given problem be sure that it can be solved using Dynamic Programming.

### Step 2: Deciding the state

!!! important
    Dynamic Programming problems are all about the ***state*** and its ***transition***.

#### state: 
A state can be defined as the set of **parameters** that can uniquely identify a certain position or standing in the given problem. This set of parameters should be as small as possible to reduce state space.

#### Example: Knapsack Problem
Here, we define our state using two parameters: 
*index* and *weight* (dp[index][weight]). These two parameters work together to uniquely identify each subproblem we need to solve.

### Step 3: Formulating a relation among the states

The Hardest Part:
require a lot of intuition, observation, and practice
#### Example:
Given 3 numbers {1, 3, 5}, The task is to tell the total number of ways we can form a number *n* using the *sum* of the given three numbers. (allowing repetitions and different arrangements).
>The total number of ways to form 6 is: 8  
1 + 1 + 1 + 1 + 1 + 1  
1 + 1 + 1 + 3  
1 + 1 + 3 + 1  
1 + 3 + 1 + 1  
3 + 1 + 1 + 1  
3 + 3  
1 + 5  
5 + 1


The steps to solve the given problem will be:
- Decide a state for the given problem. 
- Take a parameter *n* to decide the state as it uniquely identifies any subproblem. 
- DP state will look like ***state(n)***; ***state(n)*** means the total number of arrangements to form *n* by using {1, 3, 5} as elements. Derive a transition relation between any two states.
- Now, compute state(n).

#### **How to Compute the state?**

Assume that the result for n = 1, 2, 3, 4, 5, 6
Let us say we know the result for:  
state (n = 1), state (n = 2), state (n = 3) ......... state (n = 6)   
Now, we wish to know the result of the state (n = 7). we can only add 1, 3, and 5. Now we can get a sum total of 7 in the following 3 ways:
???+ important "Analysis"
    1) Adding 1 to all possible combinations of *state (n = 6)*
    Eg : [(1 + 1 + 1 + 1 + 1 + 1) + 1]   
    [(1 + 1 + 1 + 3) + 1]   
    [(1 + 1 + 3 + 1) + 1]   
    [(1 + 3 + 1 + 1) + 1]   
    [(3 + 1 + 1 + 1) + 1]   
    [(3 + 3) + 1]   
    [(1 + 5) + 1]   
    [(5 + 1) + 1] 

    2) Adding 3 to all possible combinations of *state (n = 4)*
    [(1 + 1 + 1 + 1) + 3]   
    [(1 + 3) + 3]   
    [(3 + 1) + 3] 

    3) Adding 5 to all possible combinations of *state(n = 2)*
    [(1 + 1) + 5]

    __(Note how it sufficient to add only on the right-side - all the add-from-left-side cases are covered, either in the same state, or another, e.g. [1 + (1 + 1 + 1 + 3)]  is not needed in state (n=6) because it's covered by state (n = 4) [(1 + 1 + 1 + 1) + 3])__

    Therefore, we can say that result for   
    state(7) = state (6) + state (4) + state (2)   
    OR  
    state(7) = state (7-1) + state (7-3) + state (7-5)  
    In general,   
    ***state(n) = state(n-1) + state(n-3) + state(n-5)***

```python
# Python program to express
# n as sum of 1, 3, 5.

# Returns the number of 
# arrangements to form 'n' 
def countWays(n):
    
    # base case
    if n < 0:
        return 0
    if n == 0:
        return 1

    return countWays(n - 1) + countWays(n - 3) + countWays(n - 5)

if __name__ == "__main__":
    n = 7
    print(countWays(n))
```
output:
`12`
**Time Complexity:** O(3^n), As at every stage we need to take three decisions and the height of the tree will be of the order of n.  
**Auxiliary Space:** O(n), The extra space is used due to the recursion call stack.

The above code seems exponential as it is calculating the same state again and again. So, we just need to add **memoization**.
### Step 4: Adding memoization or tabulation for the state

The easiest part of a dynamic programming solution: just need to store the state answer so that the next time that state is required, then directly use it from memory.

#### Using Top-Down DP (Memoization)

Break down the problem into smaller subproblems, where each subproblem corresponds to finding the number of ways to form a sum for a smaller value of 'n'. By utilizing previously computed results, we can avoid redundant calculations and build up the solution for larger values of 'n'.
```python
# Python program to express
# n as sum of 1, 3, 5.

def countRecur(n, memo):
    
    # base case
    if n < 0:
        return 0
    if n == 0:
        return 1

    # If value is memoized
    if memo[n] != -1:
        return memo[n]

    # Memoize the state 
    memo[n] = countRecur(n - 1, memo) + \
              countRecur(n - 3, memo) + \
              countRecur(n - 5, memo)
    
    return memo[n]

# Returns the number of 
# arrangements to form 'n' 
def countWays(n):
    memo = [-1] * (n + 1)
    return countRecur(n, memo)

if __name__ == "__main__":
    n = 7
    print(countWays(n))
```
output:
`12`
**Time Complexity:** O(n), As at every stage we need to take three decisions and the height of the tree will be of the order of n.  
**Auxiliary Space:** O(n + n), The extra space is used due to the recursion call stack and memo array of size n+1 is used to store the results of subproblems.

#### Using Bottom-Up DP (Tabulation)

Define a DP array where each element dp[i] represents the number of ways to form the sum 'i'. Starting with the base case dp[0] = 1 (since there is exactly one way to form a sum of 0 - using no numbers), we iteratively calculate the number of ways to form each value from 1 to n.
```python
# Python program to express
# n as sum of 1, 3, 5.

# Returns the number of 
# arrangements to form 'n' 
def countWays(n):
    dp = [0] * (n + 1)
    dp[0] = 1

    for i in range(1, n + 1):
        dp[i] = 0

        if i - 1 >= 0:
            dp[i] += dp[i - 1]
        if i - 3 >= 0:
            dp[i] += dp[i - 3]
        if i - 5 >= 0:
            dp[i] += dp[i - 5]

    return dp[n]

if __name__ == "__main__":
    n = 7
    print(countWays(n))
```
output:
`12`
**Time Complexity:** O(n), As we just need to make 3n function calls and there will be no repetitive calculations as we are returning previously calculated results.  
**Auxiliary Space:** O(n), dp array of size n+1 is used to store the results of subproblems.