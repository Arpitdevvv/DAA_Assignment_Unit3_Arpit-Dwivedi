# DAA_Assignment_Unit3_Arpit-Dwivedi

**Student:** Arpit Dwivedi  
**Course:** Design and Analysis of Algorithms  
**Assignment:** Unit 3  

- Sections included: A (Short Theory) and B (Algorithms & Recurrences)
## SECTION A – Short Theory

### 1. Dynamic Programming Essentials
Dynamic Programming (DP) uses three core ideas:

- **Optimal Substructure:** The optimal solution to a problem can be constructed from optimal solutions of its subproblems.  
- **Overlapping Subproblems:** The same subproblems occur multiple times; computing them once and reusing results saves time.  
- **Memoization / Tabulation:** Store results — top-down (memoization) or bottom-up (tabulation) — to avoid redundant work.

---

**DP vs Divide and Conquer**

**Overlapping Subproblems**: Dynamic Programming is used for problems where the same subproblems appear repeatedly and can be reused, while Divide and Conquer solves distinct subproblems that don’t overlap.

**Result Reuse**: DP stores computed results to prevent redundant work, whereas Divide and Conquer recalculates results every time.
**Examples**:
Dynamic Programming: 0/1 Knapsack, Matrix Chain Multiplication.
Divide and Conquer: Binary Search, Strassen’s Matrix Multiplication

---

### 3. Principle of Optimality
A problem satisfies the Principle of Optimality if an optimal solution of the given problem contains optimal solutions to its possible subproblems.  
**Example:** Shortest-path problems — each subpath of an optimal path is optimal.
like **Floyd–Warshall Algorithm** (All-Pairs Shortest Path):
The shortest path between any two vertices i and j through an intermediate vertex k relies on the optimal shortest paths i → k and k → j.

---

### 4. Memoization
- **Memoization:** Top-down dynamic programming recursion approach where the recursive results are stored in the form of cache and reused when needed or in other words it is computed recursively and results are stored in a map/array when first computed.  
- **Tabulation:** It is a bottom-up approach in Dynamic Programming where we start from the base cases and iteratively fill a table or array to build the final solution.
Instead of using recursion, it computes all smaller subproblems first and then uses their results to solve larger ones efficiently.
---

### 5. Branch and Bound — Core Idea
Branch and Bound explores a decision tree where each node represents a partial solution.  
A **bound** (upper or lower) estimates the best achievable solution below that node. If the bound cannot beat the current best solution, the branch is pruned. This drastically reduces search.

## SECTION B – Algorithms & Recurrences

**6. Matrix Chain Multiplication**  
Given matrices A₁(5×4), A₂(4×6), A₃(6×2), A₄(2×7), we want the minimum number of scalar multiplications.

**Recurrence:**  
```
m[i, j] = 0, if i = j  
m[i, j] = min_{k=i to j-1} (m[i, k] + m[k+1, j] + p_{i-1} * p_k * p_j)
```
Here, `p` represents matrix dimensions.  
**Base Case:** A single matrix needs zero multiplications.  
**Minimum scalar multiplications:** 158

---

**7. Longest Common Subsequence (X = "ABCDGH", Y = "AEDFHR")**  

**Recurrence:**  
```
LCS(i, j) = 0, if i = 0 or j = 0  
LCS(i, j) = 1 + LCS(i-1, j-1), if X[i] = Y[j]  
LCS(i, j) = max(LCS(i-1, j), LCS(i, j-1)), otherwise
```
This formula finds the longest subsequence common to both strings without changing their order.  
**Base Case:** If either string is empty, LCS = 0.  
**LCS length:** 3 (common subsequence “ADH”).

---

**8. Optimal Binary Search Tree**  
Keys: {10, 20, 30}, probabilities p = {0.4, 0.3, 0.3}, q = 0.  
The goal is to minimize the expected search cost.

**Formulations:**  
```
w[i, j] = w[i, j-1] + p[j]  
e[i, j] = min_{r=i to j} (e[i, r-1] + e[r+1, j] + w[i, j])
```
**Base Case:**  
e[i, i-1] = 0, w[i, i-1] = 0  
**Minimum expected search cost:** 1.7 (root at key 10 or 20 yields optimal arrangement).

---

**9. 0/1 Knapsack – Branch & Bound**  
Given: W = 5; weights = {2, 3, 4, 5}; profits = {3, 4, 5, 6}.  
The objective is to maximize profit without exceeding capacity.

**Fractional Upper Bound Formula:**  
```
UB = current_profit + (remaining_capacity * next_item_profit / next_item_weight)
```
This upper bound helps in pruning non-promising nodes.  

**Nodes:**  
Level 0 (root) → (v=0, w=0, ub=10.5)  
Level 1 include item1 → (v=3, w=2, ub=9.33)  
Level 1 exclude item1 → (v=0, w=0, ub=9.0)  
The branch with higher bound is explored further.

---

**10. Travelling Salesman Problem – Dynamic Programming (Held–Karp)**  

**Recurrence:**  
```
C[S, j] = min_{k ∈ S, k ≠ j} [C[S - {j}, k] + D[k][j]]
Final answer = min_{j ≠ 1} [C[{2,3,4}, j] + D[j][1]]
```
Here, S represents the set of visited cities and D is the distance matrix.  
**Base Initialization:**  
C[{2},2] = D[1][2]  
C[{3},3] = D[1][3]  
C[{4},4] = D[1][4]  
This DP approach computes all subsets to find the minimum Hamiltonian cycle cost.
