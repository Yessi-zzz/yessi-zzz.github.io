---
date: 2025-11-04
tags:
  - DP
  - cods
  - problems
---
> **Recurrence relation:**
> 
> - **Base case:** F(n) = n, when n = 0 or n = 1
> - **Recursive case:** F(n) = F(n-1) + F(n-2) for n>1

```python
def nth_fibonacci(n):
  
    # Base case: if n is 0 or 1, return n
    if n <= 1:
        return n
      
    # Recursive case: sum of the two preceding Fibonacci numbers
    return nth_fibonacci(n - 1) + nth_fibonacci(n - 2)

n = 5
result = nth_fibonacci(n)
print(result)
```
output:
`5`
**Time Complexity:** O(2n)  
**Auxiliary Space:** O(n), due to recursion stack

### Memoization Approach
```python
# Function to calculate the nth Fibonacci number using memoization
def nth_fibonacci_util(n, memo):

    # Base case: if n is 0 or 1, return n
    if n <= 1:
        return n

    # Check if the result is already in the memo table
    if memo[n] != -1:
        return memo[n]

    # Recursive case: calculate Fibonacci number
    # and store it in memo
    memo[n] = nth_fibonacci_util(n - 1, memo) + nth_fibonacci_util(n - 2, memo)

    return memo[n]


# Wrapper function that handles both initialization
# and Fibonacci calculation
def nth_fibonacci(n):

    # Create a memoization table and initialize with -1
    memo = [-1] * (n + 1)

    # Call the utility function
    return nth_fibonacci_util(n, memo)


if __name__ == "__main__":
    n = 5
    result = nth_fibonacci(n)
    print(result)
```
output:
`5`
**Time Complexity:** O(n), each fibonacci number is calculated only one times from 1 to n;  
**Auxiliary Space:** O(n), due to memo table

### Bottom-Up Approach
```python
def nth_fibonacci(n):
  
    # Handle the edge cases
    if n <= 1:
        return n

    # Create a list to store Fibonacci numbers
    dp = [0] * (n + 1)

    # Initialize the first two Fibonacci numbers
    dp[0] = 0
    dp[1] = 1

    # Fill the list iteratively
    for i in range(2, n + 1):
        dp[i] = dp[i - 1] + dp[i - 2]

    # Return the nth Fibonacci number
    return dp[n]

n = 5
result = nth_fibonacci(n)
print(result)
```
output:
`5`
**Time Complexity:** O(n), the loop runs from 2 to n, performing a constant amount of work per iteration.  
**Auxiliary Space:** O(n), due to the use of an extra array to store Fibonacci numbers up to n.

### Space Optimized Approach
```python
def nth_fibonacci(n):
    if n <= 1:
        return n

    # To store the curr Fibonacci number
    curr = 0

    # To store the previous Fibonacci numbers
    prev1 = 1
    prev2 = 0

    # Loop to calculate Fibonacci numbers from 2 to n
    for i in range(2, n + 1):
      
        # Calculate the curr Fibonacci number
        curr = prev1 + prev2

        # Update prev2 to the last Fibonacci number
        prev2 = prev1

        # Update prev1 to the curr Fibonacci number
        prev1 = curr

    return curr

n = 5
result = nth_fibonacci(n)
print(result)
```
output:
`5`
**Time Complexity:** O(n), The loop runs from 2 to n, performing constant time operations in each iteration.)  
**Auxiliary Space:** O(1), Only a constant amount of extra space is used to store the current and two previous Fibonacci numbers.

### Using Matrix Exponentiation - O(log(n)) time and O(log(n)) space
```python
# Function to multiply two 2x2 matrices
def multiply(mat1, mat2):
  
    # Perform matrix multiplication
    x = mat1[0][0] * mat2[0][0] + mat1[0][1] * mat2[1][0]
    y = mat1[0][0] * mat2[0][1] + mat1[0][1] * mat2[1][1]
    z = mat1[1][0] * mat2[0][0] + mat1[1][1] * mat2[1][0]
    w = mat1[1][0] * mat2[0][1] + mat1[1][1] * mat2[1][1]

    # Update matrix mat1 with the result
    mat1[0][0], mat1[0][1] = x, y
    mat1[1][0], mat1[1][1] = z, w

# Function to perform matrix exponentiation
def matrix_power(mat1, n):
  
    # Base case for recursion
    if n == 0 or n == 1:
        return

    # Initialize a helper matrix
    mat2 = [[1, 1], [1, 0]]

    # Recursively calculate mat1^(n // 2)
    matrix_power(mat1, n // 2)

    # Square the matrix mat1
    multiply(mat1, mat1)

    # If n is odd, multiply by the helper matrix mat2
    if n % 2 != 0:
        multiply(mat1, mat2)

# Function to calculate the nth Fibonacci number
def nth_fibonacci(n):
    if n <= 1:
        return n

    # Initialize the transformation matrix
    mat1 = [[1, 1], [1, 0]]

    # Raise the matrix mat1 to the power of (n - 1)
    matrix_power(mat1, n - 1)

    # The result is in the top-left cell of the matrix
    return mat1[0][0]

if __name__ == "__main__":
    n = 5
    result = nth_fibonacci(n)
    print(result)
```

