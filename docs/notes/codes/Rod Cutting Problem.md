---
date: 2025-10-30
tags:
  - DP
  - codes
  - problems
---
Given a rod of length ***n inches*** and an array *price[]*. *price[i]* denotes the value of a *piece* of length i. The task is to determine the **maximum** value obtainable by **cutting up the rod** and selling the pieces.

???+ example "例1"
    **Input:** price[] = [1, 5, 8, 9, 10, 17, 17, 20]
    **Output:** 22
    **Explanation**: The maximum obtainable value is 22 by cutting in two pieces of lengths 2 and 6, i.e., 5 + 17 = 22.

???+ example "例2"
    **Input :** price[] = [3, 5, 8, 9, 10, 17, 17, 20]
    **Output** : 24
    **Explanation :** The maximum obtainable value is 24 by cutting the rod into 8 pieces of length 1, i.e, 8 * price[1]= 8 * 3 = 24.

In the **rod cutting problem**, the goal is to determine the **maximum profit** that can be obtained by **cutting** a rod into smaller pieces and selling them, given a price list for each possible piece length. The approach involves considering all possible cuts for the rod and **recursively** calculating the maximum profit for each cut. For detailed explanation and approaches, refer to [Rod Cutting](https://www.geeksforgeeks.org/dsa/cutting-a-rod-dp-13/).

### Using Top-Down DP (Memoization) - *** O(n^2)*** ***Time and*** ***O(n) Space***

In this implementation of the **rod cutting problem**,**memoization** is used to optimize the recursive approach by storing the results of subproblems, avoiding redundant calculations.

```python
# Python program to find maximum
# profit from rod of size n 
def cutRodRecur(i, price, memo):
    
    # Base case
    if i == 0:
        return 0
    
    # If value is memoized
    if memo[i - 1] != -1:
        return memo[i - 1]
    
    ans = 0

    # Find maximum value for each cut.
    # Take value of rod of length j, and 
    # recursively find value of rod of 
    # length (i-j).
    for j in range(1, i + 1):
        ans = max(ans, price[j - 1] + cutRodRecur(i - j, price, memo))

    memo[i - 1] = ans
    return ans

def cutRod(price):
    n = len(price)
    memo = [-1] * n
    return cutRodRecur(n, price, memo)

if __name__ == "__main__":
    price = [1, 5, 8, 9, 10, 17, 17, 20]
    print(cutRod(price))
```
output:
`22`

### Using Bottom-Up DP (Tabulation) - ***O(n^2)*** Time and ***O(n)*** Space

We **iteratively** calculate the maximum profit for each possible rod length. For each length `i`, we check all possible smaller cuts, update the profit by comparing the current maximum profit with the profit obtained by combining smaller cuts, and ultimately return the maximum profit for the entire rod.

```python
# Python program to find maximum
# profit from rod of size n 

def cutRod(price):
    n = len(price)
    dp = [0] * (n + 1)

    # Find maximum value for all 
    # rod of length i.
    for i in range(1, n + 1):
        for j in range(1, i + 1):
            dp[i] = max(dp[i], price[j - 1] + dp[i - j])

    return dp[n]

if __name__ == "__main__":
    price = [1, 5, 8, 9, 10, 17, 17, 20]
    print(cutRod(price))
```
output:
`22`
