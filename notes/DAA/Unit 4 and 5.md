← [[DAA]] Home

Okay, let's break down this syllabus into comprehensive study material, following your requested structure for each topic.

---

**Unit IV – Dynamic Programming and Greedy Techniques**

**Introduction to Dynamic Programming (DP)**

*   **Concept:** Dynamic Programming is an algorithmic technique for solving complex problems by breaking them down into simpler, overlapping subproblems. It solves each subproblem only once and stores its result (memorization or tabulation) to avoid redundant computations. Key characteristics are **Optimal Substructure** (an optimal solution to the problem contains optimal solutions to its subproblems) and **Overlapping Subproblems** (the same subproblems are encountered multiple times during recursion).
*   **Analogy:** Imagine calculating Fibonacci numbers recursively (fib(n) = fib(n-1) + fib(n-2)). You'd recalculate fib(2), fib(3) etc., many times. DP is like writing down the result for fib(2) the first time you calculate it, and then just looking it up whenever you need it again, saving immense time.
*   **Use-Cases:** Optimization problems (finding min/max values), sequence alignment (bioinformatics), pathfinding, resource allocation, scheduling.

---

## 1. Computing a Binomial Coefficient (C(n, k))

### 1. Concept Explanation

*   **What:** The binomial coefficient C(n, k), often read as "n choose k", represents the number of ways to choose k items from a set of n distinct items without regard to the order of selection.
*   **Why DP:** The naive recursive formula C(n, k) = C(n-1, k-1) + C(n-1, k) involves recalculating the same subproblems multiple times. DP provides an efficient way using a table (Pascal's Triangle).
*   **How:** We can build a 2D table `dp[n+1][k+1]` where `dp[i][j]` stores the value of C(i, j). We fill the table using the recurrence relation, relying on previously computed values.
*   **Base Cases:** C(n, 0) = 1, C(n, n) = 1. Also, C(n, k) = 0 if k > n.

### 2. Real-World Analogies and Use-Cases

*   **Analogy:** How many ways can you form a committee of 3 people (k=3) from a group of 10 people (n=10)? This is C(10, 3).
*   **Use-Cases:** Probability calculations (binomial distribution), combinatorics, polynomial expansions ((a+b)^n), statistical mechanics.

### 3. Step-by-Step Solved Example

**Problem:** Calculate C(4, 2).

**DP Table Approach (Tabulation):**
Create a table `dp[5][3]` (indices up to n=4 and k=2).

*   **Initialization (Base Cases):**
    *   `dp[i][0] = 1` for all i (C(i, 0) = 1) -> `dp[0][0]=1, dp[1][0]=1, dp[2][0]=1, dp[3][0]=1, dp[4][0]=1`
    *   `dp[i][i] = 1` (where applicable) -> `dp[1][1]=1, dp[2][2]=1` (we only need up to k=2)
    *   `dp[i][j] = 0` if j > i

*   **Filling the table using `dp[i][j] = dp[i-1][j-1] + dp[i-1][j]`:**
    *   `dp[2][1] = dp[1][0] + dp[1][1] = 1 + 1 = 2`
    *   `dp[3][1] = dp[2][0] + dp[2][1] = 1 + 2 = 3`
    *   `dp[3][2] = dp[2][1] + dp[2][2] = 2 + 1 = 3`
    *   `dp[4][1] = dp[3][0] + dp[3][1] = 1 + 3 = 4`
    *   `dp[4][2] = dp[3][1] + dp[3][2] = 3 + 3 = 6`

**Result:** `dp[4][2] = 6`.

### 4. Pseudocode and Code Implementation

**Pseudocode (DP Tabulation):**

```pseudocode
function BinomialCoefficient(n, k):
  // Create a DP table C[0..n][0..k]
  C = new array[n+1][k+1]

  // Fill the table in bottom-up manner
  for i from 0 to n:
    for j from 0 to min(i, k):
      // Base Cases
      if j == 0 or j == i:
        C[i][j] = 1
      // Recurrence Relation
      else:
        C[i][j] = C[i-1][j-1] + C[i-1][j]

  return C[n][k]
```

**Python Implementation:**

```python
def binomial_coefficient(n, k):
    """Computes C(n, k) using dynamic programming."""
    if k < 0 or k > n:
        return 0
    if k == 0 or k == n:
        return 1
    # Optimize: C(n, k) == C(n, n-k)
    if k > n // 2:
        k = n - k

    # DP table (or use space optimization)
    dp = [[0] * (k + 1) for _ in range(n + 1)]

    for i in range(n + 1):
        for j in range(min(i, k) + 1):
            if j == 0 or j == i:
                dp[i][j] = 1
            else:
                # Ensure indices are valid before accessing
                if i > 0 and j > 0:
                     dp[i][j] = dp[i-1][j-1] + dp[i-1][j]

    return dp[n][k]

# Example usage
n_val = 4
k_val = 2
print(f"C({n_val}, {k_val}) = {binomial_coefficient(n_val, k_val)}") # Output: C(4, 2) = 6
```

**C++ Implementation:**

```c++
#include <vector>
#include <iostream>
#include <algorithm> // For std::min

long long binomial_coefficient(int n, int k) {
    if (k < 0 || k > n) {
        return 0;
    }
    if (k == 0 || k == n) {
        return 1;
    }
    // Optimize: C(n, k) == C(n, n-k)
    if (k > n / 2) {
        k = n - k;
    }

    // DP table
    std::vector<std::vector<long long>> dp(n + 1, std::vector<long long>(k + 1, 0));

    for (int i = 0; i <= n; ++i) {
        for (int j = 0; j <= std::min(i, k); ++j) {
            if (j == 0 || j == i) {
                dp[i][j] = 1;
            } else {
                 // Ensure indices are valid (though loop bounds should handle this)
                 if (i > 0 && j > 0) {
                    dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j];
                 }
            }
        }
    }
    return dp[n][k];
}

int main() {
    int n_val = 4;
    int k_val = 2;
    std::cout << "C(" << n_val << ", " << k_val << ") = "
              << binomial_coefficient(n_val, k_val) << std::endl; // Output: C(4, 2) = 6
    return 0;
}
```

*(Space Optimization Note: Since calculating row `i` only depends on row `i-1`, you can optimize space complexity to O(k) by using only two rows or even a single row.)*

### 5. Diagrams or Flowcharts

**DP Table for C(4, 2):**

```
  k=0  k=1  k=2
n=0 [ 1 ] [ - ] [ - ]
n=1 [ 1 ] [ 1 ] [ - ]
n=2 [ 1 ] [ 2 ] [ 1 ]
n=3 [ 1 ] [ 3 ] [ 3 ]
n=4 [ 1 ] [ 4 ] [ 6 ]  <- Result
```
Arrows showing dependencies: `dp[i][j]` depends on `dp[i-1][j-1]` (diagonal up-left) and `dp[i-1][j]` (directly above).

### 6. Key Formulas and Logic Summary

*   **Recurrence:** C(n, k) = C(n-1, k-1) + C(n-1, k)
*   **Base Cases:** C(n, 0) = 1, C(n, n) = 1
*   **Logic:** Build a table storing C(i, j) values, filling it row by row or column by column using the recurrence.
*   **Time Complexity:** O(n * k)
*   **Space Complexity:** O(n * k) (Can be optimized to O(k))

### 7. Common Mistakes and Edge Cases

*   **Off-by-one errors:** Incorrect loop bounds or table indexing.
*   **Base cases:** Forgetting or incorrectly implementing base cases (j=0 or j=i).
*   **k > n:** Should return 0. The code handles this.
*   **Integer Overflow:** For large n and k, the result can exceed standard integer limits. Use `long long` in C++ or Python's arbitrary-precision integers.
*   **Space Optimization:** Implementing space optimization correctly requires careful index handling.

### 8. MCQ/Short Questions and Answers

1.  **Q:** What does C(n, k) represent?
    **A:** The number of ways to choose k items from a set of n distinct items.
2.  **Q:** What are the two key properties that suggest a problem might be solvable with Dynamic Programming?
    **A:** Optimal Substructure and Overlapping Subproblems.
3.  **Q:** What is the time complexity of the DP algorithm for C(n, k)?
    **A:** O(n * k).
4.  **Q:** What is the value of C(5, 0)?
    **A:** 1.
5.  **Q:** How can the space complexity for computing C(n, k) be optimized?
    **A:** By realizing that computing row `i` only requires row `i-1`, reducing space to O(k).

---

## 2. Warshall's Algorithm

### 1. Concept Explanation

*   **What:** Warshall's algorithm computes the **transitive closure** of a directed graph. The transitive closure T of a graph G is a graph such that there is an edge from vertex i to vertex j in T if and only if there is a path (of length 1 or more) from i to j in G.
*   **Why DP:** It uses a DP-like approach. It determines reachability between nodes `i` and `j` by considering whether they can reach each other *via* intermediate nodes `k`.
*   **How:** It uses an adjacency matrix `R` (initially the graph's adjacency matrix, or a boolean matrix indicating direct edges). It iterates through all possible intermediate vertices `k`. For every pair of vertices `(i, j)`, it checks if there's a path from `i` to `k` AND a path from `k` to `j`. If so, it means there's a path from `i` to `j` (possibly through `k`), and it updates `R[i][j]` to true (or 1).
*   **Logic:** `R^(k)[i][j] = R^(k-1)[i][j] OR (R^(k-1)[i][k] AND R^(k-1)[k][j])`. This means a path exists from `i` to `j` using only intermediate vertices from `{1, ..., k}` if either a path existed using only `{1, ..., k-1}` OR there's a path from `i` to `k` and `k` to `j` using only `{1, ..., k-1}`.

### 2. Real-World Analogies and Use-Cases

*   **Analogy:** Imagine a network of one-way flights between cities. Warshall's algorithm helps determine *all* pairs of cities (A, B) such that you can eventually fly from A to B, possibly with multiple layovers.
*   **Use-Cases:** Checking reachability in networks (computer networks, social networks), logic inference, context-free grammar analysis, finding dependencies.

### 3. Step-by-Step Solved Example

**Problem:** Find the transitive closure of the following graph:
Nodes: {1, 2, 3}
Edges: (1, 2), (2, 3)

**Initial Adjacency Matrix (R^(0)):** (1 if edge exists, 0 otherwise. Diagonal is 0 or 1 depending on definition, let's use 0 for simplicity unless self-loops exist)

```
   1 2 3
1 [0 1 0]
2 [0 0 1]
3 [0 0 0]
```

**Iteration k = 1:** (Can we reach j from i via node 1?)
*   Check (i, j) pairs using `R[i][j] = R[i][j] OR (R[i][1] AND R[1][j])`
*   (2, 2): `R[2][2] = R[2][2] OR (R[2][1] AND R[1][2]) = 0 OR (0 AND 1) = 0`
*   (3, 2): `R[3][2] = R[3][2] OR (R[3][1] AND R[1][2]) = 0 OR (0 AND 1) = 0`
*   ... (No changes occur as there are no paths *into* 1 and *out of* 1 to create new paths)
*   **R^(1) = R^(0)**

**Iteration k = 2:** (Can we reach j from i via node 2?)
*   Check (i, j) pairs using `R[i][j] = R[i][j] OR (R[i][2] AND R[2][j])`
*   (1, 3): `R[1][3] = R[1][3] OR (R[1][2] AND R[2][3]) = 0 OR (1 AND 1) = 1`. **Update!**
*   **R^(2):**
    ```
       1 2 3
    1 [0 1 1]  <- Changed
    2 [0 0 1]
    3 [0 0 0]
    ```

**Iteration k = 3:** (Can we reach j from i via node 3?)
*   Check (i, j) pairs using `R[i][j] = R[i][j] OR (R[i][3] AND R[3][j])`
*   (1, ?): `R[1][3]` is 1. `R[3][j]` is always 0. No change.
*   (2, ?): `R[2][3]` is 1. `R[3][j]` is always 0. No change.
*   **R^(3) = R^(2)**

**Final Transitive Closure Matrix (T = R^(3)):**

```
   1 2 3
1 [0 1 1]  (1 can reach 2 directly, 1 can reach 3 via 2)
2 [0 0 1]  (2 can reach 3 directly)
3 [0 0 0]  (3 cannot reach any other node)
```
*(Note: Often, the diagonal T[i][i] is set to 1 if reachability includes paths of length 0. If only paths > 0, keep as is or based on self-loops in original graph).*

### 4. Pseudocode and Code Implementation

**Pseudocode:**

```pseudocode
function Warshall(Graph G):
  n = number of vertices in G
  // Initialize R^(0) as the adjacency matrix (boolean or 0/1)
  // R[i][j] = 1 if edge (i, j) exists or i == j, else 0
  // (Adjust diagonal based on whether path length 0 counts)
  R = AdjacencyMatrix(G)
  // Optionally set R[i][i] = 1 for all i

  for k from 1 to n: // Intermediate vertex
    for i from 1 to n: // Start vertex
      for j from 1 to n: // End vertex
        R[i][j] = R[i][j] OR (R[i][k] AND R[k][j])

  return R // The Transitive Closure Matrix
```

**Python Implementation:**

```python
def warshall(graph):
    """
    Computes the transitive closure of a graph using Warshall's algorithm.
    Args:
        graph: A list of lists representing the adjacency matrix (0 or 1).
               graph[i][j] = 1 if there is an edge from i to j.
    Returns:
        A list of lists representing the transitive closure matrix.
    """
    n = len(graph)
    # Copy the graph to create the reachability matrix
    reach = [row[:] for row in graph]

    # Optional: Include self-loops in reachability
    # for i in range(n):
    #     reach[i][i] = 1

    for k in range(n):  # Intermediate vertex
        for i in range(n):  # Source vertex
            for j in range(n):  # Destination vertex
                # If path i->k and k->j exists, then path i->j exists
                reach[i][j] = reach[i][j] or (reach[i][k] and reach[k][j])

    return reach

# Example Usage:
adj_matrix = [
    [0, 1, 0],
    [0, 0, 1],
    [0, 0, 0]
]
transitive_closure = warshall(adj_matrix)
print("Original Adjacency Matrix:")
for row in adj_matrix: print(row)
print("\nTransitive Closure Matrix:")
for row in transitive_closure: print(row)
# Output:
# Original Adjacency Matrix:
# [0, 1, 0]
# [0, 0, 1]
# [0, 0, 0]
#
# Transitive Closure Matrix:
# [0, 1, 1]
# [0, 0, 1]
# [0, 0, 0]
```

**C++ Implementation:**

```c++
#include <vector>
#include <iostream>

using namespace std;

vector<vector<bool>> warshall(const vector<vector<bool>>& graph) {
    int n = graph.size();
    if (n == 0) return {};

    // Copy the graph to create the reachability matrix
    vector<vector<bool>> reach = graph;

    // Optional: Include self-loops
    // for (int i = 0; i < n; ++i) {
    //     reach[i][i] = true;
    // }

    for (int k = 0; k < n; ++k) { // Intermediate vertex
        for (int i = 0; i < n; ++i) { // Source vertex
            for (int j = 0; j < n; ++j) { // Destination vertex
                // If path i->k and k->j exists, then path i->j exists
                reach[i][j] = reach[i][j] || (reach[i][k] && reach[k][j]);
            }
        }
    }
    return reach;
}

int main() {
    // Example graph (same as Python example)
    vector<vector<bool>> adj_matrix = {
        {false, true, false},
        {false, false, true},
        {false, false, false}
    };

    vector<vector<bool>> transitive_closure = warshall(adj_matrix);

    cout << "Original Adjacency Matrix (0/1):" << endl;
    for (int i = 0; i < adj_matrix.size(); ++i) {
        for (int j = 0; j < adj_matrix[i].size(); ++j) {
            cout << adj_matrix[i][j] << " ";
        }
        cout << endl;
    }

    cout << "\nTransitive Closure Matrix (0/1):" << endl;
    for (int i = 0; i < transitive_closure.size(); ++i) {
        for (int j = 0; j < transitive_closure[i].size(); ++j) {
            cout << transitive_closure[i][j] << " ";
        }
        cout << endl;
    }

    return 0;
}
```

### 5. Diagrams or Flowcharts

**Flowchart:**

```
Start
|
Initialize Reachability Matrix R = Adjacency Matrix
|
Set k = 0
|
+-----------------------+
| Is k < n ?            |-- No --> End
+-----------------------+
       | Yes
       | Set i = 0
       |
       +-----------------------+
       | Is i < n ?            |-- No --> Increment k, Go back to k loop check
       +-----------------------+
              | Yes
              | Set j = 0
              |
              +-----------------------+
              | Is j < n ?            |-- No --> Increment i, Go back to i loop check
              +-----------------------+
                     | Yes
                     | R[i][j] = R[i][j] OR (R[i][k] AND R[k][j])
                     | Increment j
                     +-----------------------+
```

### 6. Key Formulas and Logic Summary

*   **Core Logic:** `R^(k)[i][j] = R^(k-1)[i][j] OR (R^(k-1)[i][k] AND R^(k-1)[k][j])`
*   **Input:** Adjacency matrix of a directed graph.
*   **Output:** Transitive closure matrix (boolean or 0/1).
*   **Time Complexity:** O(n^3), where n is the number of vertices.
*   **Space Complexity:** O(n^2) for storing the matrix.

### 7. Common Mistakes and Edge Cases

*   **Incorrect Initialization:** Forgetting to copy the initial adjacency matrix properly.
*   **Loop Order:** The order of loops (`k`, `i`, `j`) is crucial. `k` must be the outermost loop. Swapping them leads to incorrect results.
*   **Boolean vs. Integer:** Using integer addition instead of logical OR if the matrix stores 0/1.
*   **Self-Loops:** Deciding whether T[i][i] should be true (path of length 0) or depend on actual self-loops in the graph. Be consistent.
*   **Undirected Graphs:** While applicable, it's less common. If used, ensure the initial adjacency matrix is symmetric.

### 8. MCQ/Short Questions and Answers

1.  **Q:** What does Warshall's algorithm compute?
    **A:** The transitive closure of a directed graph (all pairs reachability).
2.  **Q:** What is the time complexity of Warshall's algorithm?
    **A:** O(n^3).
3.  **Q:** What is the core logical operation in Warshall's algorithm update step?
    **A:** `R[i][j] = R[i][j] OR (R[i][k] AND R[k][j])`.
4.  **Q:** Why must the loop for the intermediate vertex `k` be the outermost loop?
    **A:** Because the calculation `R^(k)` relies entirely on the completed results of `R^(k-1)`. Placing `k` inside would use partially updated values from the current `k` iteration, leading to errors.
5.  **Q:** Can Warshall's algorithm detect negative cycles?
    **A:** No, Warshall's algorithm deals with reachability (existence of paths), not path weights or cycles. Floyd's algorithm handles weights.

---

## 3. Floyd's Algorithm (Floyd-Warshall Algorithm)

### 1. Concept Explanation

*   **What:** Floyd's algorithm (often called Floyd-Warshall) solves the **All-Pairs Shortest Paths (APSP)** problem for a weighted directed graph. It finds the shortest path distance between *every* pair of vertices. It can handle graphs with negative edge weights, but not negative cycles.
*   **Why DP:** Similar to Warshall's, it uses a DP approach. It finds the shortest path from `i` to `j` using only intermediate vertices from a progressively larger set `{1, ..., k}`.
*   **How:** It uses a distance matrix `D` initialized with direct edge weights (infinity if no direct edge, 0 for `D[i][i]`). It iterates through all possible intermediate vertices `k`. For every pair `(i, j)`, it checks if going from `i` to `k` and then from `k` to `j` gives a shorter path than the current known shortest path from `i` to `j`. If so, it updates `D[i][j]`.
*   **Logic:** `D^(k)[i][j] = min( D^(k-1)[i][j], D^(k-1)[i][k] + D^(k-1)[k][j] )`. This means the shortest path from `i` to `j` using intermediates from `{1, ..., k}` is the minimum of: (1) the shortest path using only `{1, ..., k-1}`, and (2) the path going from `i` to `k` and then `k` to `j` (both using only intermediates from `{1, ..., k-1}`).

### 2. Real-World Analogies and Use-Cases

*   **Analogy:** Finding the shortest driving distance between all pairs of cities in a region, considering all possible intermediate cities you could drive through.
*   **Use-Cases:** Network routing (finding shortest paths between all nodes), computational biology (sequence alignment, phylogenetic distance), transit networks (shortest travel times), checking for negative cycles.

### 3. Step-by-Step Solved Example

**Problem:** Find all-pairs shortest paths for the graph:
Nodes: {1, 2, 3}
Edges: (1, 2, 3), (1, 3, 8), (2, 1, 2), (2, 3, 2), (3, 1, 5), (3, 2, -1)
*(Weight notation: (source, destination, weight))*

**Initial Distance Matrix (D^(0)):** (Use ∞ for no direct edge, 0 for diagonal)

```
   1  2  3
1 [0  3  8]
2 [2  0  2]
3 [5 -1  0]
```

**Iteration k = 1:** (Can we shorten paths via node 1?)
*   Check `D[i][j] = min(D[i][j], D[i][1] + D[1][j])`
*   (2, 2): `min(D[2][2], D[2][1] + D[1][2]) = min(0, 2 + 3) = min(0, 5) = 0`
*   (2, 3): `min(D[2][3], D[2][1] + D[1][3]) = min(2, 2 + 8) = min(2, 10) = 2`
*   (3, 2): `min(D[3][2], D[3][1] + D[1][2]) = min(-1, 5 + 3) = min(-1, 8) = -1`
*   (3, 3): `min(D[3][3], D[3][1] + D[1][3]) = min(0, 5 + 8) = min(0, 13) = 0`
*   **D^(1) = D^(0)** (No changes in this case)

**Iteration k = 2:** (Can we shorten paths via node 2?)
*   Check `D[i][j] = min(D[i][j], D[i][2] + D[2][j])`
*   (1, 1): `min(D[1][1], D[1][2] + D[2][1]) = min(0, 3 + 2) = min(0, 5) = 0`
*   (1, 3): `min(D[1][3], D[1][2] + D[2][3]) = min(8, 3 + 2) = min(8, 5) = 5`. **Update!**
*   (3, 1): `min(D[3][1], D[3][2] + D[2][1]) = min(5, -1 + 2) = min(5, 1) = 1`. **Update!**
*   (3, 3): `min(D[3][3], D[3][2] + D[2][3]) = min(0, -1 + 2) = min(0, 1) = 0`
*   **D^(2):**
    ```
       1  2  3
    1 [0  3  5]  <- Changed
    2 [2  0  2]
    3 [1 -1  0]  <- Changed
    ```

**Iteration k = 3:** (Can we shorten paths via node 3?)
*   Check `D[i][j] = min(D[i][j], D[i][3] + D[3][j])`
*   (1, 1): `min(D[1][1], D[1][3] + D[3][1]) = min(0, 5 + 1) = min(0, 6) = 0`
*   (1, 2): `min(D[1][2], D[1][3] + D[3][2]) = min(3, 5 + (-1)) = min(3, 4) = 3`
*   (2, 1): `min(D[2][1], D[2][3] + D[3][1]) = min(2, 2 + 1) = min(2, 3) = 2`
*   (2, 2): `min(D[2][2], D[2][3] + D[3][2]) = min(0, 2 + (-1)) = min(0, 1) = 0`
*   **D^(3):** (No changes in this iteration)
    ```
       1  2  3
    1 [0  3  5]
    2 [2  0  2]
    3 [1 -1  0]
    ```

**Final Shortest Path Distance Matrix (D = D^(3)):**

```
   1  2  3
1 [0  3  5]
2 [2  0  2]
3 [1 -1  0]
```
This matrix shows the minimum cost to travel between any pair of nodes. E.g., shortest path from 1 to 3 is 5. Shortest path from 3 to 1 is 1.

**Detecting Negative Cycles:** After the algorithm completes, check the diagonal elements `D[i][i]`. If any `D[i][i]` is negative, it indicates that node `i` is part of, or can reach, a negative cycle.

### 4. Pseudocode and Code Implementation

**Pseudocode:**

```pseudocode
function FloydWarshall(Graph G with weights W):
  n = number of vertices in G
  // Initialize D^(0) matrix
  D = new array[n+1][n+1]
  for i from 1 to n:
    for j from 1 to n:
      if i == j:
        D[i][j] = 0
      else if edge (i, j) exists:
        D[i][j] = W[i][j] // Weight of direct edge
      else:
        D[i][j] = INFINITY

  // Main loops
  for k from 1 to n: // Intermediate vertex
    for i from 1 to n: // Start vertex
      for j from 1 to n: // End vertex
        // Check if path through k is shorter
        if D[i][k] != INFINITY AND D[k][j] != INFINITY: // Avoid overflow with INFINITY
           D[i][j] = min(D[i][j], D[i][k] + D[k][j])

  // Optional: Check for negative cycles
  for i from 1 to n:
    if D[i][i] < 0:
      // Negative cycle detected
      Report "Negative cycle exists"

  return D // The matrix of shortest path distances
```

**Python Implementation:**

```python
import math

INF = math.inf

def floyd_warshall(graph_weights):
    """
    Computes all-pairs shortest paths using Floyd-Warshall algorithm.
    Args:
        graph_weights: A list of lists representing the weighted adjacency matrix.
                       Use INF for no direct edge, 0 for diagonal.
    Returns:
        A tuple: (distance matrix, predecessor matrix or None)
                 Returns (None, None) if a negative cycle is detected.
    """
    n = len(graph_weights)
    if n == 0:
        return [], []

    dist = [row[:] for row in graph_weights]
    # Predecessor matrix (optional, for path reconstruction)
    pred = [[None] * n for _ in range(n)]
    for i in range(n):
        for j in range(n):
            if i != j and graph_weights[i][j] != INF:
                pred[i][j] = i # Direct edge predecessor is i

    for k in range(n):  # Intermediate vertex
        for i in range(n):  # Source vertex
            for j in range(n):  # Destination vertex
                # Check for potential path improvement via k
                if dist[i][k] != INF and dist[k][j] != INF:
                    new_dist = dist[i][k] + dist[k][j]
                    if new_dist < dist[i][j]:
                        dist[i][j] = new_dist
                        pred[i][j] = pred[k][j] # Update predecessor

        # Check for negative cycles after each k iteration (or just at the end)
        for i in range(n):
            if dist[i][i] < 0:
                print("Negative cycle detected!")
                return None, None # Indicate error

    return dist, pred

# Example Usage:
weights = [
    [0, 3, 8],
    [2, 0, 2],
    [5, -1, 0]
]
shortest_paths, predecessors = floyd_warshall(weights)

if shortest_paths:
    print("Shortest Path Distances:")
    for row in shortest_paths:
        print([f"{d:.0f}" if d != INF else "INF" for d in row])
    # print("\nPredecessor Matrix:") # For path reconstruction
    # for row in predecessors: print(row)

# Example path reconstruction (2 -> 1):
# Path: 2 -> ... -> 1. pred[2][1] = 3 (means path is 2 -> ... -> 3 -> 1)
# Path: 2 -> ... -> 3. pred[2][3] = 2 (means path is 2 -> 3)
# Full path: 2 -> 3 -> 1 (Matches D[2][1]=2, which is D[2][3]+D[3][1] = 2+1=3 - ERROR in manual trace, let's recheck)
# Recheck k=2:
# (3, 1): min(D[3][1], D[3][2] + D[2][1]) = min(5, -1 + 2) = min(5, 1) = 1. Correct. D[3][1] becomes 1.
# Recheck k=3:
# (2, 1): min(D[2][1], D[2][3] + D[3][1]) = min(2, 2 + 1) = min(2, 3) = 2. Correct. D[2][1] stays 2.
# Final Matrix D:
#    1  2  3
# 1 [0  3  5]
# 2 [2  0  2]
# 3 [1 -1  0]
# Path 2->1: Cost is 2. Predecessor pred[2][1] should reflect the path.
# Let's trace predecessors carefully:
# Initial pred: [[None, 0, 0], [1, None, 1], [2, 2, None]] (pred[i][j] = i if edge i->j)
# k=1: No changes
# k=2:
#   dist[1][3] updated (5 < 8) via k=2. Path 1->2->3. pred[1][3] = pred[2][3] = 1.
#   dist[3][1] updated (1 < 5) via k=2. Path 3->2->1. pred[3][1] = pred[2][1] = 1.
# k=3:
#   No distance changes.
# Final Predecessor Matrix (approx):
# [[None, 0, 1], [1, None, 1], [1, 2, None]]
# Path 2->1: pred[2][1] = 1. Path is 2 -> ... -> 1. Predecessor is 1. Path is 2->1. Cost 2. Correct.
# Path 3->1: pred[3][1] = 1. Path is 3 -> ... -> 1. Predecessor is 1. Path is 3->1. Cost 1. Correct.
# Path 1->3: pred[1][3] = 1. Path is 1 -> ... -> 3. Predecessor is 1. Path is 1->3? No, cost is 5. Path is 1->2->3.
# Let's re-run pred logic: If dist[i][j] updated via k, pred[i][j] = pred[k][j].
# k=2:
#   dist[1][3] updated (5 < 8) via k=2. pred[1][3] = pred[2][3] = 1.
#   dist[3][1] updated (1 < 5) via k=2. pred[3][1] = pred[2][1] = 1.
# Final Pred: [[None, 0, 1], [1, None, 1], [1, 2, None]]
# Reconstruct 1->3: End=3. pred[1][3]=1. Path: ...->1->3. End=1. pred[1][1]=None? No, need start node.
# Path reconstruction needs a loop:
# def get_path(pred, start, end):
#   path = [end]
#   curr = end
#   while pred[start][curr] is not None and pred[start][curr] != start:
#      curr = pred[start][curr]
#      path.append(curr)
#   path.append(start)
#   return path[::-1] # Reverse
# Let's try again with standard pred definition: pred[i][j] = k that optimizes path i->j.
# Need separate pred matrix init: [[j if graph[i][j] != INF else None for j ..] for i ..]
# Let's skip detailed path reconstruction here, focus on distances.

```

**C++ Implementation:**

```c++
#include <vector>
#include <iostream>
#include <algorithm> // For std::min
#include <limits>    // For numeric_limits

const double INF = std::numeric_limits<double>::infinity();

using namespace std;

// Function to print the distance matrix
void printMatrix(const vector<vector<double>>& dist) {
    int n = dist.size();
    cout << "Shortest Path Distances:" << endl;
    for (int i = 0; i < n; ++i) {
        for (int j = 0; j < n; ++j) {
            if (dist[i][j] == INF) {
                cout << "INF ";
            } else {
                cout << dist[i][j] << "  ";
            }
        }
        cout << endl;
    }
}

vector<vector<double>> floyd_warshall(const vector<vector<double>>& graph_weights) {
    int n = graph_weights.size();
    if (n == 0) return {};

    vector<vector<double>> dist = graph_weights;

    for (int k = 0; k < n; ++k) { // Intermediate vertex
        for (int i = 0; i < n; ++i) { // Source vertex
            for (int j = 0; j < n; ++j) { // Destination vertex
                // Check if path through k is shorter
                // Avoid overflow with INF
                if (dist[i][k] != INF && dist[k][j] != INF) {
                    dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j]);
                }
            }
        }
    }

    // Check for negative cycles
    for (int i = 0; i < n; ++i) {
        if (dist[i][i] < 0) {
            cerr << "Error: Negative cycle detected!" << endl;
            // Return an empty matrix or throw an exception to indicate error
            return {};
        }
    }

    return dist;
}

int main() {
    // Example graph (same as Python example)
    vector<vector<double>> weights = {
        {0, 3, 8},
        {2, 0, 2},
        {5, -1, 0}
    };
    // Replace large number with INF if needed, or handle during init
     for(int i=0; i<weights.size(); ++i) {
         for(int j=0; j<weights[i].size(); ++j) {
             if (i != j && weights[i][j] == 8) weights[i][j] = INF; // Example: Treat 8 as INF if it means no path
         }
     }
     // Let's use the original weights, assuming they are actual weights
     weights = { {0, 3, 8}, {2, 0, 2}, {5, -1, 0} };


    vector<vector<double>> shortest_paths = floyd_warshall(weights);

    if (!shortest_paths.empty()) {
        printMatrix(shortest_paths);
    }

    return 0;
}
// C++ Output (using original weights):
// Shortest Path Distances:
// 0  3  5
// 2  0  2
// 1 -1  0
```

### 5. Diagrams or Flowcharts

Similar flowchart structure to Warshall's, but the update step changes:

```
Start
|
Initialize Distance Matrix D based on weights (0 on diag, INF if no edge)
|
Set k = 0
|
+-----------------------+
| Is k < n ?            |-- No --> Check Negative Cycles, End
+-----------------------+
       | Yes
       | Set i = 0
       |
       +-----------------------+
       | Is i < n ?            |-- No --> Increment k, Go back to k loop check
       +-----------------------+
              | Yes
              | Set j = 0
              |
              +-----------------------+
              | Is j < n ?            |-- No --> Increment i, Go back to i loop check
              +-----------------------+
                     | Yes
                     | // Check for valid path through k
                     | if D[i][k] != INF AND D[k][j] != INF:
                     |   D[i][j] = min(D[i][j], D[i][k] + D[k][j])
                     | Increment j
                     +-----------------------+
```

### 6. Key Formulas and Logic Summary

*   **Core Logic:** `D^(k)[i][j] = min( D^(k-1)[i][j], D^(k-1)[i][k] + D^(k-1)[k][j] )`
*   **Input:** Weighted adjacency matrix (use INF for no edge).
*   **Output:** Matrix of shortest path distances between all pairs.
*   **Time Complexity:** O(n^3)
*   **Space Complexity:** O(n^2)
*   **Negative Cycles:** Detectable if `D[i][i] < 0` after completion.

### 7. Common Mistakes and Edge Cases

*   **Loop Order:** Like Warshall's, `k` must be the outermost loop.
*   **Initialization:** Correctly setting initial distances (0 for `i==j`, weight for direct edges, INF otherwise).
*   **Infinity Arithmetic:** Handling `INF + weight` (still INF) and `INF + INF`. Check `D[i][k]` and `D[k][j]` are not INF before adding.
*   **Negative Cycles:** Forgetting to check for them or misinterpreting the result if they exist (shortest paths are ill-defined).
*   **Path Reconstruction:** Requires a separate predecessor matrix and careful logic to trace paths back.

### 8. MCQ/Short Questions and Answers

1.  **Q:** What problem does Floyd-Warshall solve?
    **A:** 
	
2.  **Q:** What is the time complexity of Floyd-Warshall?
    **A:** O(n^3).
3.  **Q:** Can Floyd-Warshall handle negative edge weights?
    **A:** Yes.
4.  **Q:** Can Floyd-Warshall handle negative cycles?
    **A:** It can detect them (if `D[i][i]` becomes negative), but the shortest path distances are not meaningful in their presence.
5.  **Q:** What is the core update rule in Floyd-Warshall?
    **A:** `D[i][j] = min(D[i][j], D[i][k] + D[k][j])`.

---

## 4. Optimal Binary Search Trees (OBST)

### 1. Concept Explanation

*   **What:** Given a sorted sequence of keys `k_1, k_2, ..., k_n` and their probabilities of being searched `p_1, p_2, ..., p_n` (and optionally probabilities `q_0, q_1, ..., q_n` of searching for values *between* keys, representing unsuccessful searches), the Optimal Binary Search Tree (OBST) problem is to construct a BST that minimizes the *expected search cost*.
*   **Why DP:** The problem has optimal substructure. An optimal BST for keys `k_i, ..., k_j` with root `k_r` must have its left subtree be an optimal BST for `k_i, ..., k_{r-1}` and its right subtree be an optimal BST for `k_{r+1}, ..., k_j`. It also has overlapping subproblems, as the cost of subtrees like `(k_i, ..., k_m)` might be needed for multiple larger trees.
*   **How:** We use DP to compute the minimum expected cost for BSTs containing keys `k_i` through `k_j`. Let `cost(i, j)` be the minimum cost for keys `k_i` to `k_j`. We try each key `k_r` (where `i <= r <= j`) as the root. The cost if `k_r` is the root is `cost(i, r-1) + cost(r+1, j) + sum_of_probabilities(i, j)`. The `sum_of_probabilities` term accounts for the fact that every node in the subtree `(i, j)` increases its depth by 1 when `k_r` becomes the root. We choose the `k_r` that minimizes this total cost.
*   **Formula:**
    `cost(i, j) = min_{i <= r <= j} { cost(i, r-1) + cost(r+1, j) + W(i, j) }` for `i <= j`
    `cost(i, i-1) = 0` (Base case: empty tree)
    `W(i, j) = sum(p_k for k from i to j) + sum(q_k for k from i-1 to j)` (Total probability weight of the subtree)
    *(Simplified version often only uses key probabilities `p_k`, so `W(i, j) = sum(p_k for k from i to j)`)*

### 2. Real-World Analogies and Use-Cases

*   **Analogy:** Designing a dictionary or encyclopedia index. You want to place the most frequently looked-up words/topics closer to the "front" (root of the search tree) to minimize average lookup time.
*   **Use-Cases:** Compiler design (symbol tables), dictionary implementation, data retrieval systems where access frequencies are known or can be estimated.

### 3. Step-by-Step Solved Example

**Problem:** Construct an OBST for keys {10, 20, 30} with search probabilities P = {p1=0.2, p2=0.3, p3=0.1}. For simplicity, let's ignore unsuccessful search probabilities (q_i = 0).

Keys: K = {10, 20, 30} (Indices i=1, 2, 3)
Probs: P = {0.2, 0.3, 0.1}

Calculate `W(i, j) = sum(p_k for k from i to j)`:
*   W(1, 1) = p1 = 0.2
*   W(2, 2) = p2 = 0.3
*   W(3, 3) = p3 = 0.1
*   W(1, 2) = p1 + p2 = 0.5
*   W(2, 3) = p2 + p3 = 0.4
*   W(1, 3) = p1 + p2 + p3 = 0.6

Initialize DP table `cost[n+1][n]` (or similar, e.g., `cost[1..n+1][0..n]`). `cost[i][j]` stores min cost for keys `i` to `j`.
Base cases: `cost[i][i-1] = 0`

**Length l = 1 (Subtrees with 1 key):**
*   `cost[1][1] = min_{r=1} {cost[1][0] + cost[2][1] + W(1, 1)} = 0 + 0 + 0.2 = 0.2` (Root=10)
*   `cost[2][2] = min_{r=2} {cost[2][1] + cost[3][2] + W(2, 2)} = 0 + 0 + 0.3 = 0.3` (Root=20)
*   `cost[3][3] = min_{r=3} {cost[3][2] + cost[4][3] + W(3, 3)} = 0 + 0 + 0.1 = 0.1` (Root=30)

**Length l = 2 (Subtrees with 2 keys):**
*   `cost[1][2]` (Keys 10, 20):
    *   Try r=1 (Root=10): `cost[1][0] + cost[2][2] + W(1, 2) = 0 + 0.3 + 0.5 = 0.8`
    *   Try r=2 (Root=20): `cost[1][1] + cost[3][2] + W(1, 2) = 0.2 + 0 + 0.5 = 0.7`
    *   `cost[1][2] = min(0.8, 0.7) = 0.7` (Root=20)
*   `cost[2][3]` (Keys 20, 30):
    *   Try r=2 (Root=20): `cost[2][1] + cost[3][3] + W(2, 3) = 0 + 0.1 + 0.4 = 0.5`
    *   Try r=3 (Root=30): `cost[2][2] + cost[4][3] + W(2, 3) = 0.3 + 0 + 0.4 = 0.7`
    *   `cost[2][3] = min(0.5, 0.7) = 0.5` (Root=20)

**Length l = 3 (Subtree with 3 keys - the whole tree):**
*   `cost[1][3]` (Keys 10, 20, 30):
    *   Try r=1 (Root=10): `cost[1][0] + cost[2][3] + W(1, 3) = 0 + 0.5 + 0.6 = 1.1`
    *   Try r=2 (Root=20): `cost[1][1] + cost[3][3] + W(1, 3) = 0.2 + 0.1 + 0.6 = 0.9`
    *   Try r=3 (Root=30): `cost[1][2] + cost[4][3] + W(1, 3) = 0.7 + 0 + 0.6 = 1.3`
    *   `cost[1][3] = min(1.1, 0.9, 1.3) = 0.9` (Root=20)

**Result:** The minimum expected search cost is 0.9. The optimal root for the entire tree is key 20.
To reconstruct the tree, we need to store the optimal root `r` chosen for each `cost[i][j]`.
*   Root(1, 3) = 2 (Key 20)
*   Left subtree (1, 1): Root(1, 1) = 1 (Key 10)
*   Right subtree (3, 3): Root(3, 3) = 3 (Key 30)

**Optimal Tree Structure:**

```
      20 (p=0.3)
     /  \
10(p=0.2) 30(p=0.1)
```

**Cost Calculation Check:**
Cost = sum(p_i * depth(k_i))
Depth(20) = 1, Depth(10) = 2, Depth(30) = 2
Expected Cost = p2*1 + p1*2 + p3*2 = 0.3*1 + 0.2*2 + 0.1*2 = 0.3 + 0.4 + 0.2 = 0.9. Matches!

### 4. Pseudocode and Code Implementation

**Pseudocode:**

```pseudocode
function OptimalBST(keys K, probabilities P, dummy_probabilities Q): // Q can be all zeros
  n = length(K)
  // Initialize cost table C[1..n+1][0..n] and weight table W[1..n+1][0..n]
  // Initialize root table R[1..n][1..n] to store optimal root for C[i][j]
  C = new array[n+2][n+1] // Use 1-based indexing for keys, 0-based for dummy intervals
  W = new array[n+2][n+1]
  R = new array[n+1][n+1]

  // Initialize base cases for cost and weight (for intervals of length 0)
  for i from 1 to n + 1:
    C[i][i-1] = 0
    W[i][i-1] = Q[i-1] // Weight of dummy key q_{i-1}

  // Calculate costs for subtrees of increasing length l
  for l from 1 to n: // l = length (j - i + 1)
    for i from 1 to n - l + 1:
      j = i + l - 1
      // Calculate weight W(i, j)
      W[i][j] = W[i][j-1] + P[j] + Q[j] // Assumes P is 1-indexed, Q is 0-indexed

      // Initialize cost for this subproblem to infinity
      C[i][j] = INFINITY

      // Try each key k_r as root (r from i to j)
      for r from i to j:
        current_cost = C[i][r-1] + C[r+1][j] + W[i][j]
        if current_cost < C[i][j]:
          C[i][j] = current_cost
          R[i][j] = r // Store index r of the key K[r]

  return C[1][n], R // Min cost and root table for reconstruction
```

**Python Implementation:**

```python
import sys

def optimal_bst(keys, freqs):
    """
    Calculates the minimum cost of an Optimal Binary Search Tree.
    Args:
        keys: Sorted list of keys.
        freqs: List of frequencies/probabilities corresponding to keys.
               (Assumes only successful searches for simplicity here).
    Returns:
        Minimum cost. (Also computes root table internally for reconstruction).
    """
    n = len(keys)
    # Cost table: cost[i][j] = min cost for keys[i..j]
    # Use 0-based indexing for keys/freqs list, but logic maps to 1..n concept
    cost = [[0.0] * n for _ in range(n)]
    # Optional: root table for reconstruction
    root = [[0] * n for _ in range(n)]

    # Precompute cumulative frequencies (Weights W(i,j))
    cum_freq = [0.0] * (n + 1)
    for i in range(n):
        cum_freq[i+1] = cum_freq[i] + freqs[i]

    def get_weight(i, j):
        if i > j: return 0.0
        # W(i, j) = sum(freqs[k] for k from i to j)
        return cum_freq[j+1] - cum_freq[i]

    # Base case: single node trees
    for i in range(n):
        cost[i][i] = freqs[i] # Cost is just the frequency (depth 1)
        root[i][i] = i       # Root is the node itself

    # Fill table for lengths l = 2 to n
    for length in range(2, n + 1):
        for i in range(n - length + 1):
            j = i + length - 1
            cost[i][j] = sys.float_info.max
            weight_ij = get_weight(i, j)

            for r in range(i, j + 1): # Try key r (index r) as root
                # Cost if r is root: cost(i, r-1) + cost(r+1, j) + W(i, j)
                left_cost = cost[i][r-1] if r > i else 0.0
                right_cost = cost[r+1][j] if r < j else 0.0
                current_cost = left_cost + right_cost + weight_ij

                if current_cost < cost[i][j]:
                    cost[i][j] = current_cost
                    root[i][j] = r # Store index of the root key

    # print("Root table (indices):")
    # for row in root: print(row)
    return cost[0][n-1] # Min cost for the whole tree (keys 0 to n-1)

# Example Usage (from step-by-step):
keys_list = [10, 20, 30]
freq_list = [0.2, 0.3, 0.1]
min_cost = optimal_bst(keys_list, freq_list)
print(f"Minimum expected search cost: {min_cost}") # Output: 0.9
```

**C++ Implementation:**

```c++
#include <vector>
#include <iostream>
#include <numeric>   // For std::accumulate (or manual sum)
#include <limits>    // For std::numeric_limits
#include <algorithm> // For std::min

using namespace std;

// Helper to get sum of frequencies (Weight W(i,j))
double get_weight(const vector<double>& freqs, int i, int j) {
    if (i > j) return 0.0;
    double sum = 0.0;
    // Ensure indices are within bounds
    for (int k = max(0, i); k <= min((int)freqs.size() - 1, j); ++k) {
         sum += freqs[k];
    }
    return sum;
    // Alternative using precomputed sums:
    // vector<double> cum_freq(freqs.size() + 1, 0.0);
    // for(int k=0; k<freqs.size(); ++k) cum_freq[k+1] = cum_freq[k] + freqs[k];
    // return cum_freq[j+1] - cum_freq[i];
}


double optimal_bst(const vector<int>& keys, const vector<double>& freqs) {
    int n = keys.size();
    if (n == 0) return 0.0;

    // Cost table: cost[i][j] = min cost for keys[i..j]
    vector<vector<double>> cost(n, vector<double>(n, 0.0));
    // Optional: root table
    vector<vector<int>> root(n, vector<int>(n, 0));

    // Precompute cumulative frequencies for efficiency
    vector<double> cum_freq(n + 1, 0.0);
    for(int i=0; i<n; ++i) cum_freq[i+1] = cum_freq[i] + freqs[i];

    auto calculate_weight = [&](int i, int j) {
        if (i > j) return 0.0;
        return cum_freq[j+1] - cum_freq[i];
    };


    // Base case: single node trees
    for (int i = 0; i < n; ++i) {
        cost[i][i] = freqs[i]; // Cost is frequency (depth 1 relative to subtree root)
        root[i][i] = i;
    }

    // Fill table for lengths l = 2 to n
    for (int length = 2; length <= n; ++length) {
        for (int i = 0; i <= n - length; ++i) {
            int j = i + length - 1;
            cost[i][j] = numeric_limits<double>::max();
            double weight_ij = calculate_weight(i, j);

            for (int r = i; r <= j; ++r) { // Try key r (index r) as root
                double left_cost = (r > i) ? cost[i][r - 1] : 0.0;
                double right_cost = (r < j) ? cost[r + 1][j] : 0.0;
                double current_cost = left_cost + right_cost + weight_ij;

                if (current_cost < cost[i][j]) {
                    cost[i][j] = current_cost;
                    root[i][j] = r;
                }
            }
        }
    }

    // cout << "Root table (indices):" << endl;
    // for(int i=0; i<n; ++i) { for(int j=0; j<n; ++j) cout << root[i][j] << " "; cout << endl; }

    return cost[0][n - 1]; // Min cost for the whole tree
}

int main() {
    vector<int> keys_list = {10, 20, 30};
    vector<double> freq_list = {0.2, 0.3, 0.1};
    double min_cost = optimal_bst(keys_list, freq_list);
    cout << "Minimum expected search cost: " << min_cost << endl; // Output: 0.9
    return 0;
}
```

### 5. Diagrams or Flowcharts

**DP Table `cost[i][j]` Filling Order:**

```
j=0  j=1  j=2  j=3 ... j=n-1
i=0 [ L=1] [L=2 ] [L=3 ] ... [ L=n ]
i=1      [ L=1] [L=2 ] ... [L=n-1]
i=2           [ L=1] ... [L=n-2]
...                ...
i=n-1                     [ L=1 ]
```
Fill along diagonals, starting from main diagonal (Length L=1) upwards/rightwards to the top-right corner (L=n).

**Example Tree Construction:**

```
Root(0, 2) = 1 (Key 20)
   /       \
Root(0, 0)=0  Root(2, 2)=2
 (Key 10)      (Key 30)

Resulting Tree:
      20
     /  \
    10  30
```

### 6. Key Formulas and Logic Summary

*   **Goal:** Minimize expected search cost `Sum(p_i * depth(k_i)) + Sum(q_j * depth(dummy_j))`.
*   **Recurrence:** `cost(i, j) = min_{i <= r <= j} { cost(i, r-1) + cost(r+1, j) + W(i, j) }`
*   **Weight:** `W(i, j) = Sum(p_k for k=i..j) + Sum(q_k for k=i-1..j)`
*   **Base Case:** `cost(i, i-1) = q_{i-1}` (or 0 if only considering successful searches). `cost(i, i) = p_i` (if using depth 1 cost for single node). *Note: The formula `cost(i, r-1) + cost(r+1, j) + W(i, j)` inherently calculates the total cost including depths.*
*   **Time Complexity:** O(n^3) (due to three nested loops: `l`, `i`, `r`). Can be optimized to O(n^2) using Knuth's optimization (based on properties of the root indices), but O(n^3) is standard.
*   **Space Complexity:** O(n^2) for storing cost and root tables.

### 7. Common Mistakes and Edge Cases

*   **Indexing:** Off-by-one errors are very common due to mapping between 0-based array indices and 1-based key indices/formulas. Be consistent.
*   **Base Cases:** Incorrectly handling empty subtrees (`cost(i, i-1)`) or single-node subtrees (`cost(i, i)`).
*   **Weight Calculation:** Forgetting to include the `W(i, j)` term or calculating it incorrectly (especially if including dummy node probabilities `q`).
*   **Loop Bounds:** Ensuring the loops for `l`, `i`, `j`, and `r` cover all required subproblems and potential roots correctly.
*   **Reconstruction:** The `root[i][j]` table stores the *index* `r` of the key `K[r]` that is the optimal root for the subtree `(i, j)`. Reconstructing the tree requires a recursive function using this table.

### 8. MCQ/Short Questions and Answers

1.  **Q:** What does the Optimal Binary Search Tree problem aim to minimize?
    **A:** The expected search cost in a Binary Search Tree, given key search probabilities.
2.  **Q:** What is the typical time complexity of the standard DP algorithm for OBST?
    **A:** O(n^3).
3.  **Q:** What does `W(i, j)` represent in the OBST recurrence relation?
    **A:** The sum of probabilities of all keys (and possibly dummy keys) within the range `i` to `j`. It represents the cost added at each level increase when this subtree is placed under a root.
4.  **Q:** If all key probabilities are equal, does the OBST necessarily look like a balanced BST?
    **A:** Yes, if only key probabilities `p_i` are considered and are equal, the OBST will tend to be balanced to minimize the average depth. If dummy probabilities `q_i` are significant and uneven, they can skew the tree.
5.  **Q:** What DP property is demonstrated by the fact that an optimal BST for keys `i..j` contains optimal BSTs for its left and right sub-ranges?
    **A:** Optimal Substructure.

---

## 5. 0/1 Knapsack Problem with Memory Functions (Memoization)

### 1. Concept Explanation

*   **What:** The 0/1 Knapsack problem involves selecting items from a set, each with a specific weight and value, to maximize the total value carried in a knapsack without exceeding its maximum weight capacity. The "0/1" means you can either take an entire item (1) or leave it behind (0) – you cannot take fractions of items.
*   **Why DP/Memoization:** A naive recursive approach explores taking or not taking each item, leading to exponential time complexity due to re-calculating the optimal value for the same remaining capacity and items. Memoization (a top-down DP technique) stores the results of these subproblems in a lookup table (e.g., a dictionary or array) to avoid re-computation.
*   **How (Recursive Structure):** Consider the `i`-th item with weight `w_i` and value `v_i`, and a remaining knapsack capacity `C`.
    *   **Base Cases:**
        *   If `i` reaches the end (no more items) or `C` becomes 0 or less, the value is 0.
    *   **Recursive Step:** For item `i`:
        1.  **Option 1: Don't take item `i`**. The maximum value is obtained by solving the problem for the remaining items (`i+1` onwards) with the same capacity `C`. -> `knapsack(i+1, C)`
        2.  **Option 2: Take item `i` (only if `w_i <= C`)**. The value is `v_i` plus the maximum value obtained by solving the problem for the remaining items (`i+1` onwards) with reduced capacity `C - w_i`. -> `v_i + knapsack(i+1, C - w_i)`
    *   **Decision:** Choose the option that yields the maximum value. `max(Option 1, Option 2)`
*   **Memoization:** Store the result of `knapsack(i, C)` in a table `memo[i][C]`. Before making recursive calls, check if `memo[i][C]` already has a computed value. If yes, return it directly. Otherwise, compute it, store it, and then return it.

### 2. Real-World Analogies and Use-Cases

*   **Analogy:** You're going on a hike (knapsack with capacity) and have various items (food, gear) each with a weight and a "usefulness" value. You want to pack the most useful combination without exceeding the weight limit.
*   **Use-Cases:** Resource allocation (allocating a fixed budget/time/resource to projects with different costs and returns), investment portfolio selection, cutting stock problems, cargo loading.

### 3. Step-by-Step Solved Example

**Problem:** Knapsack Capacity W = 5. Items (Weight, Value): Item 1 (2, 60), Item 2 (3, 100), Item 3 (4, 120).

**Memoization Approach:** Function `solve(index, capacity)`, Memo Table `memo[item_count+1][W+1]` initialized to -1 (or null).

1.  `solve(0, 5)`: Item 0 (2, 60). Capacity 5.
    *   `memo[0][5]` is -1. Compute.
    *   **Option 1 (Don't take Item 0):** `solve(1, 5)`
        *   `solve(1, 5)`: Item 1 (3, 100). Capacity 5. `memo[1][5]` is -1.
        *   **Option 1.1 (Don't take Item 1):** `solve(2, 5)`
            *   `solve(2, 5)`: Item 2 (4, 120). Capacity 5. `memo[2][5]` is -1.
            *   **Option 1.1.1 (Don't take Item 2):** `solve(3, 5)`. Index 3 is out of bounds. Return 0.
            *   **Option 1.1.2 (Take Item 2):** Weight 4 <= 5. `120 + solve(3, 5 - 4) = 120 + solve(3, 1)`. Index 3 out. Return 120 + 0 = 120.
            *   `solve(2, 5)` returns `max(0, 120) = 120`. Store `memo[2][5] = 120`.
        *   **Option 1.2 (Take Item 1):** Weight 3 <= 5. `100 + solve(2, 5 - 3) = 100 + solve(2, 2)`
            *   `solve(2, 2)`: Item 2 (4, 120). Capacity 2. `memo[2][2]` is -1.
            *   **Option 1.2.1 (Don't take Item 2):** `solve(3, 2)`. Index 3 out. Return 0.
            *   **Option 1.2.2 (Take Item 2):** Weight 4 > 2. Cannot take.
            *   `solve(2, 2)` returns `max(0, -inf) = 0`. Store `memo[2][2] = 0`.
        *   Option 1.2 value is `100 + 0 = 100`.
        *   `solve(1, 5)` returns `max(120, 100) = 120`. Store `memo[1][5] = 120`.
    *   **Option 2 (Take Item 0):** Weight 2 <= 5. `60 + solve(1, 5 - 2) = 60 + solve(1, 3)`
        *   `solve(1, 3)`: Item 1 (3, 100). Capacity 3. `memo[1][3]` is -1.
        *   **Option 2.1 (Don't take Item 1):** `solve(2, 3)`
            *   `solve(2, 3)`: Item 2 (4, 120). Capacity 3. `memo[2][3]` is -1.
            *   **Option 2.1.1 (Don't take Item 2):** `solve(3, 3)`. Return 0.
            *   **Option 2.1.2 (Take Item 2):** Weight 4 > 3. Cannot take.
            *   `solve(2, 3)` returns `max(0, -inf) = 0`. Store `memo[2][3] = 0`.
        *   **Option 2.2 (Take Item 1):** Weight 3 <= 3. `100 + solve(2, 3 - 3) = 100 + solve(2, 0)`
            *   `solve(2, 0)`: Capacity 0. Return 0. Store `memo[2][0] = 0`.
        *   Option 2.2 value is `100 + 0 = 100`.
        *   `solve(1, 3)` returns `max(0, 100) = 100`. Store `memo[1][3] = 100`.
    *   Option 2 value is `60 + 100 = 160`.
    *   `solve(0, 5)` returns `max(120, 160) = 160`. Store `memo[0][5] = 160`.

**Result:** Maximum value is 160. (Achieved by taking Item 0 (2, 60) and Item 1 (3, 100)).

**Memoization Table `memo` (relevant entries filled):**
```
      Cap=0 Cap=1 Cap=2 Cap=3 Cap=4 Cap=5
Idx=3 [  0 ] [  0 ] [  0 ] [  0 ] [  0 ] [  0 ] (Base case)
Idx=2 [  0 ] [  0 ] [  0 ] [  0 ] [ 120] [ 120] (Filled during calls)
Idx=1 [  - ] [  - ] [  - ] [ 100] [  - ] [ 120] (Filled during calls)
Idx=0 [  - ] [  - ] [  - ] [  - ] [  - ] [ 160] (Final result)
```
*(Note: Table size is (n+1) x (W+1). Indices map to item index and capacity. '-' means not computed/needed for this specific top-level call trace).*

### 4. Pseudocode and Code Implementation

**Pseudocode (Memoization):**

```pseudocode
// Global or class members:
// memo: 2D array/map initialized with a sentinel value (e.g., -1)
// weights: array of item weights
// values: array of item values
// n: number of items

function KnapsackMemo(index, capacity):
  // Base Cases
  if index >= n or capacity <= 0:
    return 0

  // Check memo table
  if memo[index][capacity] != -1:
    return memo[index][capacity]

  // Option 1: Don't take item 'index'
  value_without = KnapsackMemo(index + 1, capacity)

  // Option 2: Take item 'index' (if possible)
  value_with = -INFINITY // Or 0 if values are non-negative
  if weights[index] <= capacity:
    value_with = values[index] + KnapsackMemo(index + 1, capacity - weights[index])

  // Calculate result, store in memo, and return
  result = max(value_without, value_with)
  memo[index][capacity] = result
  return result

// Initial call: KnapsackMemo(0, MaxCapacity)
```

**Python Implementation:**

```python
def knapsack_memo_util(weights, values, capacity, index, memo):
    """Recursive helper for 0/1 Knapsack with memoization."""
    n = len(weights)

    # Base case: No items left or no capacity left
    if index == n or capacity <= 0:
        return 0

    # Check memoization table
    # Use tuple (index, capacity) as key for dictionary memo
    if (index, capacity) in memo:
        return memo[(index, capacity)]

    # Option 1: Exclude the current item
    value_without = knapsack_memo_util(weights, values, capacity, index + 1, memo)

    # Option 2: Include the current item (if it fits)
    value_with = 0 # Initialize to 0 since values are non-negative
    if weights[index] <= capacity:
        value_with = values[index] + knapsack_memo_util(weights, values,
                                                      capacity - weights[index],
                                                      index + 1, memo)

    # Store result in memo and return
    result = max(value_without, value_with)
    memo[(index, capacity)] = result
    return result

def knapsack_01_memo(weights, values, capacity):
    """Solves the 0/1 Knapsack problem using memoization."""
    memo = {} # Using a dictionary for sparse memoization table
    return knapsack_memo_util(weights, values, capacity, 0, memo)

# Example Usage:
w = [2, 3, 4]
v = [60, 100, 120]
W_cap = 5
max_val = knapsack_01_memo(w, v, W_cap)
print(f"Maximum value (Memoization): {max_val}") # Output: 160
```

**C++ Implementation:**

```c++
#include <vector>
#include <iostream>
#include <vector>
#include <map> // Or use a 2D vector initialized to -1

using namespace std;

// Using a 2D vector for memoization
vector<vector<int>> memo;
vector<int> weights_g;
vector<int> values_g;
int n_items;

int knapsack_memo_util(int index, int capacity) {
    // Base case
    if (index == n_items || capacity <= 0) {
        return 0;
    }

    // Check memo table
    if (memo[index][capacity] != -1) {
        return memo[index][capacity];
    }

    // Option 1: Exclude item
    int value_without = knapsack_memo_util(index + 1, capacity);

    // Option 2: Include item (if possible)
    int value_with = 0; // Initialize to 0 for non-negative values
    if (weights_g[index] <= capacity) {
        value_with = values_g[index] + knapsack_memo_util(index + 1, capacity - weights_g[index]);
    }

    // Store and return result
    memo[index][capacity] = max(value_without, value_with);
    return memo[index][capacity];
}

int knapsack_01_memo(const vector<int>& weights, const vector<int>& values, int capacity) {
    n_items = weights.size();
    if (n_items == 0 || capacity <= 0) return 0;

    // Initialize global variables / pass them around
    weights_g = weights;
    values_g = values;

    // Initialize memo table with -1 (sentinel value)
    memo.assign(n_items + 1, vector<int>(capacity + 1, -1));

    return knapsack_memo_util(0, capacity);
}

int main() {
    vector<int> w = {2, 3, 4};
    vector<int> v = {60, 100, 120};
    int W_cap = 5;
    int max_val = knapsack_01_memo(w, v, W_cap);
    cout << "Maximum value (Memoization): " << max_val << endl; // Output: 160
    return 0;
}
```

### 5. Diagrams or Flowcharts

**Recursion Tree (without memoization - showing overlapping subproblems):**

```
          KS(0, 5)
         /       \
      KS(1, 5)    KS(1, 3) + v0
     /     \       /     \
 KS(2, 5) KS(2, 2)+v1 KS(2, 3)+v1 KS(2, 0)+v1+v0
 /    \      |       |         |
KS(3,5) KS(3,1)+v2 KS(3,2)   KS(3,-1)+v2  ...
 |       |         |         |
 0       0         0         0
```
Notice how `KS(2, ...)` or `KS(3, ...)` with the same capacity might be called multiple times. Memoization prunes this tree by storing results.

**Memoization Table:** (See table in Step 3)

### 6. Key Formulas and Logic Summary

*   **Problem:** Maximize `Sum(v_i * x_i)` subject to `Sum(w_i * x_i) <= W`, where `x_i` is 0 or 1.
*   **Recursive Relation:**
    `Knapsack(i, C) = 0` if `i == n` or `C <= 0`
    `Knapsack(i, C) = Knapsack(i+1, C)` if `w_i > C` (cannot take item i)
    `Knapsack(i, C) = max( Knapsack(i+1, C), v_i + Knapsack(i+1, C - w_i) )` if `w_i <= C`
*   **Memoization:** Store results of `Knapsack(i, C)` in `memo[i][C]` to avoid re-computation.
*   **Time Complexity:** O(n * W), where n is the number of items and W is the capacity. Each state `(i, C)` is computed at most once.
*   **Space Complexity:** O(n * W) for the memoization table (plus recursion stack space, which can also be O(n*W) in worst case, but often less in practice).

### 7. Common Mistakes and Edge Cases

*   **Base Cases:** Incorrectly handling the end of items (`i == n`) or zero capacity (`C <= 0`).
*   **Memoization Check:** Forgetting to check the memo table *before* making recursive calls.
*   **Memoization Store:** Forgetting to store the computed result *before* returning it.
*   **State Definition:** Using incorrect state variables (e.g., forgetting the item index `i`). The state must uniquely identify a subproblem.
*   **Capacity Check:** Incorrectly checking if an item fits (`weights[index] <= capacity`).
*   **Tabulation vs. Memoization:** Confusing the top-down memoized recursion with the bottom-up iterative tabulation approach (which also achieves O(n*W)).

### 8. MCQ/Short Questions and Answers

1.  **Q:** What does "0/1" signify in the 0/1 Knapsack problem?
    **A:** You must either take an item entirely or leave it entirely; no fractions allowed.
2.  **Q:** What is the time complexity of the 0/1 Knapsack solution using memoization (or tabulation)?
    **A:** O(n * W), where n is the number of items and W is the capacity.
3.  **Q:** What are the two choices considered for each item in the recursive formulation?
    **A:** Either exclude the item or include the item (if it fits within the remaining capacity).
4.  **Q:** How does memoization improve the efficiency of the recursive solution?
    **A:** By storing the results of already solved subproblems (defined by item index and remaining capacity) and reusing them, avoiding exponential redundant calculations.
5.  **Q:** Is the O(n*W) complexity polynomial?
    **A:** It is pseudo-polynomial time because the complexity depends on the *magnitude* of the input parameter W (the capacity), not just the *size* of the input (number of items n). If W can be exponentially large relative to n, the algorithm is not truly polynomial.

---

## 6. Matrix-Chain Multiplication (MCM)

### 1. Concept Explanation

*   **What:** Given a sequence (chain) of matrices `A1, A2, ..., An`, where matrix `Ai` has dimensions `p_{i-1} x p_i`, the Matrix-Chain Multiplication problem is to find the most efficient way (minimum number of scalar multiplications) to multiply the entire chain. The order of multiplication matters significantly, but the final result matrix is the same.
*   **Why DP:** Multiplying `(A1 * A2) * A3` can have a very different cost than `A1 * (A2 * A3)`. The problem has optimal substructure: the optimal way to multiply `Ai * ... * Aj` involves splitting it into `(Ai * ... * Ak) * (Ak+1 * ... * Aj)` for some `k`, where the parenthesizations of the two sub-chains must also be optimal. It also has overlapping subproblems, as the optimal cost for multiplying a sub-chain like `A2 * A3 * A4` might be needed when computing `A1*..*A4` and `A2*..*A5`.
*   **How:** Let `m[i][j]` be the minimum number of scalar multiplications needed to compute the product `Ai * ... * Aj`.
    *   **Base Case:** `m[i][i] = 0` (cost of multiplying a single matrix is 0).
    *   **Recursive Step:** To compute `m[i][j]`, we consider all possible places `k` to split the chain (`i <= k < j`), i.e., `(Ai * ... * Ak) * (Ak+1 * ... * Aj)`.
        The cost for a given split `k` is: `cost(Ai..Ak) + cost(Ak+1..Aj) + cost_of_multiplying_results`.
        The result of `Ai..Ak` is a `p_{i-1} x p_k` matrix.
        The result of `Ak+1..Aj` is a `p_k x p_j` matrix.
        Multiplying these two results costs `p_{i-1} * p_k * p_j` scalar multiplications.
        So, `m[i][j] = min_{i <= k < j} { m[i][k] + m[k+1][j] + p_{i-1} * p_k * p_j }`.
*   **Dimensions:** The input is usually given as an array `p` of dimensions, where `Ai` is `p[i-1] x p[i]`. For `n` matrices, the array `p` has size `n+1`.

### 2. Real-World Analogies and Use-Cases

*   **Analogy:** Planning a series of tasks where the output of one task is the input to the next, and combining intermediate results has different costs. You want to find the cheapest order to combine them. (e.g., merging sorted lists of different sizes).
*   **Use-Cases:** Primarily optimizing sequences of matrix multiplications in scientific computing, graphics (transformations), and database query optimization (join order). The DP technique itself is widely applicable.

### 3. Step-by-Step Solved Example

**Problem:** Find the minimum cost to multiply matrices A1, A2, A3, A4 with dimensions given by `p = {10, 20, 50, 1, 100}`.
*   A1: 10x20 (p0 x p1)
*   A2: 20x50 (p1 x p2)
*   A3: 50x1  (p2 x p3)
*   A4: 1x100 (p3 x p4)

**DP Table `m[n+1][n+1]` (using 1-based indexing):** `m[i][j]` = min cost for `Ai...Aj`.
Initialize `m[i][i] = 0`.

**Length l = 2 (Multiplying pairs):**
*   `m[1][2]` (A1*A2): Split k=1. `m[1][1] + m[2][2] + p0*p1*p2 = 0 + 0 + 10*20*50 = 10000`.
*   `m[2][3]` (A2*A3): Split k=2. `m[2][2] + m[3][3] + p1*p2*p3 = 0 + 0 + 20*50*1 = 1000`.
*   `m[3][4]` (A3*A4): Split k=3. `m[3][3] + m[4][4] + p2*p3*p4 = 0 + 0 + 50*1*100 = 5000`.

**Length l = 3 (Multiplying triples):**
*   `m[1][3]` (A1*A2*A3):
    *   Split k=1: (A1) * (A2*A3). Cost = `m[1][1] + m[2][3] + p0*p1*p3 = 0 + 1000 + 10*20*1 = 1000 + 200 = 1200`.
    *   Split k=2: (A1*A2) * (A3). Cost = `m[1][2] + m[3][3] + p0*p2*p3 = 10000 + 0 + 10*50*1 = 10000 + 500 = 10500`.
    *   `m[1][3] = min(1200, 10500) = 1200`. (Optimal split: A1*(A2*A3))
*   `m[2][4]` (A2*A3*A4):
    *   Split k=2: (A2) * (A3*A4). Cost = `m[2][2] + m[3][4] + p1*p2*p4 = 0 + 5000 + 20*50*100 = 5000 + 100000 = 105000`.
    *   Split k=3: (A2*A3) * (A4). Cost = `m[2][3] + m[4][4] + p1*p3*p4 = 1000 + 0 + 20*1*100 = 1000 + 2000 = 3000`.
    *   `m[2][4] = min(105000, 3000) = 3000`. (Optimal split: (A2*A3)*A4)

**Length l = 4 (Multiplying all four):**
*   `m[1][4]` (A1*A2*A3*A4):
    *   Split k=1: (A1) * (A2*A3*A4). Cost = `m[1][1] + m[2][4] + p0*p1*p4 = 0 + 3000 + 10*20*100 = 3000 + 20000 = 23000`.
    *   Split k=2: (A1*A2) * (A3*A4). Cost = `m[1][2] + m[3][4] + p0*p2*p4 = 10000 + 5000 + 10*50*100 = 15000 + 50000 = 65000`.
    *   Split k=3: (A1*A2*A3) * (A4). Cost = `m[1][3] + m[4][4] + p0*p3*p4 = 1200 + 0 + 10*1*100 = 1200 + 1000 = 2200`.
    *   `m[1][4] = min(23000, 65000, 2200) = 2200`. (Optimal split: (A1*(A2*A3))*A4)

**Result:** Minimum cost is 2200 scalar multiplications.
The optimal parenthesization is (A1 * (A2 * A3)) * A4. (We need a separate table `s[i][j]` to store the optimal split `k` for each `m[i][j]` to reconstruct this).

### 4. Pseudocode and Code Implementation

**Pseudocode:**

```pseudocode
function MatrixChainOrder(p): // p is array of dimensions p[0...n] for n matrices
  n = length(p) - 1 // Number of matrices
  // m[i][j] = min cost to compute Ai...Aj
  m = new array[n+1][n+1]
  // s[i][j] = index k that achieved min cost for m[i][j] (for reconstruction)
  s = new array[n+1][n+1]

  // Base case: cost is 0 for single matrix
  for i from 1 to n:
    m[i][i] = 0

  // Compute cost for chains of length l = 2 to n
  for l from 2 to n: // l is chain length
    for i from 1 to n - l + 1:
      j = i + l - 1
      m[i][j] = INFINITY
      for k from i to j - 1: // k is split point: (Ai..Ak)*(Ak+1..Aj)
        // Cost = cost(left) + cost(right) + cost(multiply results)
        cost = m[i][k] + m[k+1][j] + p[i-1] * p[k] * p[j]
        if cost < m[i][j]:
          m[i][j] = cost
          s[i][j] = k // Store the best split point

  return m[1][n], s // Min cost and split table
```

**Python Implementation:**

```python
import sys

def matrix_chain_order(p):
    """
    Finds the minimum cost for matrix chain multiplication.
    Args:
        p: List of dimensions, where matrix A_i has dimension p[i-1] x p[i].
           Length of p is n+1 for n matrices.
    Returns:
        A tuple: (minimum cost, split table s for reconstruction).
    """
    n = len(p) - 1 # Number of matrices
    if n <= 0:
        return 0, []

    # m[i][j] = min cost for chain A[i]...A[j] (using 1-based index conceptually)
    # Use 0-based indexing for arrays m and s, mapping i->i-1, j->j-1
    m = [[0] * n for _ in range(n)]
    s = [[0] * n for _ in range(n)] # s[i][j] stores k for split

    # l is chain length
    for length in range(2, n + 1):
        for i in range(n - length + 1):
            j = i + length - 1
            m[i][j] = sys.maxsize # Initialize with infinity

            for k in range(i, j): # k is the split index (0-based)
                # Cost = m[i][k] + m[k+1][j] + p[i]*p[k+1]*p[j+1]
                # Indices map: p_idx = array_idx + 1
                # p[i-1] -> p[i]
                # p[k]   -> p[k+1]
                # p[j]   -> p[j+1]
                cost = m[i][k] + m[k+1][j] + p[i] * p[k+1] * p[j+1]

                if cost < m[i][j]:
                    m[i][j] = cost
                    s[i][j] = k # Store the best split index (0-based)

    return m[0][n-1], s # Return min cost and split table

# Function to print optimal parenthesis (using s table)
def print_optimal_parens(s, i, j):
    if i == j:
        print(f"A{i+1}", end="")
    else:
        print("(", end="")
        # k is 0-based index, add 1 for matrix number
        split_k = s[i][j]
        print_optimal_parens(s, i, split_k)
        print_optimal_parens(s, split_k + 1, j)
        print(")", end="")

# Example Usage:
p_dims = [10, 20, 50, 1, 100]
min_cost, split_table = matrix_chain_order(p_dims)
print(f"Minimum number of multiplications: {min_cost}") # Output: 2200

print("Optimal Parenthesization: ", end="")
print_optimal_parens(split_table, 0, len(p_dims) - 2) # Indices 0 to n-1
print() # Output: (A1(A2A3))A4) - Check logic, should be ((A1(A2A3))A4)
# Let's re-trace the optimal splits from example:
# m[1][4] min cost came from k=3. Split: (A1 A2 A3) * (A4). s[0][3] = 2 (0-based index for k=3)
# m[1][3] min cost came from k=1. Split: (A1) * (A2 A3). s[0][2] = 0 (0-based index for k=1)
# m[2][3] min cost came from k=2. Split: (A2) * (A3). s[1][2] = 1 (0-based index for k=2)

# Reconstruction trace:
# print_optimal_parens(s, 0, 3) -> i=0, j=3
#   print "("
#   k = s[0][3] = 2
#   print_optimal_parens(s, 0, 2) -> i=0, j=2
#     print "("
#     k = s[0][2] = 0
#     print_optimal_parens(s, 0, 0) -> print "A1"
#     print_optimal_parens(s, 1, 2) -> i=1, j=2
#       print "("
#       k = s[1][2] = 1
#       print_optimal_parens(s, 1, 1) -> print "A2"
#       print_optimal_parens(s, 2, 2) -> print "A3"
#       print ")" -> Output: (A2A3)
#     print ")" -> Output: (A1(A2A3))
#   print_optimal_parens(s, 3, 3) -> print "A4"
#   print ")" -> Output: ((A1(A2A3))A4) - Correct!
```

**C++ Implementation:**

```c++
#include <vector>
#include <iostream>
#include <limits>    // For std::numeric_limits
#include <algorithm> // For std::min
#include <string>

using namespace std;

// Pair to return cost and split table
using MatrixChainResult = pair<long long, vector<vector<int>>>;

MatrixChainResult matrix_chain_order_cpp(const vector<int>& p) {
    int n = p.size() - 1; // Number of matrices
    if (n <= 0) {
        return {0, {}};
    }

    // m[i][j] = min cost for chain A[i]...A[j] (1-based index conceptually)
    vector<vector<long long>> m(n + 1, vector<long long>(n + 1, 0));
    // s[i][j] stores k for split (1-based index)
    vector<vector<int>> s(n + 1, vector<int>(n + 1, 0));

    // l is chain length
    for (int length = 2; length <= n; ++length) {
        for (int i = 1; i <= n - length + 1; ++i) {
            int j = i + length - 1;
            m[i][j] = numeric_limits<long long>::max(); // Initialize with infinity

            for (int k = i; k < j; ++k) { // k is the split point (1-based)
                // Cost = m[i][k] + m[k+1][j] + p[i-1]*p[k]*p[j]
                long long cost = m[i][k] + m[k + 1][j] + (long long)p[i - 1] * p[k] * p[j];

                if (cost < m[i][j]) {
                    m[i][j] = cost;
                    s[i][j] = k; // Store the best split point (1-based)
                }
            }
        }
    }

    return {m[1][n], s}; // Return min cost and split table
}

// Function to print optimal parenthesis (using s table, 1-based)
void print_optimal_parens_cpp(const vector<vector<int>>& s, int i, int j) {
    if (i == j) {
        cout << "A" << i;
    } else {
        cout << "(";
        int k = s[i][j];
        print_optimal_parens_cpp(s, i, k);
        print_optimal_parens_cpp(s, k + 1, j);
        cout << ")";
    }
}


int main() {
    vector<int> p_dims = {10, 20, 50, 1, 100}; // A1(10x20), A2(20x50), A3(50x1), A4(1x100)
    int n_matrices = p_dims.size() - 1;

    MatrixChainResult result = matrix_chain_order_cpp(p_dims);
    long long min_cost = result.first;
    vector<vector<int>> split_table = result.second;

    cout << "Minimum number of multiplications: " << min_cost << endl; // Output: 2200

    cout << "Optimal Parenthesization: ";
    print_optimal_parens_cpp(split_table, 1, n_matrices); // Use 1-based indices
    cout << endl; // Output: ((A1(A2A3))A4)

    return 0;
}
```

### 5. Diagrams or Flowcharts

**DP Table `m[i][j]` Filling Order:** (Same as OBST)

```
j=1  j=2  j=3  j=4 ... j=n
i=1 [ 0 ] [L=2] [L=3] [L=4] ... [ L=n ]
i=2      [ 0 ] [L=2] [L=3] ... [L=n-1]
i=3           [ 0 ] [L=2] ... [L=n-2]
...                ...
i=n                     [ 0 ]
```
Fill along diagonals, starting from main diagonal (Length L=1, cost 0) upwards/rightwards to the top-right corner `m[1][n]`.

**Example `m` and `s` tables (1-based indexing):**

`m` table:
```
   j=1 j=2   j=3   j=4
i=1[ 0  10000  1200  2200 ]
i=2[ -   0    1000  3000 ]
i=3[ -   -    0    5000 ]
i=4[ -   -    -    0    ]
```

`s` table (stores optimal `k`):
```
   j=1 j=2 j=3 j=4
i=1[ -   1   1   3  ]  <- s[1][3]=1 means A1*(A2*A3), s[1][4]=3 means (A1*A2*A3)*A4
i=2[ -   -   2   3  ]  <- s[2][4]=3 means (A2*A3)*A4
i=3[ -   -   -   3  ]
i=4[ -   -   -   -  ]
```

### 6. Key Formulas and Logic Summary

*   **Goal:** Find minimum scalar multiplications for `A1 * A2 * ... * An`.
*   **Input:** Dimension array `p[0...n]` where `Ai` is `p[i-1] x p[i]`.
*   **Recurrence:** `m[i][j] = min_{i <= k < j} { m[i][k] + m[k+1][j] + p[i-1] * p[k] * p[j] }` for `i < j`.
*   **Base Case:** `m[i][i] = 0`.
*   **Time Complexity:** O(n^3) (three nested loops: `l`, `i`, `k`).
*   **Space Complexity:** O(n^2) for storing the `m` and `s` tables.

### 7. Common Mistakes and Edge Cases

*   **Indexing:** Very prone to off-by-one errors with the dimension array `p` and the matrix indices `i, j, k`. Using 1-based indexing conceptually often helps align with formulas, but implementation might use 0-based arrays requiring careful mapping.
*   **Dimension Lookups:** Using the wrong indices from `p` when calculating the cost `p[i-1] * p[k] * p[j]`. Remember `p[i-1]` is rows of `Ai`, `p[k]` is cols of `Ak` (and rows of `Ak+1`), `p[j]` is cols of `Aj`.
*   **Loop Bounds:** Incorrect bounds for `l`, `i`, `j`, or `k`. `k` must go from `i` to `j-1`.
*   **Base Cases:** Forgetting `m[i][i] = 0`.
*   **Reconstruction:** Incorrectly using the `s` table or writing the recursive reconstruction function.

### 8. MCQ/Short Questions and Answers

1.  **Q:** Why is the order of multiplication important in matrix chains?
    **A:** Because matrix multiplication is associative but not commutative, and different multiplication orders lead to the same result but can have vastly different numbers of scalar multiplications (computational cost).
2.  **Q:** What is the time complexity of the standard DP algorithm for Matrix Chain Multiplication?
    **A:** O(n^3).
3.  **Q:** If matrix A is `p x q` and matrix B is `q x r`, how many scalar multiplications are needed to compute A * B?
    **A:** `p * q * r`.
4.  **Q:** What does `m[i][j]` typically store in the MCM DP table?
    **A:** The minimum cost (scalar multiplications) required to compute the product of matrices `Ai` through `Aj`.
5.  **Q:** What information is needed besides the cost table (`m`) to reconstruct the optimal multiplication order?
    **A:** A second table (`s`) that stores the optimal split point `k` for each subproblem `m[i][j]`.

---

## 7. Longest Common Subsequence (LCS)

### 1. Concept Explanation

*   **What:** Given two sequences (e.g., strings) X and Y, the Longest Common Subsequence (LCS) problem is to find the longest subsequence that is common to both X and Y. A subsequence is derived from a sequence by deleting zero or more elements, without changing the order of the remaining elements.
*   **Example:** X = "ABCBDAB", Y = "BDCAB". LCS is "BCAB" (length 4). Other common subsequences: "BCB", "BDB", "BAB".
*   **Why DP:** The problem has optimal substructure. Let `LCS(X_i, Y_j)` denote the LCS of prefixes `X[1..i]` and `Y[1..j]`.
    *   If the last characters match (`X[i] == Y[j]`), then the LCS must include this character. The length is `1 + length(LCS(X_{i-1}, Y_{j-1}))`.
    *   If the last characters don't match (`X[i] != Y[j]`), then the LCS is the longer of the LCS of `X_{i-1}, Y_j` and the LCS of `X_i, Y_{j-1}`.
    It also has overlapping subproblems, as `LCS(X_k, Y_l)` might be needed multiple times.
*   **How:** We use a 2D table `dp[m+1][n+1]` where `m = len(X)` and `n = len(Y)`. `dp[i][j]` stores the *length* of the LCS of `X[1..i]` and `Y[1..j]`.
    *   **Base Cases:** `dp[i][0] = 0` for all `i`, `dp[0][j] = 0` for all `j` (LCS with an empty string is empty).
    *   **Recurrence:**
        *   If `X[i-1] == Y[j-1]` (using 0-based string indexing): `dp[i][j] = 1 + dp[i-1][j-1]`
        *   If `X[i-1] != Y[j-1]`: `dp[i][j] = max(dp[i-1][j], dp[i][j-1])`

### 2. Real-World Analogies and Use-Cases

*   **Analogy:** Comparing two versions of a document (like using `diff` utility). The LCS represents the parts that haven't changed between versions. The parts *not* in the LCS are the additions/deletions.
*   **Use-Cases:**
    *   **Bioinformatics:** Comparing DNA or protein sequences to find similarities (indicating evolutionary relationships or functional similarities).
    *   **Version Control:** File comparison (e.g., `diff` in Git/SVN).
    *   **Plagiarism Detection:** Finding long common subsequences between documents.
    *   **Data Compression:** Used in some compression algorithms.
    *   **Spell Checking/String Similarity:** Related to edit distance.

### 3. Step-by-Step Solved Example

**Problem:** Find the length of the LCS for X = "ABCBDAB" and Y = "BDCAB".

**DP Table `dp[m+1][n+1]` (m=7, n=5):** `dp[i][j]` = LCS length for `X[0..i-1]` and `Y[0..j-1]`.

Initialize row 0 and column 0 to 0.

```
      "" B  D  C  A  B  (Y)
    j=0 1  2  3  4  5
"" i=0 [0  0  0  0  0  0]
A  i=1 [0  0  0  0  1  1]  (X[0]=A == Y[3]=A) -> 1+dp[0][3]=1. max(dp[0][j], dp[1][j-1])
B  i=2 [0  1  1  1  1  2]  (X[1]=B == Y[0]=B) -> 1+dp[1][0]=1. (X[1]=B == Y[4]=B) -> 1+dp[1][4]=1+1=2. max(...)
C  i=3 [0  1  1  2  2  2]  (X[2]=C == Y[2]=C) -> 1+dp[2][2]=1+1=2. max(...)
B  i=4 [0  1  2  2  2  3]  (X[3]=B == Y[0]=B) -> 1+dp[3][0]=1. (X[3]=B == Y[4]=B) -> 1+dp[3][4]=1+2=3. max(...)
D  i=5 [0  1  2  2  3  3]  (X[4]=D == Y[1]=D) -> 1+dp[4][1]=1+1=2. max(...)
A  i=6 [0  1  2  2  3  3]  (X[5]=A == Y[3]=A) -> 1+dp[5][3]=1+2=3. max(...)
B  i=7 [0  1  2  2  3  4]  (X[6]=B == Y[0]=B) -> 1+dp[6][0]=1. (X[6]=B == Y[4]=B) -> 1+dp[6][4]=1+3=4. max(...)
(X)
```

**Filling Explanation (Example: dp[7][5]):**
*   Compare `X[6]` ('B') and `Y[4]` ('B'). They match.
*   `dp[7][5] = 1 + dp[6][4]`
*   Look up `dp[6][4]`. Compare `X[5]` ('A') and `Y[3]` ('A'). They match.
*   `dp[6][4] = 1 + dp[5][3]`
*   Look up `dp[5][3]`. Compare `X[4]` ('D') and `Y[2]` ('C'). No match.
*   `dp[5][3] = max(dp[4][3], dp[5][2])`
    *   `dp[4][3]`: Compare `X[3]` ('B') and `Y[2]` ('C'). No match. `max(dp[3][3], dp[4][2]) = max(2, 2) = 2`.
    *   `dp[5][2]`: Compare `X[4]` ('D') and `Y[1]` ('D'). Match. `1 + dp[4][1] = 1 + 1 = 2`.
*   So, `dp[5][3] = max(2, 2) = 2`.
*   Backtrack: `dp[6][4] = 1 + dp[5][3] = 1 + 2 = 3`.
*   Backtrack: `dp[7][5] = 1 + dp[6][4] = 1 + 3 = 4`.

**Result:** The length of the LCS is `dp[m][n] = dp[7][5] = 4`.

**Reconstructing the LCS:** Start from `dp[m][n]` and trace back:
*   `dp[7][5]`: `X[6]=='B'`, `Y[4]=='B'`. Match! Add 'B' to LCS. Move to `dp[6][4]`. LCS = "B".
*   `dp[6][4]`: `X[5]=='A'`, `Y[3]=='A'`. Match! Add 'A' to LCS. Move to `dp[5][3]`. LCS = "AB".
*   `dp[5][3]`: `X[4]=='D'`, `Y[2]=='C'`. No match. `dp[4][3]=2`, `dp[5][2]=2`. Choose either (e.g., move up). Move to `dp[4][3]`.
*   `dp[4][3]`: `X[3]=='B'`, `Y[2]=='C'`. No match. `dp[3][3]=2`, `dp[4][2]=2`. Choose either (e.g., move up). Move to `dp[3][3]`.
*   `dp[3][3]`: `X[2]=='C'`, `Y[2]=='C'`. Match! Add 'C' to LCS. Move to `dp[2][2]`. LCS = "CAB".
*   `dp[2][2]`: `X[1]=='B'`, `Y[1]=='D'`. No match. `dp[1][2]=1`, `dp[2][1]=1`. Choose either (e.g., move left). Move to `dp[2][1]`.
*   `dp[2][1]`: `X[1]=='B'`, `Y[0]=='B'`. Match! Add 'B' to LCS. Move to `dp[1][0]`. LCS = "BCAB".
*   `dp[1][0]` is 0. Stop.

Reverse the constructed LCS: "BCAB".

### 4. Pseudocode and Code Implementation

**Pseudocode (Length Calculation):**

```pseudocode
function LCS_Length(X, Y):
  m = length(X)
  n = length(Y)
  // dp[i][j] stores length of LCS for X[0..i-1] and Y[0..j-1]
  dp = new array[m+1][n+1]

  // Initialize base cases (row 0 and column 0)
  for i from 0 to m: dp[i][0] = 0
  for j from 0 to n: dp[0][j] = 0

  // Fill the dp table
  for i from 1 to m:
    for j from 1 to n:
      if X[i-1] == Y[j-1]: // Using 0-based indexing for strings
        dp[i][j] = 1 + dp[i-1][j-1]
      else:
        dp[i][j] = max(dp[i-1][j], dp[i][j-1])

  return dp[m][n] // Length of LCS is in the bottom-right cell
```

**Python Implementation (Length and Reconstruction):**

```python
def lcs(X, Y):
    """
    Computes the length and the LCS string itself.
    Args:
        X: First string.
        Y: Second string.
    Returns:
        A tuple: (length of LCS, the LCS string).
    """
    m = len(X)
    n = len(Y)
    # dp table stores lengths
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    # Fill dp table
    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if X[i - 1] == Y[j - 1]:
                dp[i][j] = 1 + dp[i - 1][j - 1]
            else:
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1])

    lcs_length = dp[m][n]

    # Reconstruct LCS string by backtracking
    lcs_str = [""] * lcs_length
    index = lcs_length - 1
    i, j = m, n
    while i > 0 and j > 0:
        # If chars match, it's part of LCS
        if X[i - 1] == Y[j - 1]:
            lcs_str[index] = X[i - 1]
            i -= 1
            j -= 1
            index -= 1
        # If not match, move in direction of the larger subproblem length
        elif dp[i - 1][j] > dp[i][j - 1]:
            i -= 1
        else: # dp[i][j-1] >= dp[i-1][j]
            j -= 1

    return lcs_length, "".join(lcs_str)

# Example Usage:
X_str = "ABCBDAB"
Y_str = "BDCAB"
length, sequence = lcs(X_str, Y_str)
print(f"LCS Length: {length}")     # Output: 4
print(f"LCS Sequence: {sequence}") # Output: BCAB
```

**C++ Implementation (Length and Reconstruction):**

```c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm> // For std::max, std::reverse

using namespace std;

pair<int, string> find_lcs(const string& X, const string& Y) {
    int m = X.length();
    int n = Y.length();

    // dp table stores lengths
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));

    // Fill dp table
    for (int i = 1; i <= m; ++i) {
        for (int j = 1; j <= n; ++j) {
            if (X[i - 1] == Y[j - 1]) {
                dp[i][j] = 1 + dp[i - 1][j - 1];
            } else {
                dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
    }

    int lcs_length = dp[m][n];

    // Reconstruct LCS string
    string lcs_str = "";
    int i = m, j = n;
    while (i > 0 && j > 0) {
        if (X[i - 1] == Y[j - 1]) {
            lcs_str += X[i - 1]; // Append character
            i--;
            j--;
        } else if (dp[i - 1][j] > dp[i][j - 1]) {
            i--;
        } else {
            j--;
        }
    }
    reverse(lcs_str.begin(), lcs_str.end()); // Reverse to get correct order

    return {lcs_length, lcs_str};
}

int main() {
    string X_str = "ABCBDAB";
    string Y_str = "BDCAB";
    pair<int, string> result = find_lcs(X_str, Y_str);
    cout << "LCS Length: " << result.first << endl;     // Output: 4
    cout << "LCS Sequence: " << result.second << endl; // Output: BCAB
    return 0;
}
```

### 5. Diagrams or Flowcharts

**DP Table:** (See table in Step 3)

**Backtracking Path for Reconstruction (Arrows indicate movement):**

```
      "" B  D  C  A  B
    j=0 1  2  3  4  5
"" i=0 [0  0  0  0  0  0]
A  i=1 [0  0  0  0  1  1]
B  i=2 [0 <1< 1 <1< 1 <2]  <- Match B (dp[2][1])
C  i=3 [0  1  1 <2< 2  2]  <- Match C (dp[3][3])
B  i=4 [0  1 <2< 2  2 <3]
D  i=5 [0  1  2 <2< 3  3]
A  i=6 [0  1  2  2 <3< 3]  <- Match A (dp[6][4])
B  i=7 [0  1  2  2  3 <4]  <- Match B (dp[7][5])
                     ^
                     Start Here
```
Follow arrows indicating matches (diagonal up-left) or moves up/left based on max value.

### 6. Key Formulas and Logic Summary

*   **Goal:** Find the longest subsequence common to sequences X and Y.
*   **Recurrence (Length):**
    *   `dp[i][j] = 1 + dp[i-1][j-1]` if `X[i-1] == Y[j-1]`
    *   `dp[i][j] = max(dp[i-1][j], dp[i][j-1])` if `X[i-1] != Y[j-1]`
*   **Base Cases:** `dp[i][0] = 0`, `dp[0][j] = 0`.
*   **Time Complexity:** O(m * n), where m and n are the lengths of the sequences.
*   **Space Complexity:** O(m * n) for the DP table. (Can be optimized to O(min(m, n)) if only length is needed, by storing only the previous row/column).

### 7. Common Mistakes and Edge Cases

*   **Indexing:** Off-by-one errors when accessing string characters (`X[i-1]`, `Y[j-1]`) relative to DP table indices (`i`, `j`).
*   **Base Cases:** Incorrect initialization of the first row and column.
*   **Reconstruction:** Errors in the backtracking logic (e.g., moving incorrectly when characters don't match, forgetting to add matched characters, not reversing the final string).
*   **Max Function:** Correctly taking the max of the two adjacent cells when characters don't match.
*   **Empty Strings:** Handling cases where one or both input strings are empty (correctly handled by base cases).

### 8. MCQ/Short Questions and Answers

1.  **Q:** What is a subsequence?
    **A:** A sequence derived from another by deleting zero or more elements without changing the order of the remaining elements.
2.  **Q:** What is the time complexity of the standard DP algorithm for LCS?
    **A:** O(m * n).
3.  **Q:** What does `dp[i][j]` store in the LCS DP table?
    **A:** The length of the Longest Common Subsequence between the first `i` characters of X and the first `j` characters of Y.
4.  **Q:** How do you reconstruct the actual LCS string after filling the DP table?
    **A:** By backtracking from `dp[m][n]`, following the choices made (diagonal if characters matched, up or left if they didn't) and collecting the matched characters.
5.  **Q:** Can the space complexity for finding just the *length* of the LCS be optimized?
    **A:** Yes, to O(min(m, n)) by only keeping track of the current and previous rows (or columns) of the DP table.

---

**Introduction to Greedy Techniques**

*   **Concept:** Greedy algorithms build up a solution piece by piece, always choosing the option that looks best (most profitable, lowest cost, etc.) at the current moment, without regard for future consequences. They make a *locally optimal* choice hoping it will lead to a *globally optimal* solution.
*   **Characteristics:**
    *   **Greedy Choice Property:** A globally optimal solution can be arrived at by making locally optimal (greedy) choices.
    *   **Optimal Substructure:** An optimal solution to the problem contains optimal solutions to its subproblems (similar to DP, but the way subproblems are constructed differs).
*   **Difference from DP:** DP typically explores multiple options for subproblems and chooses the best one later. Greedy makes one choice and sticks with it, never reconsidering. DP is often needed when a greedy choice might prevent reaching the true global optimum later.
*   **Analogy:** Giving change using the fewest coins. You greedily pick the largest denomination coin (e.g., quarter) that is less than or equal to the remaining amount, then repeat with the new remaining amount. This works for standard US currency but not all currency systems.
*   **Use-Cases:** Minimum Spanning Trees (Prim's, Kruskal's), Shortest Path (Dijkstra's), Huffman Coding, Activity Selection, Fractional Knapsack.

---

## 8. Graph Algorithms: Minimum Spanning Trees (MST)

### 1. Concept Explanation

*   **What:** Given a connected, undirected, weighted graph, a Minimum Spanning Tree (MST) is a subgraph that connects all vertices together (it's a tree, so no cycles) with the minimum possible total edge weight.
*   **Why Greedy:** MST algorithms like Prim's and Kruskal's use greedy approaches. They iteratively add the "safest" or "cheapest" edge that doesn't violate the tree property (i.e., doesn't form a cycle).
*   **Cut Property (Basis for Greedy MST):** For any cut (a partition of the graph's vertices into two disjoint sets), if an edge `(u, v)` has the minimum weight among all edges crossing the cut, then this edge must belong to *some* MST of the graph. Both Prim's and Kruskal's implicitly use this property.

### 2. Real-World Analogies and Use-Cases

*   **Analogy:** Designing a network (e.g., electrical grid, computer network, plumbing) to connect several points (cities, houses, components) using the minimum amount of cable/pipe (minimum total edge weight).
*   **Use-Cases:**
    *   Network design (telecommunications, transportation, water supply).
    *   Cluster analysis (finding clusters based on minimum connection costs).
    *   Image segmentation.
    *   Approximation algorithms for other problems (like TSP).

### 3. Step-by-Step Solved Example

*(Specific examples will be shown under Prim's and Kruskal's algorithms below).*

### 4. Pseudocode and Code Implementation

*(See Prim's and Kruskal's sections).*

### 5. Diagrams or Flowcharts

*(See Prim's and Kruskal's sections).*

### 6. Key Formulas and Logic Summary

*   **Goal:** Find a spanning tree T of graph G=(V, E) such that the sum of edge weights in T is minimized.
*   **Properties:**
    *   Connects all |V| vertices.
    *   Contains exactly |V| - 1 edges.
    *   Is acyclic.
*   **Greedy Strategy:** Iteratively add the minimum weight edge that connects a new vertex (Prim's) or connects two previously unconnected components (Kruskal's) without forming a cycle.

### 7. Common Mistakes and Edge Cases

*   **Disconnected Graphs:** MST is only defined for connected graphs. If the graph is disconnected, algorithms find a Minimum Spanning Forest (a collection of MSTs, one for each connected component).
*   **Cycles:** Ensuring the added edge does not create a cycle is crucial.
*   **Negative Weights:** MST algorithms generally work correctly with negative edge weights (unlike some shortest path algorithms).
*   **Multiple Edges with Same Weight:** There can be multiple MSTs if edge weights are not unique. The algorithms will find one of them.

### 8. MCQ/Short Questions and Answers

1.  **Q:** What is a Spanning Tree?
    **A:** A subgraph of a connected graph G that includes all vertices of G and is a tree (connected, acyclic).
2.  **Q:** What is a Minimum Spanning Tree (MST)?
    **A:** A spanning tree with the minimum possible total edge weight.
3.  **Q:** How many edges are in an MST of a graph with |V| vertices?
    **A:** |V| - 1 edges.
4.  **Q:** Name two common greedy algorithms for finding MSTs.
    **A:** Prim's Algorithm and Kruskal's Algorithm.
5.  **Q:** Does adding the globally cheapest edge always work for MST?
    **A:** Not necessarily adding *just* the cheapest edge. Kruskal's adds the cheapest available edge *that doesn't form a cycle*. Prim's adds the cheapest edge connecting the current tree to a vertex outside the tree.

---

## 9. Prim's Algorithm

### 1. Concept Explanation

*   **What:** Prim's algorithm is a greedy algorithm that finds an MST for a connected, weighted, undirected graph.
*   **How:** It builds the MST incrementally, starting from an arbitrary vertex. At each step, it adds the cheapest edge that connects a vertex *already in* the growing MST to a vertex *outside* the MST. It maintains a set of vertices currently in the MST.
*   **Analogy:** Starting a fire (the initial vertex). You look at all pieces of wood touching the current fire (edges connecting MST vertices to non-MST vertices) and add the one that catches fire most easily (cheapest edge) to expand the fire (grow the MST).
*   **Data Structures:** Typically uses a **priority queue** to efficiently find the minimum weight edge connecting a vertex in the MST to one outside. It stores potential edges or vertices (keyed by the weight of the edge connecting them to the tree).

### 2. Real-World Analogies and Use-Cases

*   (Same as general MST use-cases: network design, clustering, etc.)

### 3. Step-by-Step Solved Example

**Problem:** Find the MST for the following graph using Prim's algorithm, starting from vertex A.

```
      B --1-- C
     /|      /|
    4 |     / | 2
   /  |    /  |
  A --3-- D --5-- E
   \  |    \  |
    6 |     \ | 4
     \|      \|
      F --2-- G
```

**Steps (using Priority Queue storing `(weight, destination_vertex, source_vertex)`):**

1.  **Initialization:**
    *   MST = {} (empty set of edges)
    *   Visited = {A}
    *   PQ = {}
    *   Add edges from A to PQ: `(4, B, A)`, `(3, D, A)`, `(6, F, A)` -> PQ = `{(3, D, A), (4, B, A), (6, F, A)}` (sorted by weight)
    *   Total Cost = 0

2.  **Iteration 1:**
    *   Extract min from PQ: `(3, D, A)`.
    *   D is not visited. Add edge (A, D) to MST. Visited = {A, D}. Cost = 3.
    *   Add edges from D to PQ (to unvisited neighbors): `(1, B, D)` [B not visited], `(2, C, D)` [C not visited], `(5, E, D)` [E not visited], `(4, G, D)` [G not visited].
    *   PQ = `{(1, B, D), (2, C, D), (4, B, A), (4, G, D), (5, E, D), (6, F, A)}`

3.  **Iteration 2:**
    *   Extract min from PQ: `(1, B, D)`.
    *   B is not visited. Add edge (D, B) to MST. Visited = {A, D, B}. Cost = 3 + 1 = 4.
    *   Add edges from B to PQ (to unvisited neighbors): `(1, C, B)` [C not visited]. Note: Edge (B,A) with weight 4 is already represented by (4,B,A) or implicitly handled if we store vertices keyed by min distance. Let's assume we add edges.
    *   PQ = `{(1, C, B), (2, C, D), (4, B, A), (4, G, D), (5, E, D), (6, F, A)}`

4.  **Iteration 3:**
    *   Extract min from PQ: `(1, C, B)`.
    *   C is not visited. Add edge (B, C) to MST. Visited = {A, D, B, C}. Cost = 4 + 1 = 5.
    *   Add edges from C to PQ: `(2, E, C)` [E not visited]. Edge (C,D) is already represented by (2,C,D).
    *   PQ = `{(2, C, D), (2, E, C), (4, B, A), (4, G, D), (5, E, D), (6, F, A)}`

5.  **Iteration 4:**
    *   Extract min from PQ: `(2, C, D)`.
    *   C is already visited. Discard.

6.  **Iteration 5:**
    *   Extract min from PQ: `(2, E, C)`.
    *   E is not visited. Add edge (C, E) to MST. Visited = {A, D, B, C, E}. Cost = 5 + 2 = 7.
    *   Add edges from E to PQ: (No unvisited neighbors connected only to E). Edge (E,D) represented by (5,E,D).
    *   PQ = `{(4, B, A), (4, G, D), (5, E, D), (6, F, A)}`

7.  **Iteration 6:**
    *   Extract min from PQ: `(4, B, A)`.
    *   B is visited. Discard.

8.  **Iteration 7:**
    *   Extract min from PQ: `(4, G, D)`.
    *   G is not visited. Add edge (D, G) to MST. Visited = {A, D, B, C, E, G}. Cost = 7 + 4 = 11.
    *   Add edges from G to PQ: `(2, F, G)` [F not visited].
    *   PQ = `{(2, F, G), (5, E, D), (6, F, A)}`

9.  **Iteration 8:**
    *   Extract min from PQ: `(2, F, G)`.
    *   F is not visited. Add edge (G, F) to MST. Visited = {A, D, B, C, E, G, F}. Cost = 11 + 2 = 13.
    *   Add edges from F to PQ: (No unvisited neighbors). Edge (F,A) represented by (6,F,A).
    *   PQ = `{(5, E, D), (6, F, A)}`

10. **Iteration 9:**
    *   Extract min from PQ: `(5, E, D)`.
    *   E is visited. Discard.

11. **Iteration 10:**
    *   Extract min from PQ: `(6, F, A)`.
    *   F is visited. Discard.

12. **Termination:** PQ is empty (or all remaining vertices are visited). All vertices are visited.

**Result:**
*   MST Edges: {(A, D), (D, B), (B, C), (C, E), (D, G), (G, F)}
*   Total Cost: 13

### 4. Pseudocode and Code Implementation

**Pseudocode (using Priority Queue):**

```pseudocode
function PrimMST(Graph G, start_vertex s):
  // Initialize
  MST_Edges = empty set
  Visited = empty set
  PQ = empty PriorityQueue // Stores (weight, destination, source) or (weight, vertex)
  TotalCost = 0

  // Add start vertex data
  Visited.add(s)
  // Add edges from 's' to PQ, or initialize distances
  // Approach 1: Add edges to PQ
  // for each neighbor 'v' of 's':
  //   PQ.insert((weight(s, v), v, s))

  // Approach 2: Key-based (more common)
  key = array[|V|] initialized to INFINITY
  parent = array[|V|] initialized to NULL
  key[s] = 0
  PQ.insert((0, s)) // Store (key_value, vertex)

  while PQ is not empty:
    // Extract vertex 'u' with minimum key not yet in MST
    (min_key, u) = PQ.extract_min()

    if u in Visited: // Handles stale entries in some PQ implementations
        continue

    Visited.add(u)
    TotalCost = TotalCost + min_key // Add weight of edge connecting u
    if parent[u] is not NULL:
        MST_Edges.add((parent[u], u))

    // Update keys of neighbors 'v' of 'u'
    for each neighbor 'v' of 'u':
      if v not in Visited and weight(u, v) < key[v]:
        key[v] = weight(u, v)
        parent[v] = u
        // If v is already in PQ, decrease its key. If not, insert it.
        PQ.decrease_key(v, key[v]) or PQ.insert((key[v], v))

  return MST_Edges, TotalCost
```

**Python Implementation (using `heapq` as Priority Queue):**

```python
import heapq

def prim_mst(graph, start_node):
    """
    Finds the MST using Prim's algorithm.
    Args:
        graph: Adjacency list representation {node: [(neighbor, weight), ...]}
        start_node: The node to start the MST from.
    Returns:
        A tuple: (total_cost, mst_edges)
                 mst_edges is a list of tuples (u, v, weight).
    """
    if not graph or start_node not in graph:
        return 0, []

    mst_edges = []
    visited = set()
    # Min-heap stores (weight, current_node, previous_node)
    min_heap = [(0, start_node, None)] # (cost to reach, node, parent)
    total_cost = 0
    edge_count = 0
    num_nodes = len(graph)

    # Track minimum edge cost to reach each node from the MST
    min_cost_to_reach = {node: float('inf') for node in graph}
    min_cost_to_reach[start_node] = 0

    while min_heap and edge_count < num_nodes : # Stop when all nodes are potentially reached
        weight, current_node, prev_node = heapq.heappop(min_heap)

        # If already visited, skip (this handles stale entries in heap)
        if current_node in visited:
            continue

        # Add node to visited set and edge to MST (if not the start node)
        visited.add(current_node)
        if prev_node is not None:
            mst_edges.append((prev_node, current_node, weight))
            total_cost += weight
        edge_count += 1 # Count nodes added to the MST 'cloud'

        # Explore neighbors
        for neighbor, edge_weight in graph.get(current_node, []):
            if neighbor not in visited and edge_weight < min_cost_to_reach[neighbor]:
                 min_cost_to_reach[neighbor] = edge_weight # Update min cost
                 heapq.heappush(min_heap, (edge_weight, neighbor, current_node))

    # Check if MST spans all nodes (graph might be disconnected)
    if len(visited) != num_nodes:
         print(f"Warning: Graph might be disconnected. MST found for component containing {start_node}.")
         # Depending on requirements, return error or the forest found

    return total_cost, mst_edges

# Example Usage (Graph from Step 3):
graph_adj = {
    'A': [('B', 4), ('D', 3), ('F', 6)],
    'B': [('A', 4), ('C', 1), ('D', 1)],
    'C': [('B', 1), ('D', 2), ('E', 2)],
    'D': [('A', 3), ('B', 1), ('C', 2), ('E', 5), ('G', 4)],
    'E': [('C', 2), ('D', 5)],
    'F': [('A', 6), ('G', 2)],
    'G': [('D', 4), ('F', 2)]
}

cost, edges = prim_mst(graph_adj, 'A')
print(f"Prim's MST Cost: {cost}") # Output: 13
print("Prim's MST Edges:")
for u, v, w in sorted(edges, key=lambda x: x[2]): # Sort for consistent output
    print(f"  ({u}, {v}, {w})")
# Output:
# Prim's MST Cost: 13
# Prim's MST Edges:
#   (D, B, 1)
#   (B, C, 1)
#   (G, F, 2)
#   (C, E, 2)
#   (A, D, 3)
#   (D, G, 4)
```

**C++ Implementation (using `priority_queue`):**

```c++
#include <iostream>
#include <vector>
#include <queue>
#include <map>
#include <set>
#include <limits> // For numeric_limits
#include <tuple>  // For pair or tuple

using namespace std;

const double INF = numeric_limits<double>::infinity();

// Define edge structure for result
struct Edge {
    char u, v;
    double weight;
    // For sorting output
    bool operator<(const Edge& other) const {
        return weight < other.weight;
    }
};

// Graph representation: Adjacency list
using Graph = map<char, vector<pair<char, double>>>;

pair<double, vector<Edge>> prim_mst_cpp(const Graph& graph, char start_node) {
    if (graph.find(start_node) == graph.end()) {
        return {0.0, {}};
    }

    vector<Edge> mst_edges;
    set<char> visited;
    // Min-heap: stores {weight, {destination, source}}
    // Use negative weight for max-heap to simulate min-heap or use std::greater
    priority_queue<pair<double, pair<char, char>>,
                   vector<pair<double, pair<char, char>>>,
                   greater<pair<double, pair<char, char>>>> pq;

    double total_cost = 0.0;
    map<char, double> min_cost_to_reach; // Tracks min cost to reach node from MST cloud
    map<char, char> parent; // Tracks parent in MST

    // Initialize costs
    for (const auto& pair : graph) {
        min_cost_to_reach[pair.first] = INF;
        parent[pair.first] = 0; // Use 0 or special char for null parent
    }

    // Start with the start_node
    min_cost_to_reach[start_node] = 0;
    pq.push({0.0, {start_node, 0}}); // {cost, {node, parent}}

    while (!pq.empty()) {
        double weight = pq.top().first;
        char u = pq.top().second.first;
        char prev = pq.top().second.second; // Parent node that added this edge to PQ
        pq.pop();

        // If already visited, skip
        if (visited.count(u)) {
            continue;
        }

        // Add to MST
        visited.insert(u);
        total_cost += weight; // Add the cost of the edge connecting u to the tree
        if (prev != 0) { // Don't add edge for the starting node
            mst_edges.push_back({prev, u, weight});
        }

        // Explore neighbors
        if (graph.count(u)) { // Check if node u exists in graph keys
             for (const auto& edge : graph.at(u)) {
                char v = edge.first;
                double edge_weight = edge.second;

                if (!visited.count(v) && edge_weight < min_cost_to_reach[v]) {
                    min_cost_to_reach[v] = edge_weight;
                    parent[v] = u; // Update parent
                    pq.push({edge_weight, {v, u}}); // Add potential edge to PQ
                }
            }
        }
    }

     // Optional: Check for disconnected graph
     if (visited.size() != graph.size()) {
         cerr << "Warning: Graph might be disconnected." << endl;
     }


    return {total_cost, mst_edges};
}

int main() {
    Graph graph_adj = {
        {'A', {{'B', 4}, {'D', 3}, {'F', 6}}},
        {'B', {{'A', 4}, {'C', 1}, {'D', 1}}},
        {'C', {{'B', 1}, {'D', 2}, {'E', 2}}},
        {'D', {{'A', 3}, {'B', 1}, {'C', 2}, {'E', 5}, {'G', 4}}},
        {'E', {{'C', 2}, {'D', 5}}},
        {'F', {{'A', 6}, {'G', 2}}},
        {'G', {{'D', 4}, {'F', 2}}}
    };

    pair<double, vector<Edge>> result = prim_mst_cpp(graph_adj, 'A');
    double cost = result.first;
    vector<Edge> edges = result.second;

    cout << "Prim's MST Cost: " << cost << endl; // Output: 13
    cout << "Prim's MST Edges:" << endl;
    sort(edges.begin(), edges.end()); // Sort edges by weight
    for (const auto& edge : edges) {
        cout << "  (" << edge.u << ", " << edge.v << ", " << edge.weight << ")" << endl;
    }
    // Output: (Matches Python output order if sorted)

    return 0;
}
```

### 5. Diagrams or Flowcharts

**Algorithm Flow:**

```
Start Prim(Graph G, start_node s)
|
Initialize Visited={s}, MST={}, Cost=0
Initialize PQ with edges from s (or key[s]=0, others=INF)
|
+-----------------------+
| While PQ is not empty |
| AND MST not complete  |
+-----------------------+
       | Yes
       | Extract min-weight edge (u, v) from PQ where u in Visited, v not in Visited
       | (Or extract min-key vertex v from PQ)
       |
       +-----------------------+
       | Is v already Visited? | -- Yes --> Continue (Skip)
       +-----------------------+
              | No
              | Add v to Visited
              | Add edge (u, v) to MST
              | Add weight(u, v) to Cost
              | For each neighbor w of v:
              |   If w not in Visited:
              |     Add edge (v, w) to PQ (or update key[w] and PQ)
              +-----------------------+
|
End (Return MST, Cost)
```

**Example Progression Diagram:**

Show the graph at each step, highlighting visited nodes and the edges added to the MST.

*   **Step 0:** Node A is visited. PQ has edges (A,D,3), (A,B,4), (A,F,6).
*   **Step 1:** Edge (A,D) added. D visited. PQ updated.
*   **Step 2:** Edge (D,B) added. B visited. PQ updated.
*   ...and so on.

### 6. Key Formulas and Logic Summary

*   **Logic:** Grow the MST like a "cloud" starting from one vertex. Always add the cheapest edge connecting a vertex inside the cloud to one outside.
*   **Data Structure:** Priority Queue is key for efficiency.
*   **Time Complexity:**
    *   Using adjacency matrix and scanning: O(V^2)
    *   Using adjacency list and binary heap PQ: O(E log V)
    *   Using adjacency list and Fibonacci heap PQ: O(E + V log V) (often best theoretical)
*   **Space Complexity:** O(V + E) for graph representation, O(V) for visited set, key array, parent array, and PQ.

### 7. Common Mistakes and Edge Cases

*   **PQ Implementation:** Incorrectly using the priority queue (e.g., not handling updates/decreases correctly, leading to stale entries or inefficiency).
*   **Visited Set:** Forgetting to check if a vertex extracted from PQ is already visited (important if PQ can contain multiple entries for the same vertex with different weights).
*   **Initialization:** Incorrectly initializing keys/distances or the starting state.
*   **Disconnected Graphs:** Algorithm finds MST for the component containing the start node. Need modifications to find a Minimum Spanning Forest for disconnected graphs (e.g., loop through all nodes, run Prim's if not yet visited).

### 8. MCQ/Short Questions and Answers

1.  **Q:** What is the core idea of Prim's algorithm?
    **A:** Start with one vertex and iteratively grow the MST by adding the cheapest edge connecting a vertex in the current tree to a vertex outside the tree.
2.  **Q:** What data structure is typically used to efficiently find the cheapest edge in Prim's?
    **A:** A Priority Queue.
3.  **Q:** What is the time complexity of Prim's algorithm using an adjacency list and a binary heap?
    **A:** O(E log V).
4.  **Q:** Does Prim's algorithm work on directed graphs?
    **A:** No, MST is typically defined for undirected graphs.
5.  **Q:** If a graph has multiple edges with the same minimum weight crossing a cut, can Prim's algorithm choose any of them?
    **A:** Yes, it will pick one based on PQ implementation details, potentially leading to different (but equally valid) MSTs.

---

## 10. Kruskal's Algorithm

### 1. Concept Explanation

*   **What:** Kruskal's algorithm is another greedy algorithm for finding an MST in a connected, weighted, undirected graph.
*   **How:** It builds the MST by considering edges in increasing order of weight. It adds an edge to the growing MST *if and only if* adding the edge does not form a cycle among the already selected edges.
*   **Analogy:** You have a map of potential road connections between cities, each with a construction cost. You sort all possible roads by cost (cheapest first). You go down the list and build a road *unless* it would create a redundant loop between cities already connected by the roads you've built so far. You stop when all cities are connected.
*   **Data Structures:**
    *   Requires sorting all edges by weight initially.
    *   Uses a **Disjoint Set Union (DSU)** data structure (also known as Union-Find) to efficiently detect if adding an edge `(u, v)` would form a cycle. It checks if `u` and `v` are already in the same connected component (set). If not, adding the edge connects two previously separate components, and the DSU structure is updated (union operation).

### 2. Real-World Analogies and Use-Cases

*   (Same as general MST use-cases: network design, clustering, etc.)

### 3. Step-by-Step Solved Example

**Problem:** Find the MST for the same graph using Kruskal's algorithm.

```
      B --1-- C
     /|      /|
    4 |     / | 2
   /  |    /  |
  A --3-- D --5-- E
   \  |    \  |
    6 |     \ | 4
     \|      \|
      F --2-- G
```

**Steps:**

1.  **Sort Edges by Weight:**
    *   (B, C, 1)
    *   (B, D, 1)
    *   (C, E, 2)
    *   (F, G, 2)
    *   (C, D, 2) *Note: Example graph had C-D as 2, let's use that.*
    *   (A, D, 3)
    *   (A, B, 4)
    *   (D, G, 4)
    *   (D, E, 5)
    *   (A, F, 6)

2.  **Initialize DSU:** Each vertex {A, B, C, D, E, F, G} is in its own set.
    *   Sets: {A}, {B}, {C}, {D}, {E}, {F}, {G}
    *   MST = {}
    *   Total Cost = 0
    *   Edge Count = 0

3.  **Process Edges:**
    *   **Edge (B, C, 1):** Find(B) != Find(C). Add edge. Union(B, C). Cost=1. Edges=1. Sets: {A}, {B, C}, {D}, {E}, {F}, {G}.
    *   **Edge (B, D, 1):** Find(B) != Find(D). Add edge. Union(B, D) -> Union({B,C}, {D}). Cost=1+1=2. Edges=2. Sets: {A}, {B, C, D}, {E}, {F}, {G}.
    *   **Edge (C, E, 2):** Find(C) != Find(E). Add edge. Union(C, E) -> Union({B,C,D}, {E}). Cost=2+2=4. Edges=3. Sets: {A}, {B, C, D, E}, {F}, {G}.
    *   **Edge (F, G, 2):** Find(F) != Find(G). Add edge. Union(F, G). Cost=4+2=6. Edges=4. Sets: {A}, {B, C, D, E}, {F, G}.
    *   **Edge (C, D, 2):** Find(C) == Find(D) (both in {B,C,D,E}). **Reject edge (forms cycle).**
    *   **Edge (A, D, 3):** Find(A) != Find(D). Add edge. Union(A, D) -> Union({A}, {B,C,D,E}). Cost=6+3=9. Edges=5. Sets: {A, B, C, D, E}, {F, G}.
    *   **Edge (A, B, 4):** Find(A) == Find(B). **Reject edge.**
    *   **Edge (D, G, 4):** Find(D) != Find(G). Add edge. Union(D, G) -> Union({A,B,C,D,E}, {F,G}). Cost=9+4=13. Edges=6. Sets: {A, B, C, D, E, F, G}.
    *   **Stop:** We have |V|-1 = 7-1 = 6 edges. The MST is complete.

**Result:**
*   MST Edges: {(B, C), (B, D), (C, E), (F, G), (A, D), (D, G)}
*   Total Cost: 13

*(Note: This MST has the same total cost as Prim's but includes edge (D,G) instead of (G,F). Both are valid MSTs.)* Let's recheck Prim's trace. Ah, Prim's added (D,G,4) then (G,F,2). Kruskal added (F,G,2) then (D,G,4). The set of edges differs slightly but cost is same. My Prim's trace result was correct: {(A, D), (D, B), (B, C), (C, E), (D, G), (G, F)}. Kruskal's result: {(B, C), (B, D), (C, E), (F, G), (A, D), (D, G)}. Both cost 13.

### 4. Pseudocode and Code Implementation

**Pseudocode:**

```pseudocode
function KruskalMST(Graph G=(V, E)):
  // Initialize
  MST_Edges = empty set
  TotalCost = 0
  DSU = CreateDisjointSetUnionStructure(V) // Each vertex in its own set

  // Sort all edges E by weight in non-decreasing order
  SortedEdges = Sort(E by weight)

  // Process edges
  edge_count = 0
  for each edge (u, v) with weight w in SortedEdges:
    // Check if adding edge forms a cycle using DSU
    if DSU.Find(u) != DSU.Find(v):
      // No cycle: Add edge to MST
      MST_Edges.add((u, v))
      TotalCost = TotalCost + w
      DSU.Union(u, v) // Merge the sets containing u and v
      edge_count = edge_count + 1
      // Optimization: Stop if we have |V| - 1 edges
      if edge_count == |V| - 1:
        break

  // Check if MST is complete (graph might be disconnected)
  if edge_count != |V| - 1:
      Report "Graph is disconnected, found Minimum Spanning Forest"

  return MST_Edges, TotalCost
```

**Python Implementation (using a simple DSU class):**

```python
# Disjoint Set Union (Union-Find) Class
class DSU:
    def __init__(self, items):
        # Initialize parent array: each item is its own parent initially
        self.parent = {item: item for item in items}
        # Optional: Rank/Size optimization
        self.rank = {item: 0 for item in items} # Or size = 1

    def find(self, item):
        # Find the root of the set containing 'item' with path compression
        if self.parent[item] == item:
            return item
        self.parent[item] = self.find(self.parent[item]) # Path compression
        return self.parent[item]

    def union(self, item1, item2):
        # Merge the sets containing item1 and item2 using union by rank/size
        root1 = self.find(item1)
        root2 = self.find(item2)

        if root1 != root2:
            # Union by rank
            if self.rank[root1] < self.rank[root2]:
                self.parent[root1] = root2
            elif self.rank[root1] > self.rank[root2]:
                self.parent[root2] = root1
            else:
                self.parent[root2] = root1
                self.rank[root1] += 1
            return True # Union performed
        return False # Already in the same set

def kruskal_mst(graph_nodes, edges):
    """
    Finds the MST using Kruskal's algorithm.
    Args:
        graph_nodes: A list or set of all node identifiers.
        edges: A list of tuples representing edges (u, v, weight).
    Returns:
        A tuple: (total_cost, mst_edges)
                 mst_edges is a list of tuples (u, v, weight).
    """
    if not graph_nodes:
        return 0, []

    mst_edges = []
    total_cost = 0
    dsu = DSU(graph_nodes)

    # Sort edges by weight
    sorted_edges = sorted(edges, key=lambda x: x[2])

    edge_count = 0
    num_nodes = len(graph_nodes)

    for u, v, weight in sorted_edges:
        # If u and v are not already connected (in different sets)
        if dsu.union(u, v): # union returns True if merge happened
            mst_edges.append((u, v, weight))
            total_cost += weight
            edge_count += 1
            # Optimization: Stop when MST is complete
            if edge_count == num_nodes - 1:
                break

    # Check if MST spans all nodes
    if edge_count != num_nodes - 1 and num_nodes > 0 :
         # Check if graph was connected to begin with by seeing if all nodes ended up in one set
         root_check = None
         all_connected = True
         if graph_nodes:
             first_node = next(iter(graph_nodes)) # Get an arbitrary node
             root_check = dsu.find(first_node)
             for node in graph_nodes:
                 if dsu.find(node) != root_check:
                     all_connected = False
                     break
         if not all_connected:
             print("Warning: Graph is disconnected. Found Minimum Spanning Forest.")


    return total_cost, mst_edges

# Example Usage (Graph from Step 3):
nodes = {'A', 'B', 'C', 'D', 'E', 'F', 'G'}
edge_list = [
    ('A', 'B', 4), ('A', 'D', 3), ('A', 'F', 6),
    ('B', 'C', 1), ('B', 'D', 1),
    ('C', 'D', 2), ('C', 'E', 2),
    ('D', 'E', 5), ('D', 'G', 4),
    ('F', 'G', 2)
]

cost_k, edges_k = kruskal_mst(nodes, edge_list)
print(f"Kruskal's MST Cost: {cost_k}") # Output: 13
print("Kruskal's MST Edges:")
for u, v, w in sorted(edges_k, key=lambda x: x[2]): # Sort for consistent output
    print(f"  ({u}, {v}, {w})")
# Output:
# Kruskal's MST Cost: 13
# Kruskal's MST Edges:
#   (B, C, 1)
#   (B, D, 1)
#   (C, E, 2)
#   (F, G, 2)
#   (A, D, 3)
#   (D, G, 4)
```

**C++ Implementation (using a simple DSU implementation):**

```c++
#include <iostream>
#include <vector>
#include <numeric>   // For std::iota
#include <algorithm> // For std::sort
#include <map>
#include <set>
#include <string> // If using string node IDs

using namespace std;

// Edge structure for input and MST result
struct EdgeK {
    char u, v;
    double weight;
    // For sorting edges
    bool operator<(const EdgeK& other) const {
        return weight < other.weight;
    }
};

// Disjoint Set Union (DSU) Structure
struct DSU_cpp {
    map<char, char> parent;
    map<char, int> rank; // Or size

    DSU_cpp(const set<char>& items) {
        for (char item : items) {
            parent[item] = item;
            rank[item] = 0;
        }
    }

    char find(char item) {
        if (parent[item] == item) {
            return item;
        }
        // Path compression
        return parent[item] = find(parent[item]);
    }

    bool unite(char item1, char item2) {
        char root1 = find(item1);
        char root2 = find(item2);

        if (root1 != root2) {
            // Union by rank
            if (rank[root1] < rank[root2]) {
                parent[root1] = root2;
            } else if (rank[root1] > rank[root2]) {
                parent[root2] = root1;
            } else {
                parent[root2] = root1;
                rank[root1]++;
            }
            return true; // Union performed
        }
        return false; // Already in the same set
    }
};


pair<double, vector<EdgeK>> kruskal_mst_cpp(const set<char>& graph_nodes, vector<EdgeK>& edges) {
     if (graph_nodes.empty()) {
        return {0.0, {}};
    }

    vector<EdgeK> mst_edges;
    double total_cost = 0.0;
    DSU_cpp dsu(graph_nodes);

    // Sort edges by weight
    sort(edges.begin(), edges.end());

    int edge_count = 0;
    int num_nodes = graph_nodes.size();

    for (const auto& edge : edges) {
        // If u and v are not already connected
        if (dsu.unite(edge.u, edge.v)) {
            mst_edges.push_back(edge);
            total_cost += edge.weight;
            edge_count++;
            if (edge_count == num_nodes - 1) {
                break;
            }
        }
    }

     // Optional: Check for disconnected graph
     if (edge_count != num_nodes - 1 && num_nodes > 0) {
         char root_check = 0;
         bool all_connected = true;
         if (!graph_nodes.empty()) {
             root_check = dsu.find(*graph_nodes.begin());
             for(char node : graph_nodes) {
                 if (dsu.find(node) != root_check) {
                     all_connected = false;
                     break;
                 }
             }
         }
         if (!all_connected) {
            cerr << "Warning: Graph is disconnected. Found Minimum Spanning Forest." << endl;
         }
     }

    return {total_cost, mst_edges};
}


int main() {
    set<char> nodes = {'A', 'B', 'C', 'D', 'E', 'F', 'G'};
    vector<EdgeK> edge_list = {
        {'A', 'B', 4}, {'A', 'D', 3}, {'A', 'F', 6},
        {'B', 'C', 1}, {'B', 'D', 1},
        {'C', 'D', 2}, {'C', 'E', 2},
        {'D', 'E', 5}, {'D', 'G', 4},
        {'F', 'G', 2}
    };

    pair<double, vector<EdgeK>> result = kruskal_mst_cpp(nodes, edge_list);
    double cost = result.first;
    vector<EdgeK> mst = result.second;

    cout << "Kruskal's MST Cost: " << cost << endl; // Output: 13
    cout << "Kruskal's MST Edges:" << endl;
    // Sort output for consistency (already sorted by Kruskal's process, but maybe re-sort)
    sort(mst.begin(), mst.end());
    for (const auto& edge : mst) {
        cout << "  (" << edge.u << ", " << edge.v << ", " << edge.weight << ")" << endl;
    }
     // Output: (Matches Python output order if sorted)

    return 0;
}
```

### 5. Diagrams or Flowcharts

**Algorithm Flow:**

```
Start Kruskal(Graph G=(V, E))
|
Initialize MST={}, Cost=0
Initialize DSU with each vertex in its own set
Sort edges E by weight non-decreasingly -> SortedEdges
EdgeCount = 0
|
+---------------------------------+
| For each edge (u, v, w) in      |
| SortedEdges                     |
+---------------------------------+
       |
       +--------------------------+
       | If Find(u) != Find(v) ?  | -- No (Cycle) --> Continue to next edge
       +--------------------------+
              | Yes (No Cycle)
              | Add edge (u, v) to MST
              | Cost = Cost + w
              | Union(u, v)
              | EdgeCount = EdgeCount + 1
              | If EdgeCount == |V| - 1:
              |   Break loop
              +--------------------------+
|
End (Return MST, Cost)
```

**Example Progression Diagram:**

Show the graph state, highlighting the edges added to the MST and the sets in the DSU structure after processing each edge.

*   **Initial:** Sets: {A}, {B}, {C}, {D}, {E}, {F}, {G}. Edges sorted.
*   **After (B,C,1):** Sets: {A}, {B,C}, {D}, {E}, {F}, {G}. MST={(B,C)}.
*   **After (B,D,1):** Sets: {A}, {B,C,D}, {E}, {F}, {G}. MST={(B,C), (B,D)}.
*   ...and so on.

### 6. Key Formulas and Logic Summary

*   **Logic:** Consider edges in increasing order of weight. Add an edge if it connects two previously disconnected components (checked using DSU Find operation). Merge components using DSU Union operation.
*   **Data Structure:** Sorting edges, Disjoint Set Union (DSU).
*   **Time Complexity:** O(E log E) for sorting edges. The DSU operations with path compression and union by rank/size are nearly constant on average (amortized time complexity is related to the inverse Ackermann function, α(V), which is extremely slow-growing, effectively O(1) for practical purposes). Therefore, the dominant factor is usually edge sorting: **O(E log E)** or **O(E log V)** (since E can be up to V^2, log(E) can be up to log(V^2) = 2 log V).
*   **Space Complexity:** O(V + E) for graph, edges, and DSU structure.

### 7. Common Mistakes and Edge Cases

*   **DSU Implementation:** Errors in the Find (especially path compression) or Union (especially rank/size tracking) logic.
*   **Cycle Detection:** Incorrectly determining if adding an edge creates a cycle (the core purpose of DSU here).
*   **Edge Sorting:** Forgetting to sort edges or sorting incorrectly.
*   **Disconnected Graphs:** Algorithm finds a Minimum Spanning Forest. The termination condition (`|V|-1` edges) might not be met if the graph is disconnected. Need to check the final state (e.g., number of sets in DSU).

### 8. MCQ/Short Questions and Answers

1.  **Q:** What is the core idea of Kruskal's algorithm?
    **A:** Sort edges by weight and add the next cheapest edge to the MST if it doesn't form a cycle with already selected edges.
2.  **Q:** What data structure is crucial for efficiently detecting cycles in Kruskal's?
    **A:** Disjoint Set Union (DSU) / Union-Find.
3.  **Q:** What is the typical time complexity bottleneck for Kruskal's algorithm?
    **A:** Sorting the edges, leading to O(E log E) or O(E log V).
4.  **Q:** How does Kruskal's handle disconnected graphs?
    **A:** It finds a Minimum Spanning Forest, containing the MST for each connected component.
5.  **Q:** Does Kruskal's algorithm start from a specific vertex?
    **A:** No, it considers edges globally based on weight, not starting from a particular node like Prim's.

---

## 11. Dijkstra's Algorithm

### 1. Concept Explanation

*   **What:** Dijkstra's algorithm finds the shortest paths from a single source vertex to all other vertices in a weighted **directed or undirected graph** with **non-negative edge weights**.
*   **Why Greedy:** It's greedy because at each step, it selects the unvisited vertex with the smallest known distance from the source and declares this distance as final (shortest). It assumes that once we find the shortest path to a vertex `u`, any path going through `u` to another vertex `v` will build upon this shortest path. This greedy choice works because edge weights are non-negative, ensuring that visiting a vertex later cannot lead to a shorter path to an already finalized vertex.
*   **How:**
    1.  Initialize distances: `dist[source] = 0`, `dist[all_others] = infinity`.
    2.  Maintain a set of visited vertices (whose shortest path is finalized) and usually a priority queue of unvisited vertices keyed by their current known shortest distance from the source.
    3.  Start with the source node in the PQ.
    4.  While the PQ is not empty:
        a.  Extract the vertex `u` with the smallest distance from the PQ.
        b.  Mark `u` as visited.
        c.  For each neighbor `v` of `u`:
            i.  **Relaxation:** If `dist[u] + weight(u, v) < dist[v]`:
                *   Update `dist[v] = dist[u] + weight(u, v)`.
                *   Update `v`'s position in the PQ (decrease-key) or add the new distance to the PQ.
                *   Optionally, store `parent[v] = u` to reconstruct the path.
*   **Analogy:** Finding the fastest way to drive from your home (source) to all other locations in a city. You explore outwards, always finalizing the shortest time to the nearest reachable, unvisited location, and then updating the estimated times to its neighbors.

### 2. Real-World Analogies and Use-Cases

*   **Analogy:** GPS navigation finding the shortest/fastest route. Network routing protocols determining the best path for data packets.
*   **Use-Cases:**
    *   **Network Routing:** OSPF (Open Shortest Path First) protocol.
    *   **Mapping Services:** Google Maps, Waze finding shortest driving routes.
    *   **Social Networks:** Finding shortest connection paths between users.
    *   **Robotics/AI:** Pathfinding for agents.
    *   **Telecommunications:** Finding lowest latency paths.

### 3. Step-by-Step Solved Example

**Problem:** Find the shortest paths from source A to all other vertices in the graph from the MST example.

```
      B --1-- C
     /|      /|
    4 |     / | 2
   /  |    /  |
  A --3-- D --5-- E
   \  |    \  |
    6 |     \ | 4
     \|      \|
      F --2-- G
```

**Steps (using Priority Queue storing `(distance, vertex)`):**

1.  **Initialization:**
    *   `dist = {A: 0, B: inf, C: inf, D: inf, E: inf, F: inf, G: inf}`
    *   `parent = {A: None, ...}`
    *   `visited = {}`
    *   `PQ = {(0, A)}`

2.  **Iteration 1:**
    *   Extract min: `(0, A)`. Add A to `visited`.
    *   Neighbors of A: B, D, F.
    *   Relax (A, B): `dist[A]+4 = 4 < dist[B]`. Update `dist[B]=4`, `parent[B]=A`. Add `(4, B)` to PQ.
    *   Relax (A, D): `dist[A]+3 = 3 < dist[D]`. Update `dist[D]=3`, `parent[D]=A`. Add `(3, D)` to PQ.
    *   Relax (A, F): `dist[A]+6 = 6 < dist[F]`. Update `dist[F]=6`, `parent[F]=A`. Add `(6, F)` to PQ.
    *   `PQ = {(3, D), (4, B), (6, F)}`

3.  **Iteration 2:**
    *   Extract min: `(3, D)`. Add D to `visited`.
    *   Neighbors of D: A, B, C, E, G. (A is visited).
    *   Relax (D, B): `dist[D]+1 = 3+1 = 4`. `4 == dist[B]`. No update needed (or update if strictly less). Let's assume no update on equal.
    *   Relax (D, C): `dist[D]+2 = 3+2 = 5 < dist[C]`. Update `dist[C]=5`, `parent[C]=D`. Add `(5, C)` to PQ.
    *   Relax (D, E): `dist[D]+5 = 3+5 = 8 < dist[E]`. Update `dist[E]=8`, `parent[E]=D`. Add `(8, E)` to PQ.
    *   Relax (D, G): `dist[D]+4 = 3+4 = 7 < dist[G]`. Update `dist[G]=7`, `parent[G]=D`. Add `(7, G)` to PQ.
    *   `PQ = {(4, B), (5, C), (6, F), (7, G), (8, E)}`

4.  **Iteration 3:**
    *   Extract min: `(4, B)`. Add B to `visited`.
    *   Neighbors of B: A, C, D. (A, D visited).
    *   Relax (B, C): `dist[B]+1 = 4+1 = 5`. `5 == dist[C]`. No update.
    *   `PQ = {(5, C), (6, F), (7, G), (8, E)}`

5.  **Iteration 4:**
    *   Extract min: `(5, C)`. Add C to `visited`.
    *   Neighbors of C: B, D, E. (B, D visited).
    *   Relax (C, E): `dist[C]+2 = 5+2 = 7 < dist[E]`. Update `dist[E]=7`, `parent[E]=C`. Add `(7, E)` to PQ (or decrease-key).
    *   `PQ = {(6, F), (7, G), (7, E), (8, E)}` *(Note: (8, E) is now stale)*

6.  **Iteration 5:**
    *   Extract min: `(6, F)`. Add F to `visited`.
    *   Neighbors of F: A, G. (A visited).
    *   Relax (F, G): `dist[F]+2 = 6+2 = 8 > dist[G]=7`. No update.
    *   `PQ = {(7, G), (7, E), (8, E)}`

7.  **Iteration 6:**
    *   Extract min: `(7, G)`. Add G to `visited`.
    *   Neighbors of G: D, F. (D, F visited). No relaxations.
    *   `PQ = {(7, E), (8, E)}`

8.  **Iteration 7:**
    *   Extract min: `(7, E)`. Add E to `visited`.
    *   Neighbors of E: C, D. (C, D visited). No relaxations.
    *   `PQ = {(8, E)}`

9.  **Iteration 8:**
    *   Extract min: `(8, E)`. E is already visited. Skip.
    *   `PQ = {}`

10. **Termination:** PQ is empty.

**Result:** Shortest path distances from A:
*   `dist = {A: 0, B: 4, C: 5, D: 3, E: 7, F: 6, G: 7}`
*   `parent` allows path reconstruction (e.g., path to E: E <- C <- D <- A. Path: A->D->C->E)

### 4. Pseudocode and Code Implementation

**Pseudocode:**

```pseudocode
function Dijkstra(Graph G, source s):
  // Initialization
  dist = array[|V|] initialized to INFINITY
  parent = array[|V|] initialized to NULL
  dist[s] = 0
  PQ = empty PriorityQueue // Stores (distance, vertex)

  // Add source to PQ
  PQ.insert((0, s))

  while PQ is not empty:
    // Get vertex 'u' with smallest distance in PQ
    (d, u) = PQ.extract_min()

    // Optimization: If we extracted a stale distance, skip
    if d > dist[u]:
      continue

    // Process neighbors 'v' of 'u'
    for each neighbor 'v' of 'u':
      weight_uv = weight(u, v)
      // Relaxation step
      if dist[u] + weight_uv < dist[v]:
        dist[v] = dist[u] + weight_uv
        parent[v] = u
        // Add/update 'v' in PQ with the new distance
        PQ.insert_or_decrease_key((dist[v], v))

  return dist, parent
```

**Python Implementation:**

```python
import heapq

def dijkstra(graph, start_node):
    """
    Finds shortest paths from start_node using Dijkstra's algorithm.
    Args:
        graph: Adjacency list representation {node: [(neighbor, weight), ...]}
        start_node: The source node.
    Returns:
        A tuple: (distances, parents)
                 distances is a dict {node: shortest_distance_from_start}
                 parents is a dict {node: predecessor_on_shortest_path}
    """
    if not graph or start_node not in graph:
        return {}, {}

    distances = {node: float('inf') for node in graph}
    parents = {node: None for node in graph}
    distances[start_node] = 0

    # Min-heap stores (current_distance, node)
    priority_queue = [(0, start_node)]

    while priority_queue:
        current_dist, current_node = heapq.heappop(priority_queue)

        # If we found a shorter path already, skip this one
        if current_dist > distances[current_node]:
            continue

        # Explore neighbors
        for neighbor, weight in graph.get(current_node, []):
            distance = current_dist + weight

            # Relaxation: If found a shorter path to neighbor
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                parents[neighbor] = current_node
                heapq.heappush(priority_queue, (distance, neighbor))

    return distances, parents

# Function to reconstruct path
def get_path(parents, start_node, end_node):
    path = []
    curr = end_node
    while curr is not None:
        path.append(curr)
        if curr == start_node:
            break
        curr = parents.get(curr) # Use get to avoid KeyError if no path
    if path[-1] != start_node: # Check if path reaches start node
        return None # No path exists
    return path[::-1] # Reverse


# Example Usage (Graph from Step 3):
graph_adj = {
    'A': [('B', 4), ('D', 3), ('F', 6)],
    'B': [('A', 4), ('C', 1), ('D', 1)],
    'C': [('B', 1), ('D', 2), ('E', 2)],
    'D': [('A', 3), ('B', 1), ('C', 2), ('E', 5), ('G', 4)],
    'E': [('C', 2), ('D', 5)],
    'F': [('A', 6), ('G', 2)],
    'G': [('D', 4), ('F', 2)]
}

distances, parents = dijkstra(graph_adj, 'A')

print("Dijkstra Shortest Distances from A:")
for node, dist in sorted(distances.items()):
    print(f"  To {node}: {dist}")

print("\nExample Path (A to E):")
path_ae = get_path(parents, 'A', 'E')
print(f"  {' -> '.join(path_ae) if path_ae else 'No path'}")

# Output:
# Dijkstra Shortest Distances from A:
#   To A: 0
#   To B: 4
#   To C: 5
#   To D: 3
#   To E: 7
#   To F: 6
#   To G: 7
#
# Example Path (A to E):
#   A -> D -> C -> E
```

**C++ Implementation:**

```c++
#include <iostream>
#include <vector>
#include <queue>
#include <map>
#include <limits> // For numeric_limits
#include <string> // If using string node IDs
#include <algorithm> // For reverse

using namespace std;

const double INF_DIJKSTRA = numeric_limits<double>::infinity();

// Graph representation: Adjacency list
using GraphD = map<char, vector<pair<char, double>>>;
using DistanceMap = map<char, double>;
using ParentMap = map<char, char>;

pair<DistanceMap, ParentMap> dijkstra_cpp(const GraphD& graph, char start_node) {
    DistanceMap distances;
    ParentMap parents;

    if (graph.find(start_node) == graph.end()) {
        return {distances, parents}; // Return empty maps if start node not in graph
    }

    // Initialize distances and parents
    for (const auto& pair : graph) {
        distances[pair.first] = INF_DIJKSTRA;
        parents[pair.first] = 0; // Use 0 or special char for null parent
    }
    distances[start_node] = 0;

    // Min-heap: stores {distance, node}
    priority_queue<pair<double, char>, vector<pair<double, char>>, greater<pair<double, char>>> pq;
    pq.push({0.0, start_node});

    while (!pq.empty()) {
        double current_dist = pq.top().first;
        char current_node = pq.top().second;
        pq.pop();

        // Optimization: Skip if found shorter path already
        if (current_dist > distances[current_node]) {
            continue;
        }

        // Explore neighbors (check if current_node exists in graph keys)
        if (graph.count(current_node)) {
            for (const auto& edge : graph.at(current_node)) {
                char neighbor = edge.first;
                double weight = edge.second;
                double distance_through_current = current_dist + weight;

                // Relaxation
                if (distance_through_current < distances[neighbor]) {
                    distances[neighbor] = distance_through_current;
                    parents[neighbor] = current_node;
                    pq.push({distances[neighbor], neighbor});
                }
            }
        }
    }

    return {distances, parents};
}

// Function to reconstruct path
vector<char> get_path_cpp(const ParentMap& parents, char start_node, char end_node) {
    vector<char> path;
    char curr = end_node;
    while (parents.count(curr)) { // Check if curr exists in parents map
        path.push_back(curr);
        if (curr == start_node) break;
        curr = parents.at(curr);
         if (curr == 0) { // Reached null parent before start node
             if (path.back() != start_node) return {}; // No path
             else break; // Found start node
         }
    }
     if (path.empty() || path.back() != start_node) return {}; // No path found

    reverse(path.begin(), path.end());
    return path;
}


int main() {
    GraphD graph_adj = {
        {'A', {{'B', 4}, {'D', 3}, {'F', 6}}},
        {'B', {{'A', 4}, {'C', 1}, {'D', 1}}},
        {'C', {{'B', 1}, {'D', 2}, {'E', 2}}},
        {'D', {{'A', 3}, {'B', 1}, {'C', 2}, {'E', 5}, {'G', 4}}},
        {'E', {{'C', 2}, {'D', 5}}},
        {'F', {{'A', 6}, {'G', 2}}},
        {'G', {{'D', 4}, {'F', 2}}}
    };

    pair<DistanceMap, ParentMap> result = dijkstra_cpp(graph_adj, 'A');
    DistanceMap distances = result.first;
    ParentMap parents = result.second;

    cout << "Dijkstra Shortest Distances from A:" << endl;
    // Sort nodes for consistent output
    vector<char> nodes;
    for(auto const& [key, val] : distances) nodes.push_back(key);
    sort(nodes.begin(), nodes.end());

    for (char node : nodes) {
         cout << "  To " << node << ": " << (distances[node] == INF_DIJKSTRA ? "inf" : to_string(distances[node])) << endl;
    }


    cout << "\nExample Path (A to E):" << endl;
    vector<char> path_ae = get_path_cpp(parents, 'A', 'E');
    if (!path_ae.empty()) {
        cout << "  ";
        for (size_t i = 0; i < path_ae.size(); ++i) {
            cout << path_ae[i] << (i == path_ae.size() - 1 ? "" : " -> ");
        }
        cout << endl;
    } else {
        cout << "  No path" << endl;
    }


    return 0;
}
```

### 5. Diagrams or Flowcharts

**Algorithm Flow:** (Similar structure to Prim's, but updates distances and uses relaxation)

```
Start Dijkstra(Graph G, source s)
|
Initialize dist[s]=0, dist[v]=INF for v!=s, parent[v]=NULL
Initialize PQ with (0, s)
|
+-----------------------+
| While PQ is not empty |
+-----------------------+
       | Yes
       | Extract vertex 'u' with minimum distance from PQ
       | If dist[u] is stale (already found shorter path), continue
       |
       | For each neighbor 'v' of 'u':
       |   // Relaxation
       |   If dist[u] + weight(u, v) < dist[v]:
       |     dist[v] = dist[u] + weight(u, v)
       |     parent[v] = u
       |     Add/Update (dist[v], v) in PQ
       +-----------------------+
|
End (Return dist, parent)
```

**Example Progression Diagram:**

Show the graph, the `dist` array, and the PQ contents at each iteration as vertices are finalized.

*   **Init:** `dist={A:0, B:inf, ...}`, `PQ={(0,A)}`
*   **Iter 1 (Extract A):** `dist={A:0, B:4, C:inf, D:3, E:inf, F:6, G:inf}`, `PQ={(3,D), (4,B), (6,F)}`
*   **Iter 2 (Extract D):** `dist={A:0, B:4, C:5, D:3, E:8, F:6, G:7}`, `PQ={(4,B), (5,C), (6,F), (7,G), (8,E)}`
*   ...and so on.

### 6. Key Formulas and Logic Summary

*   **Goal:** Find shortest paths from a single source `s` to all other vertices.
*   **Constraint:** Edge weights must be non-negative.
*   **Core Operation:** Relaxation: `if dist[u] + weight(u, v) < dist[v]: update dist[v]`.
*   **Logic:** Maintain tentative distances, iteratively finalize the distance to the closest unvisited vertex `u`, and relax edges outgoing from `u`.
*   **Data Structure:** Priority Queue is key for efficiency.
*   **Time Complexity:** Same as Prim's: O(V^2) (matrix), **O(E log V)** (adj list + binary heap), O(E + V log V) (adj list + Fibonacci heap).
*   **Space Complexity:** O(V + E) for graph, O(V) for distances, parents, PQ.

### 7. Common Mistakes and Edge Cases

*   **Negative Weights:** Dijkstra's algorithm **does not work correctly** if the graph has negative edge weights. The greedy choice can be wrong. (Use Bellman-Ford for graphs with negative edges).
*   **PQ Implementation:** Similar issues as Prim's (stale entries, decrease-key efficiency). The optimization `if current_dist > distances[current_node]: continue` handles stale entries simply.
*   **Initialization:** Forgetting to set `dist[source] = 0` or initializing others to infinity.
*   **Relaxation Condition:** Using `<=` instead of `<` (usually doesn't affect correctness but might do unnecessary updates) or getting the formula wrong.
*   **Path Reconstruction:** Errors in the `parent` tracking or the backtracking function.

### 8. MCQ/Short Questions and Answers

1.  **Q:** What problem does Dijkstra's algorithm solve?
    **A:** The single-source shortest paths problem in a weighted graph with non-negative edge weights.
2.  **Q:** What is the main limitation of Dijkstra's algorithm?
    **A:** It does not work correctly if the graph contains negative edge weights.
3.  **Q:** What is the "relaxation" step in Dijkstra's algorithm?
    **A:** Checking if the path to a neighbor `v` through the current node `u` is shorter than the currently known shortest path to `v`, and updating `dist[v]` if it is.
4.  **Q:** What is the time complexity of Dijkstra's using an adjacency list and a binary heap?
    **A:** O(E log V).
5.  **Q:** Is Dijkstra's a Dynamic Programming or Greedy algorithm?
    **A:** It is a Greedy algorithm because it makes the locally optimal choice of finalizing the closest unvisited vertex at each step.

---

## 12. Huffman Coding

### 1. Concept Explanation

*   **What:** Huffman coding is a greedy algorithm used for lossless data compression. It assigns variable-length binary codes (sequences of 0s and 1s) to input characters, where the lengths of the codes are based on the frequencies of the characters. More frequent characters get shorter codes, and less frequent characters get longer codes.
*   **Prefix Codes:** Huffman codes are **prefix codes** (also called prefix-free codes), meaning that no code assigned to a character is a prefix of the code assigned to any other character. This property ensures unambiguous decoding.
*   **Why Greedy:** The algorithm greedily builds an optimal binary tree (the Huffman tree). At each step, it combines the two nodes (characters or subtrees) with the *lowest frequencies* into a new subtree. This locally optimal choice of merging the least frequent items leads to a globally optimal (minimum expected code length) prefix code.
*   **How:**
    1.  Calculate the frequency of each character in the input data.
    2.  Create a leaf node for each character, storing the character and its frequency.
    3.  Use a min-priority queue to store these nodes, ordered by frequency.
    4.  While there is more than one node in the priority queue:
        a.  Extract the two nodes with the lowest frequencies (say `node1` and `node2`).
        b.  Create a new internal node whose frequency is the sum of `node1`'s and `node2`'s frequencies.
        c.  Make `node1` the left child and `node2` the right child (or vice-versa, consistently).
        d.  Insert the new internal node back into the priority queue.
    5.  The single node remaining in the priority queue is the root of the Huffman tree.
    6.  Traverse the tree from the root to each leaf node to generate the codes: assign '0' for traversing a left edge and '1' for a right edge. The path from the root to a character's leaf node forms its Huffman code.

### 2. Real-World Analogies and Use-Cases

*   **Analogy:** Creating abbreviations for frequently used long words in your notes. You'd use very short abbreviations for common words ("the" -> "t") and longer ones for rare words. Huffman coding does this systematically with binary codes.
*   **Use-Cases:**
    *   File compression (used within formats like PKZIP, GZIP, PNG, JPEG).
    *   Data transmission (reducing bandwidth usage).
    *   Multimedia codecs (part of compressing audio/video data).

### 3. Step-by-Step Solved Example

**Problem:** Generate Huffman codes for characters with frequencies: A:5, B:9, C:12, D:13, E:16, F:45.

**Steps:**

1.  **Initial Nodes (Leaves in PQ):**
    *   PQ = {(5, A), (9, B), (12, C), (13, D), (16, E), (45, F)}

2.  **Iteration 1:**
    *   Extract min: (5, A), (9, B).
    *   Combine: New internal node N1 (freq=5+9=14). Left=A, Right=B.
    *   PQ = {(12, C), (13, D), (14, N1), (16, E), (45, F)}

3.  **Iteration 2:**
    *   Extract min: (12, C), (13, D).
    *   Combine: New internal node N2 (freq=12+13=25). Left=C, Right=D.
    *   PQ = {(14, N1), (16, E), (25, N2), (45, F)}

4.  **Iteration 3:**
    *   Extract min: (14, N1), (16, E).
    *   Combine: New internal node N3 (freq=14+16=30). Left=N1, Right=E.
    *   PQ = {(25, N2), (30, N3), (45, F)}

5.  **Iteration 4:**
    *   Extract min: (25, N2), (30, N3).
    *   Combine: New internal node N4 (freq=25+30=55). Left=N2, Right=N3.
    *   PQ = {(45, F), (55, N4)}

6.  **Iteration 5:**
    *   Extract min: (45, F), (55, N4).
    *   Combine: Root node N5 (freq=45+55=100). Left=F, Right=N4.
    *   PQ = {(100, N5)}

7.  **Termination:** Only root node remains.

**Huffman Tree:**

```
          N5 (100)
         /      \
      0 /        \ 1
       F (45)    N4 (55)
                /      \
             0 /        \ 1
              N2 (25)    N3 (30)
             /      \    /      \
          0 /        \1 0/        \ 1
           C (12)    D(13) N1(14)   E(16)
                        /      \
                     0 /        \ 1
                      A(5)      B(9)
```

**Generate Codes (0=left, 1=right):**
*   F: 0
*   C: 100
*   D: 101
*   A: 1100
*   B: 1101
*   E: 111

**Check Prefix Property:** No code is a prefix of another.
**Check Length vs Frequency:** F (most frequent) has shortest code (1 bit). A, B (least frequent) have longest codes (4 bits).

### 4. Pseudocode and Code Implementation

**Pseudocode:**

```pseudocode
function HuffmanCoding(Characters C, Frequencies F):
  n = number of characters
  // Create leaf nodes
  Nodes = CreateLeafNodes(C, F) // Each node stores char, freq, left=null, right=null

  // Build Min-Priority Queue based on frequency
  PQ = BuildMinPriorityQueue(Nodes)

  // Build the Huffman Tree
  while PQ.size() > 1:
    node1 = PQ.extract_min()
    node2 = PQ.extract_min()

    newNode = CreateInternalNode()
    newNode.frequency = node1.frequency + node2.frequency
    newNode.left = node1
    newNode.right = node2
    // newNode.character = null (or special marker)

    PQ.insert(newNode)

  // The single remaining node is the root
  root = PQ.extract_min()

  // Generate codes by traversing the tree
  Codes = GenerateCodes(root, "") // Recursive function

  return Codes

// Helper function to generate codes
function GenerateCodes(node, current_code):
  if node is null: return

  // If leaf node, store the code
  if node.isLeaf(): // Check if node.character is not null
    Codes[node.character] = current_code
    return

  // Traverse left (append '0')
  GenerateCodes(node.left, current_code + "0")
  // Traverse right (append '1')
  GenerateCodes(node.right, current_code + "1")
```

**Python Implementation:**

```python
import heapq
from collections import defaultdict, Counter

class HuffmanNode:
    def __init__(self, char, freq, left=None, right=None):
        self.char = char
        self.freq = freq
        self.left = left
        self.right = right

    # Make nodes comparable for priority queue (based on frequency)
    def __lt__(self, other):
        return self.freq < other.freq

def build_huffman_tree(text):
    """Builds the Huffman tree from input text."""
    if not text:
        return None, {}

    frequency = Counter(text)
    priority_queue = [HuffmanNode(char, freq) for char, freq in frequency.items()]
    heapq.heapify(priority_queue)

    while len(priority_queue) > 1:
        left = heapq.heappop(priority_queue)
        right = heapq.heappop(priority_queue)

        # Create new internal node (char is None)
        merged_freq = left.freq + right.freq
        merged_node = HuffmanNode(None, merged_freq, left, right)

        heapq.heappush(priority_queue, merged_node)

    # The root of the tree is the only item left
    return priority_queue[0] if priority_queue else None

def generate_codes_recursive(node, current_code, codes_dict):
    """Helper to traverse tree and generate codes."""
    if node is None:
        return

    # If it's a leaf node, store the code
    if node.char is not None:
        codes_dict[node.char] = current_code if current_code else "0" # Handle single node case
        return

    # Traverse left (0) and right (1)
    generate_codes_recursive(node.left, current_code + "0", codes_dict)
    generate_codes_recursive(node.right, current_code + "1", codes_dict)

def huffman_coding(text):
    """Generates Huffman codes for characters in the text."""
    root = build_huffman_tree(text)
    if root is None:
        return {}

    codes = {}
    generate_codes_recursive(root, "", codes)
    # Handle case of text with only one unique character
    if not codes and root and root.char is not None:
         codes[root.char] = "0"

    return codes

# Example Usage (Frequencies from Step 3):
# Construct a sample text with those frequencies (approx)
sample_text = ("A"*5) + ("B"*9) + ("C"*12) + ("D"*13) + ("E"*16) + ("F"*45)

huffman_codes = huffman_coding(sample_text)

print("Huffman Codes:")
# Sort by character for consistent output
for char, code in sorted(huffman_codes.items()):
    print(f"  '{char}': {code}")

# Output: (Matches codes from Step 3)
# Huffman Codes:
#   'A': 1100
#   'B': 1101
#   'C': 100
#   'D': 101
#   'E': 111
#   'F': 0
```

**C++ Implementation:**

```c++
#include <iostream>
#include <string>
#include <vector>
#include <queue>
#include <map>
#include <memory> // For shared_ptr
#include <functional> // For std::greater

using namespace std;

// Node structure for Huffman Tree
struct HuffmanNode {
    char data;
    unsigned frequency;
    shared_ptr<HuffmanNode> left, right;

    HuffmanNode(char data, unsigned frequency) : data(data), frequency(frequency), left(nullptr), right(nullptr) {}
};

// Comparison structure for priority queue (min-heap)
struct CompareNodes {
    bool operator()(const shared_ptr<HuffmanNode>& l, const shared_ptr<HuffmanNode>& r) {
        return l->frequency > r->frequency; // Min-heap based on frequency
    }
};

// Function to generate codes recursively
void generate_codes_recursive_cpp(const shared_ptr<HuffmanNode>& node, string current_code, map<char, string>& codes_dict) {
    if (!node) {
        return;
    }

    // Leaf node: store the code
    if (!node->left && !node->right) { // Check if it's a leaf
        codes_dict[node->data] = current_code.empty() ? "0" : current_code; // Handle single node case
        return;
    }

    generate_codes_recursive_cpp(node->left, current_code + "0", codes_dict);
    generate_codes_recursive_cpp(node->right, current_code + "1", codes_dict);
}

// Main Huffman Coding function
map<char, string> huffman_coding_cpp(const map<char, unsigned>& frequencies) {
    priority_queue<shared_ptr<HuffmanNode>, vector<shared_ptr<HuffmanNode>>, CompareNodes> pq;

    // Create leaf nodes and add to priority queue
    for (auto const& [key, val] : frequencies) {
        pq.push(make_shared<HuffmanNode>(key, val));
    }

     if (pq.empty()) return {}; // Handle empty input

    // Build the Huffman tree
    while (pq.size() > 1) {
        shared_ptr<HuffmanNode> left = pq.top(); pq.pop();
        shared_ptr<HuffmanNode> right = pq.top(); pq.pop();

        // Create internal node (use a special char like '$' or 0 if needed, or just rely on left/right pointers)
        shared_ptr<HuffmanNode> internal_node = make_shared<HuffmanNode>('\0', left->frequency + right->frequency);
        internal_node->left = left;
        internal_node->right = right;

        pq.push(internal_node);
    }

    // Generate codes from the tree root
    map<char, string> huffman_codes;
    if (!pq.empty()) {
         generate_codes_recursive_cpp(pq.top(), "", huffman_codes);
    }


    return huffman_codes;
}

int main() {
    // Frequencies from example
    map<char, unsigned> freq = {
        {'A', 5}, {'B', 9}, {'C', 12}, {'D', 13}, {'E', 16}, {'F', 45}
    };

    map<char, string> codes = huffman_coding_cpp(freq);

    cout << "Huffman Codes:" << endl;
    // Sort map by key (char) for consistent output
    for (auto const& [key, val] : codes) { // C++17 structured binding
         if (key != '\0') // Don't print internal node marker if used
            cout << "  '" << key << "': " << val << endl;
    }

    return 0;
}
```

### 5. Diagrams or Flowcharts

**Huffman Tree Diagram:** (See tree in Step 3)

**Algorithm Flow:**

```
Start Huffman(Frequencies)
|
Create Leaf Nodes for each character
Build Min-Priority Queue (PQ) from Leaf Nodes
|
+-----------------------+
| While PQ.size() > 1   |
+-----------------------+
       | Yes
       | Extract min node1 from PQ
       | Extract min node2 from PQ
       | Create newNode (freq = node1.freq + node2.freq)
       | newNode.left = node1
       | newNode.right = node2
       | Insert newNode into PQ
       +-----------------------+
|
root = PQ.extract_min()
Codes = {}
GenerateCodesRecursively(root, "", Codes)
|
End (Return Codes)
```

### 6. Key Formulas and Logic Summary

*   **Goal:** Generate an optimal prefix code (minimum average code length) for a set of characters based on their frequencies.
*   **Average Code Length:** `Sum(frequency(c) * length(code(c)))` for all characters `c`. Huffman coding minimizes this.
*   **Logic:** Greedily merge the two least frequent nodes (characters or subtrees) at each step using a min-priority queue. Build a binary tree representing the codes.
*   **Prefix Property:** Ensured by the tree structure (path from root to leaf is unique).
*   **Time Complexity:** O(N log N), where N is the number of unique characters. Building the frequency map takes O(L) where L is the length of the input text. Building the PQ takes O(N). Each extract-min and insert operation takes O(log N), and there are N-1 merges. Generating codes takes O(N) (proportional to tree size). If L >> N, frequency counting dominates. If N is large, tree building dominates.
*   **Space Complexity:** O(N) for storing frequencies, the tree, and the codes.

### 7. Common Mistakes and Edge Cases

*   **Priority Queue:** Using a max-heap instead of a min-heap, or incorrect comparison logic for nodes.
*   **Tree Building:** Incorrectly assigning left/right children or calculating merged frequencies.
*   **Code Generation