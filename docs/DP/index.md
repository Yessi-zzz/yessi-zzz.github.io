---
date: 2025-10-29
tags:
  - DP
---
### Properties
* A recursive solution that has repeated calls for the same inputs.
* The idea is to simply store the results of subproblems so that we do not have to re-compute them when needed later. This simple optimization typically reduces time complexities from exponential to polynomial.

### When to Use Dynamic Programming (DP)?
<!-- TODO(obsidian-blockref): 原文此处有块引用锚点 ^92e7f9，被 Steps to solve a DP Problem 用 [[Introduction to DP#^92e7f9]] 引用。跨页块引用待统一处理，暂以注释保留。 -->

1.  Optimal Substructure

    ???+ example "The minimum cost path"
        Consider the problem of finding the **minimum cost** path in a weighted graph from a **source** node to a **destination** node. We can break this problem down into smaller subproblems:

        - Find the **minimum** **cost** path from the **source** node to each **intermediate** node.
        - Find the **minimum** **cost** path from each **intermediate** node to the **destination** node.

        The solution to the larger problem (finding the minimum cost path from the source node to the destination node) can be constructed from the solutions to these smaller subproblems.

2.  Overlapping Subproblems

    The same subproblems are solved repeatedly in different parts of the problem refer to [Overlapping Subproblems Property in Dynamic Programming](https://www.geeksforgeeks.org/dsa/overlapping-subproblems-property-in-dynamic-programming-dp-1/).

    ???+ example "Fibonacci series"
        Consider the problem of computing the [**Fibonacci series**](https://www.geeksforgeeks.org/dsa/program-for-nth-fibonacci-number/). To compute the Fibonacci number at index *n*, we need to compute the Fibonacci numbers at indices *n-1* and *n-2*. This means that the subproblem of computing the Fibonacci number at index *n-2* is used twice (note that the call for *n - 1* will make two calls, one for *n-2* and other for *n-3*) in the solution to the larger problem of computing the Fibonacci number at index ***n***.
