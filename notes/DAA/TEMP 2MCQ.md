 
← [[DAA]] Home
Okay, here is a comprehensive set of Multiple Choice Questions (MCQs) covering your syllabus, categorized by topic and including the requested variety of question types.

---

**Unit IV – Dynamic Programming and Greedy Techniques**

**1. Computing a Binomial Coefficient**

1.  **[Conceptual]** What is the time complexity of computing C(n, k) using the standard dynamic programming approach with a 2D table?
    A) O(n)
    B) O(k)
    C) O(n * k)
    D) O(n + k)
    *   **Answer:** C
    *   **Explanation:** The algorithm fills an (n+1) x (k+1) table, and each cell computation takes constant time, resulting in O(n * k) time complexity.

2.  **[Numerical]** Using the dynamic programming approach, what is the value of C(5, 2)?
    A) 8
    B) 10
    C) 15
    D) 20
    *   **Answer:** B
    *   **Explanation:** C(5, 2) = C(4, 1) + C(4, 2). C(4, 1)=4, C(4, 2)=6. So, C(5, 2) = 4 + 6 = 10. The DP table systematically computes this.

3.  **[Code - Logic]** Consider the following Python snippet for computing C(n, k):
    ```python
    def solve(n, k, memo):
        if k == 0 or k == n: return 1
        if (n, k) in memo: return memo[(n, k)]
        # Missing recursive calls
        # ...
        memo[(n, k)] = result
        return result
    ```
    What should replace the `# Missing recursive calls` part for a correct top-down DP (memoization) solution?
    A) `result = solve(n, k-1, memo) + solve(n, k, memo)`
    B) `result = solve(n-1, k, memo) + solve(n, k-1, memo)`
    C) `result = solve(n-1, k-1, memo) + solve(n-1, k, memo)`
    D) `result = 1 + solve(n-1, k-1, memo)`
    *   **Answer:** C
    *   **Explanation:** The standard recurrence relation for binomial coefficients is C(n, k) = C(n-1, k-1) + C(n-1, k).

4.  **[Edge Case]** What is the value of C(n, k) if k > n?
    A) 1
    B) n
    C) 0
    D) Undefined
    *   **Answer:** C
    *   **Explanation:** It's impossible to choose k items from a set of n items if k is greater than n. Therefore, the number of ways is 0.

5.  **[Conceptual]** How can the space complexity of the standard DP algorithm for C(n, k) be optimized from O(n*k)?
    A) By using recursion instead of iteration.
    B) It cannot be optimized further.
    C) By realizing only the previous row (or column) is needed, reducing space to O(k) or O(n).
    D) By using memoization instead of tabulation.
    *   **Answer:** C
    *   **Explanation:** To compute row `i` of the DP table, only values from row `i-1` are needed. This allows optimizing the space complexity to O(k) (or O(min(k, n-k))).

**2. Warshall's Algorithm**

1.  **[Conceptual]** What problem does Warshall's algorithm solve?
    A) All-Pairs Shortest Paths
    B) Single-Source Shortest Paths
    C) Minimum Spanning Tree
    D) Transitive Closure of a graph
    *   **Answer:** D
    *   **Explanation:** Warshall's algorithm determines if a path exists between all pairs of vertices (i, j) in a directed graph.

2.  **[Code - Logic]** The core update step in Warshall's algorithm is typically `R[i][j] = R[i][j] OR (R[i][k] AND R[k][j])`. What does this check represent?
    A) If the shortest path from i to j passes through k.
    B) If there's an edge from i to j or an edge from k to j.
    C) If a path exists from i to j using only nodes {1..k-1}, OR if a path exists from i to k and from k to j using only nodes {1..k-1}.
    D) If node k is reachable from node i.
    *   **Answer:** C
    *   **Explanation:** This logic correctly updates the reachability matrix R^(k) based on R^(k-1), considering k as a potential intermediate vertex.

3.  **[Conceptual]** What is the correct order of loops in Warshall's algorithm for it to function correctly?
    A) i, j, k
    B) k, i, j
    C) i, k, j
    D) j, k, i
    *   **Answer:** B
    *   **Explanation:** The intermediate vertex `k` must be in the outermost loop to ensure that when calculating reachability via `k`, the reachability information using vertices up to `k-1` is already complete and correctly computed.

4.  **[Numerical]** Given the adjacency matrix `R = [[0, 1, 0], [0, 0, 1], [0, 0, 0]]` for a graph with vertices {0, 1, 2}. What will be the state of `R` after the iteration `k=1` (considering intermediate node 1)?
    A) `[[0, 1, 0], [0, 0, 1], [0, 0, 0]]`
    B) `[[0, 1, 1], [0, 0, 1], [0, 0, 0]]`
    C) `[[0, 1, 0], [0, 0, 1], [1, 0, 0]]`
    D) `[[0, 1, 0], [0, 1, 1], [0, 0, 0]]`
    *   **Answer:** B
    *   **Explanation:** When k=1: Check `R[i][j] = R[i][j] or (R[i][1] and R[1][j])`. The only update is for `R[0][2]`: `R[0][2] = R[0][2] or (R[0][1] and R[1][2]) = 0 or (1 and 1) = 1`.

**3. Floyd's Algorithm (Floyd-Warshall)**

1.  **[Conceptual]** What is the primary advantage of Floyd-Warshall over running Dijkstra's algorithm from each vertex for the All-Pairs Shortest Path problem?
    A) Floyd-Warshall is faster asymptotically for dense graphs.
    B) Floyd-Warshall can handle negative edge weights (but not negative cycles).
    C) Floyd-Warshall uses less memory.
    D) Floyd-Warshall is easier to implement.
    *   **Answer:** B
    *   **Explanation:** Dijkstra's algorithm fails with negative edge weights, whereas Floyd-Warshall correctly computes APSP as long as no negative cycles exist. Running Dijkstra |V| times is faster for sparse graphs *only* if weights are non-negative.

2.  **[Conceptual]** How does the Floyd-Warshall algorithm detect the presence of a negative cycle?
    A) If `D[i][j]` becomes negative during the process.
    B) If `D[i][k] + D[k][j] < 0`.
    C) If any diagonal element `D[i][i]` becomes negative after the algorithm completes.
    D) If the algorithm runs for more than `n` iterations.
    *   **Answer:** C
    *   **Explanation:** A negative value `D[i][i]` indicates that there is a path from `i` back to `i` with a negative total weight, which signifies a negative cycle reachable from `i`.

3.  **[Numerical]** Consider a graph with edge weights: (0,1, 2), (1,2, -3), (2,0, 4). What is `D[0][2]` after initialization (`D^(0)`) in Floyd-Warshall?
    A) 0
    B) 2
    C) -1
    D) Infinity
    *   **Answer:** D
    *   **Explanation:** The initialization `D^(0)` matrix stores direct edge weights. There is no direct edge from vertex 0 to vertex 2, so the initial distance is infinity.

4.  **[Numerical]** Using the graph from Q3 and Floyd-Warshall, what is `D[0][2]` after the iteration for `k=1`?
    A) Infinity
    B) 2
    C) -1
    D) 1
    *   **Answer:** C
    *   **Explanation:** We check `min(D[0][2], D[0][1] + D[1][2]) = min(inf, 2 + (-3)) = min(inf, -1) = -1`. So, `D[0][2]` becomes -1.

**4. Optimal Binary Search Trees (OBST)**

1.  **[Conceptual]** The primary goal of constructing an Optimal Binary Search Tree (OBST) is to:
    A) Minimize the height of the BST.
    B) Minimize the number of nodes in the BST.
    C) Minimize the expected search cost.
    D) Ensure the BST is perfectly balanced.
    *   **Answer:** C
    *   **Explanation:** OBST aims to arrange keys in a BST such that the average cost (considering search probabilities) to find a key is minimized. This might result in an unbalanced tree if frequent keys are placed near the root.

2.  **[Conceptual]** The dynamic programming recurrence for OBST, `cost(i, j) = min_{i <= r <= j} { cost(i, r-1) + cost(r+1, j) + W(i, j) }`, utilizes which key DP principle?
    A) Greedy Choice Property
    B) Memoization
    C) Optimal Substructure
    D) Overlapping Subproblems only
    *   **Answer:** C
    *   **Explanation:** The formula explicitly shows that the optimal cost for keys `i..j` depends on finding the optimal costs for the subproblems `i..r-1` and `r+1..j` (Optimal Substructure). Overlapping subproblems also exist, justifying DP.

3.  **[Numerical]** Given keys {10, 20} with frequencies {p1=0.6, p2=0.4}. What is the cost of the OBST? (Ignoring dummy keys).
    A) 1.0
    B) 1.4
    C) 1.6
    D) 2.0
    *   **Answer:** B
    *   **Explanation:**
        *   Root=10: Cost = cost(empty) + cost(20) + W(1,2) = 0 + 0.4*1 + (0.6+0.4) = 0.4 + 1.0 = 1.4. Tree: 10 -> 20. Depth(10)=1, Depth(20)=2. Cost = 0.6*1 + 0.4*2 = 0.6+0.8 = 1.4
        *   Root=20: Cost = cost(10) + cost(empty) + W(1,2) = 0.6*1 + 0 + (0.6+0.4) = 0.6 + 1.0 = 1.6. Tree: 20 <- 10. Depth(20)=1, Depth(10)=2. Cost = 0.4*1 + 0.6*2 = 0.4+1.2=1.6.
        Minimum cost is 1.4.

4.  **[Code - Logic]** In the standard O(n^3) DP solution for OBST, the three nested loops typically iterate over:
    A) start key `i`, end key `j`, probability `p`
    B) chain length `l`, start key `i`, root `r`
    C) root `r`, left subtree size `ls`, right subtree size `rs`
    D) start key `i`, root `r`, end key `j`
    *   **Answer:** B
    *   **Explanation:** The common approach iterates over the length `l` of the key chain being considered (from 1 to n), the starting index `i` of the chain, and then tries every possible root `r` within that chain `i..j` where `j=i+l-1`.

**5. 0/1 Knapsack Problem with Memory Functions**

1.  **[Conceptual]** Which statement best describes the 0/1 Knapsack problem?
    A) Select items to maximize weight without exceeding a value limit.
    B) Select fractional amounts of items to maximize value within a weight limit.
    C) Select items, taking each either fully or not at all, to maximize total value within a weight limit.
    D) Arrange items in a sequence to minimize access time.
    *   **Answer:** C
    *   **Explanation:** The "0/1" signifies the constraint that each item must be taken entirely (1) or left entirely (0), aiming to maximize value under a weight constraint.

2.  **[Code - Python]** What is the purpose of the `memo` dictionary in this 0/1 Knapsack Python code?
    ```python
    def knapsack_memo(weights, values, capacity, index, memo):
        state = (index, capacity)
        if state in memo:
            return memo[state]
        # ... rest of logic ...
        memo[state] = result
        return result
    ```
    A) To store the final selection of items.
    B) To store the weights and values.
    C) To avoid recomputing the maximum value for the same subproblems (remaining items and capacity).
    D) To count the number of items considered.
    *   **Answer:** C
    *   **Explanation:** This implements memoization (top-down DP) by storing the result for a given state (defined by the current item index and remaining capacity) to prevent redundant calculations.

3.  **[Numerical]** Given items (Weight, Value): A(2, 3), B(3, 4), C(4, 5) and Knapsack Capacity W=5. What is the maximum value achievable using the 0/1 Knapsack approach?
    A) 5
    B) 7
    C) 8
    D) 9
    *   **Answer:** B
    *   **Explanation:**
        *   {A, B}: Weight=2+3=5, Value=3+4=7
        *   {A, C}: Weight=2+4=6 > 5 (Invalid)
        *   {B, C}: Weight=3+4=7 > 5 (Invalid)
        *   {A}: Weight=2, Value=3
        *   {B}: Weight=3, Value=4
        *   {C}: Weight=4, Value=5
        The maximum value is 7 (by selecting items A and B).

4.  **[Conceptual]** The time complexity O(nW) for the DP solution to 0/1 Knapsack is considered:
    A) Polynomial time
    B) Exponential time
    C) Logarithmic time
    D) Pseudo-polynomial time
    *   **Answer:** D
    *   **Explanation:** The complexity depends on the *numeric value* of the input W (capacity), not just the size (number of bits) of W or the number of items n. If W grows exponentially with n, the time is exponential in the input size. Hence, it's pseudo-polynomial.

**6. Matrix-Chain Multiplication (MCM)**

1.  **[Conceptual]** What quantity does the Matrix-Chain Multiplication algorithm aim to minimize?
    A) The number of matrices in the final product.
    B) The dimensions of the final resulting matrix.
    C) The total number of scalar multiplications required.
    D) The number of parentheses needed.
    *   **Answer:** C
    *   **Explanation:** The order of multiplication affects the total scalar multiplications (cost), even though the final matrix result is the same. MCM finds the minimum cost order.

2.  **[Numerical]** Given matrices A1 (10x20), A2 (20x5), A3 (5x30). Calculate the cost of multiplying `(A1 * A2) * A3`.
    A) 1500
    B) 6000
    C) 4500
    D) 2500
    *   **Answer:** D
    *   **Explanation:**
        *   Cost(A1 * A2) = 10 * 20 * 5 = 1000. Result is 10x5.
        *   Cost((A1A2) * A3) = 10 * 5 * 30 = 1500.
        *   Total Cost = 1000 + 1500 = 2500.

3.  **[Numerical]** Using the matrices from Q2, calculate the cost of multiplying `A1 * (A2 * A3)`.
    A) 2500
    B) 6000
    C) 4000
    D) 9000
    *   **Answer:** C
    *   **Explanation:**
        *   Cost(A2 * A3) = 20 * 5 * 30 = 3000. Result is 20x30.
        *   Cost(A1 * (A2A3)) = 10 * 20 * 30 = 6000.
        *   Total Cost = 3000 + 6000 = 9000.  *Correction:* Rereading the steps. Cost is sum of multiplication costs. Cost(A1*(A2*A3)) calculation is correct but the total is asked. Total Cost = Cost(A2 * A3) + Cost(A1 * result(A2*A3)) = 3000 + (10*20*30) = 3000 + 6000 = 9000. *My original explanation in thought was wrong here, the C++ trace should be double checked as well* Let's rethink the numerical problem Q2 and Q3.
        Q2 cost: Cost(A1*A2) = 10*20*5=1000. Result Dim (10x5). Cost(Result * A3) = 10*5*30 = 1500. Total = 1000 + 1500 = 2500. (Correct)
        Q3 cost: Cost(A2*A3) = 20*5*30=3000. Result Dim (20x30). Cost(A1 * Result) = 10*20*30 = 6000. Total = 3000 + 6000 = 9000. (Correct). Okay the answer key was correct but my second reasoning attempt was confused.

    Let me adjust the option for Q3 to make the intended answer distinct if needed or provide a new numerical. Let's stick with 9000.
    *   **Answer:** D
    *   **Explanation:** Cost(A2 * A3) requires 20x5x30 = 3000 multiplications (resulting in a 20x30 matrix). Multiplying A1 (10x20) by this 20x30 result requires 10x20x30 = 6000 multiplications. Total cost = 3000 + 6000 = 9000.

4.  **[Code - Logic]** The dynamic programming table `m[i][j]` in the MCM algorithm stores:
    A) The dimensions of the matrix resulting from `Ai * ... * Aj`.
    B) The optimal split point `k` for the subproblem `Ai * ... * Aj`.
    C) The minimum number of scalar multiplications needed for `Ai * ... * Aj`.
    D) The frequency of matrix `Ai`.
    *   **Answer:** C
    *   **Explanation:** `m[i][j]` stores the minimum cost (scalar multiplications) for the subproblem of multiplying matrices `i` through `j`. The split point `k` is usually stored in a separate table `s[i][j]`.

**7. Longest Common Subsequence (LCS)**

1.  **[Conceptual]** Which of the following is a subsequence of the string "PROGRAMMING"?
    A) "GRAM"
    B) "POMING"
    C) "PRGMIN"
    D) "RAP"
    *   **Answer:** C
    *   **Explanation:** A subsequence maintains the relative order of characters but doesn't require them to be contiguous. P-R-G-M-I-N appear in that order in "PROGRAMMING". "POMING" doesn't preserve order (M appears after O).

2.  **[Numerical]** What is the length of the Longest Common Subsequence (LCS) between "ABC" and "ACB"?
    A) 1
    B) 2
    C) 3
    D) 0
    *   **Answer:** B
    *   **Explanation:** The common subsequences are "A", "B", "C", "AB", "AC". The longest are "AB" and "AC", both of length 2.

3.  **[Code - C++]** Consider the DP relation for LCS length:
    ```c++
    if (X[i-1] == Y[j-1]) {
        dp[i][j] = 1 + dp[i-1][j-1];
    } else {
        dp[i][j] = /* ??? */;
    }
    ```
    What should replace `/* ??? */`?
    A) `dp[i-1][j-1]`
    B) `max(dp[i-1][j], dp[i][j-1])`
    C) `dp[i-1][j] + dp[i][j-1]`
    D) `0`
    *   **Answer:** B
    *   **Explanation:** If the characters don't match, the LCS length is the maximum of the LCS length excluding the last character of X (`dp[i-1][j]`) and the LCS length excluding the last character of Y (`dp[i][j-1]`).

4.  **[Application]** The 'diff' utility in Unix/Linux, used to compare files, is conceptually based on finding the:
    A) Shortest Common Supersequence
    B) Edit Distance
    C) Longest Common Subsequence
    D) Minimum Spanning Tree
    *   **Answer:** C
    *   **Explanation:** The `diff` utility essentially finds the LCS to identify lines/parts that are common (unchanged), and reports the lines that are not part of the LCS as differences (insertions/deletions). Edit distance is related but calculates the minimum operations to transform one string to another.

**8. Greedy Techniques (General)**

1.  **[Conceptual]** A key property required for a greedy algorithm to guarantee a globally optimal solution is the:
    A) Overlapping Subproblems Property
    B) Memoization Capability
    C) Greedy Choice Property
    D) Negative Weight Intolerance
    *   **Answer:** C
    *   **Explanation:** The Greedy Choice Property states that a globally optimal solution can be reached by repeatedly making locally optimal choices.

2.  **[Conceptual]** Which of the following problems is NOT typically solved optimally using a standard greedy approach?
    A) Prim's algorithm for MST
    B) Huffman Coding
    C) 0/1 Knapsack Problem
    D) Dijkstra's algorithm for SSSP
    *   **Answer:** C
    *   **Explanation:** The standard greedy approach (e.g., taking items with the highest value-to-weight ratio first) works for the *Fractional* Knapsack problem but not necessarily for the 0/1 Knapsack problem, which requires Dynamic Programming.

3.  **[Conceptual]** How does a greedy algorithm differ fundamentally from Dynamic Programming?
    A) Greedy algorithms use recursion, while DP uses iteration.
    B) Greedy algorithms consider only one choice (the locally best), while DP often explores multiple choices for subproblems.
    C) Greedy algorithms have better time complexity.
    D) Dynamic Programming requires overlapping subproblems, while Greedy does not.
    *   **Answer:** B
    *   **Explanation:** The core difference lies in the decision-making process. Greedy commits to the locally optimal choice without looking back, whereas DP explores consequences of different choices for subproblems before combining them for the overall solution.

**9. Minimum Spanning Trees (MST - General)**

1.  **[Conceptual]** A Minimum Spanning Tree (MST) for a connected, weighted, undirected graph G=(V, E) always contains exactly how many edges?
    A) |V|
    B) |E|
    C) |V| - 1
    D) |E| - |V| + 1
    *   **Answer:** C
    *   **Explanation:** Any spanning tree for a graph with |V| vertices must contain exactly |V| - 1 edges to connect all vertices without forming cycles.

2.  **[Conceptual]** If a graph has multiple edges with the same minimum weight crossing a cut, which statement is true about the MST?
    A) The graph cannot have an MST.
    B) The graph might have multiple distinct MSTs.
    C) Any MST must include all minimum-weight edges crossing the cut.
    D) No MST can include more than one minimum-weight edge crossing the cut.
    *   **Answer:** B
    *   **Explanation:** If minimum weight edges are not unique, different valid choices can be made by algorithms like Prim's or Kruskal's, potentially leading to different MSTs, all having the same minimum total weight.

3.  **[Application]** Designing a minimum-cost computer network backbone to connect several data centers, where edge weights represent fiber optic cable costs, is an application of:
    A) All-Pairs Shortest Paths
    B) Maximum Flow
    C) Minimum Spanning Tree
    D) Topological Sorting
    *   **Answer:** C
    *   **Explanation:** The goal is to connect all data centers (vertices) with minimum total cable cost (edge weight) without creating redundant loops (cycles), which is precisely the definition of an MST problem.

**10. Prim's Algorithm**

1.  **[Conceptual]** Prim's algorithm for MST construction builds the tree by:
    A) Starting with an empty graph and adding the cheapest edges one by one, avoiding cycles using a DSU structure.
    B) Starting from a single vertex and iteratively adding the cheapest edge that connects a vertex *in* the tree to a vertex *outside* the tree.
    C) Finding the shortest path from a source to all other vertices.
    D) Sorting all edges and processing them in order.
    *   **Answer:** B
    *   **Explanation:** This describes the core "growing cloud" or vertex-based approach of Prim's algorithm. Option A describes Kruskal's.

2.  **[Numerical]** Consider a graph with vertices A, B, C and edges (A,B,1), (B,C,2), (A,C,3). If Prim's starts at vertex A, which edge is added *second*?
    A) (A, B)
    B) (B, C)
    C) (A, C)
    D) Impossible to determine.
    *   **Answer:** B
    *   **Explanation:** Start at A. Add A to tree. Min edge from A is (A,B,1). Add B to tree. Now consider edges from {A,B} to outside ({C}): (B,C,2) and (A,C,3). The minimum is (B,C,2). So, (B,C) is added second.

3.  **[Code - Logic]** When using a min-priority queue in Prim's algorithm (storing vertices keyed by the minimum edge weight connecting them to the tree), what happens when considering an edge (u, v) where `u` is in the MST and `v` is not, and `weight(u, v)` is less than the current key value stored for `v` in the priority queue?
    A) Add a new entry `(weight(u, v), v)` to the priority queue.
    B) Ignore the edge (u, v) as v is already in the priority queue.
    C) Remove the old entry for `v` and insert the new one `(weight(u, v), v)`.
    D) Decrease the key of `v` in the priority queue to `weight(u, v)`.
    *   **Answer:** D
    *   **Explanation:** The most efficient approach with priority queues that support it (like Fibonacci heaps, or simulation with binary heaps) is to decrease the key of the existing vertex `v` to the new, lower weight. Simply adding a new entry (A) works but is less efficient as it leaves stale entries.

**11. Kruskal's Algorithm**

1.  **[Conceptual]** Kruskal's algorithm requires which data structure to efficiently detect whether adding an edge would create a cycle?
    A) Priority Queue
    B) Stack
    C) Adjacency Matrix
    D) Disjoint Set Union (DSU) / Union-Find
    *   **Answer:** D
    *   **Explanation:** DSU is used to maintain connected components. Before adding an edge (u, v), Kruskal's checks if `Find(u) == Find(v)`. If they are the same, `u` and `v` are already connected, and adding the edge would create a cycle.

2.  **[Conceptual]** The first step typically performed in Kruskal's algorithm is:
    A) Initialize a priority queue with all vertices.
    B) Select an arbitrary starting vertex.
    C) Sort all edges in the graph by weight in non-decreasing order.
    D) Create an adjacency matrix representation of the graph.
    *   **Answer:** C
    *   **Explanation:** Kruskal's algorithm processes edges in increasing order of weight, so sorting them is the crucial first step.

3.  **[Numerical]** Given edges (A,B,5), (B,C,3), (C,A,4), (B,D,2). Which edge is added *first* by Kruskal's algorithm?
    A) (A, B)
    B) (B, C)
    C) (C, A)
    D) (B, D)
    *   **Answer:** D
    *   **Explanation:** Kruskal's considers edges in increasing order of weight. The edge weights are 5, 3, 4, 2. The smallest is 2, corresponding to edge (B, D).

**12. Dijkstra's Algorithm**

1.  **[Conceptual]** Dijkstra's algorithm is guaranteed to find the shortest paths in a weighted graph only if:
    A) The graph is undirected.
    B) The graph is acyclic.
    C) All edge weights are non-negative.
    D) The graph is connected.
    *   **Answer:** C
    *   **Explanation:** The greedy approach of Dijkstra's (permanently finalizing the distance to the closest node) fails if negative edge weights can potentially create shorter paths discovered later.

2.  **[Conceptual]** The "relaxation" step in Dijkstra's algorithm applied to an edge (u, v) involves:
    A) Checking if `u` has been visited.
    B) Adding `v` to the priority queue.
    C) Comparing `dist[v]` with `dist[u] + weight(u, v)` and updating `dist[v]` if the latter is smaller.
    D) Removing edge (u, v) if it forms a cycle.
    *   **Answer:** C
    *   **Explanation:** Relaxation is the core process of updating the shortest distance estimate to vertex `v` if a shorter path is found via vertex `u`.

3.  **[Numerical]** In the graph from Q2 of Prim's (A,B,1), (B,C,2), (A,C,3), running Dijkstra from source A, what is the final shortest distance `dist[C]`?
    A) 1
    B) 2
    C) 3
    D) 4
    *   **Answer:** C
    *   **Explanation:**
        *   Extract A (dist=0). Relax (A,B)->dist[B]=1, Relax (A,C)->dist[C]=3. PQ={(1,B), (3,C)}.
        *   Extract B (dist=1). Relax (B,C)->dist[B]+w(B,C) = 1+2=3. dist[C] is already 3. No update. PQ={(3,C)}.
        *   Extract C (dist=3). Final distance.
        The path A->B->C has cost 1+2=3. The direct path A->C costs 3. Shortest is 3.

4.  **[Code - Error Spotting]** What is a potential issue with the following basic Dijkstra implementation snippet if the graph has many edges?
    ```python
    # Assume graph is adjacency list, dist is initialized
    # ... inside the main loop after extracting u ...
    for neighbor, weight in graph[u]:
        if dist[u] + weight < dist[neighbor]:
             dist[neighbor] = dist[u] + weight
             # Missing priority queue update/insert step
    ```
    A) It doesn't handle negative weights.
    B) It might perform redundant work if `neighbor`'s distance is updated multiple times without efficiently reflecting this in finding the next node to visit.
    C) It doesn't store the parent pointers for path reconstruction.
    D) It assumes the graph is connected.
    *   **Answer:** B
    *   **Explanation:** Without updating the priority queue (either `decrease_key` or adding the new distance and handling stale entries later), the algorithm won't efficiently select the next vertex with the *truly* minimum current distance, potentially degrading performance closer to O(V^2) or worse depending on PQ management. A and C are true statements about this snippet but B highlights the specific issue related to omitting the PQ update.

**13. Huffman Coding**

1.  **[Conceptual]** Huffman coding creates codes that have the "prefix property". This means:
    A) All codes have the same length.
    B) All codes start with '0'.
    C) No code is a prefix of another code.
    D) Codes are assigned alphabetically.
    *   **Answer:** C
    *   **Explanation:** The prefix property ensures that when reading a sequence of codes concatenated together, you can uniquely identify the end of one code and the beginning of the next without ambiguity.

2.  **[Conceptual]** The Huffman coding algorithm greedily builds its tree by repeatedly merging:
    A) The two nodes with the highest frequencies.
    B) The two nodes with the shortest current codes.
    C) A leaf node and an internal node.
    D) The two nodes with the lowest frequencies.
    *   **Answer:** D
    *   **Explanation:** The core greedy step is to combine the two least frequent characters (or subtrees represented by internal nodes) into a new subtree. This ensures less frequent items end up deeper in the tree (longer codes).

3.  **[Numerical]** Given frequencies A:10, B:20, C:30. Which two nodes are merged *first* when building the Huffman tree?
    A) A and B
    B) B and C
    C) A and C
    D) Depends on the priority queue implementation.
    *   **Answer:** A
    *   **Explanation:** The algorithm merges the two nodes with the lowest frequencies. A (10) and B (20) have the lowest frequencies among {10, 20, 30}.

4.  **[Code - Logic]** How are the actual '0' and '1' codes typically generated from a completed Huffman tree?
    A) By reading the frequencies stored in the internal nodes.
    B) By performing a breadth-first traversal of the tree.
    C) By traversing from the root to each leaf node, assigning '0' for left branches and '1' for right branches.
    D) By sorting the characters alphabetically.
    *   **Answer:** C
    *   **Explanation:** The path from the root to a leaf node representing a character defines its Huffman code, with '0' usually representing a step to the left child and '1' a step to the right child.

**14. Single-Source Shortest Paths (SSSP)**

1.  **[Conceptual]** Which algorithm is suitable for finding the shortest paths from a single source vertex in a graph that may contain negative edge weights but no negative cycles?
    A) Dijkstra's Algorithm
    B) Bellman-Ford Algorithm
    C) Prim's Algorithm
    D) Floyd-Warshall Algorithm
    *   **Answer:** B
    *   **Explanation:** Bellman-Ford is designed to handle negative edge weights and can also detect negative cycles. Dijkstra fails with negative weights, Prim's finds MSTs, and Floyd-Warshall finds All-Pairs Shortest Paths.

2.  **[Application]** You need to find the quickest route from your home to your office using a map app. The map represents roads as edges and intersections as vertices, with edge weights representing average travel time. Which algorithm is most likely being used if travel times are always positive?
    A) Kruskal's Algorithm
    B) Floyd-Warshall Algorithm
    C) Bellman-Ford Algorithm
    D) Dijkstra's Algorithm
    *   **Answer:** D
    *   **Explanation:** This is a classic SSSP problem with non-negative weights (time), making Dijkstra the most suitable and efficient choice.

**15. All-Pairs Shortest Paths (APSP)**

1.  **[Conceptual]** If you need to find the shortest path distances between *every* pair of cities on a large map with potentially negative "costs" (e.g., tolls vs subsidies, but no negative cost cycles), which algorithm is generally preferred?
    A) Run Dijkstra from each city.
    B) Run Bellman-Ford from each city.
    C) Use Floyd-Warshall algorithm.
    D) Use Kruskal's algorithm.
    *   **Answer:** C
    *   **Explanation:** Floyd-Warshall directly computes APSP and handles negative edge weights. Running Bellman-Ford |V| times would also work but typically has higher complexity (O(V^2 * E)) compared to Floyd-Warshall (O(V^3)), which is often better for dense graphs or when simplicity is desired. Running Dijkstra |V| times is incorrect due to negative weights.

2.  **[Conceptual]** The time complexity of the Floyd-Warshall algorithm is:
    A) O(V^2)
    B) O(E log V)
    C) O(V * E)
    D) O(V^3)
    *   **Answer:** D
    *   **Explanation:** Floyd-Warshall uses three nested loops, each running up to V (number of vertices) iterations, resulting in O(V^3) time complexity.

**16. Iterative Improvement: The Maximum-Flow Problem**

1.  **[Conceptual]** The Ford-Fulkerson method for finding maximum flow works by iteratively:
    A) Removing edges with the highest capacity.
    B) Finding an augmenting path from source to sink in the residual graph and increasing flow along it.
    C) Calculating the shortest path from source to sink.
    D) Identifying the minimum cut in the graph.
    *   **Answer:** B
    *   **Explanation:** The core idea is to repeatedly find paths (augmenting paths) in the residual graph that still have available capacity, and pushing flow along these paths until no more such paths can be found.

2.  **[Conceptual]** In a flow network, the "residual capacity" of an edge (u, v) represents:
    A) The maximum flow the edge can ever handle.
    B) The current amount of flow passing through the edge.
    C) The additional flow that can still be pushed from u to v.
    D) The capacity required to saturate the network.
    *   **Answer:** C
    *   **Explanation:** The residual capacity `r(u, v) = capacity(u, v) - flow(u, v)` indicates how much more flow can be sent directly along the edge (u, v). The residual graph also includes backward edges representing the ability to "undo" flow.

3.  **[Numerical]** Consider a simple network S -> A -> T with capacities C(S,A)=5 and C(A,T)=3. What is the maximum flow from S to T?
    A) 8
    B) 5
    C) 3
    D) 2
    *   **Answer:** C
    *   **Explanation:** The flow is limited by the bottleneck capacity, which is the edge (A,T) with capacity 3.

4.  **[Conceptual]** The Max-Flow Min-Cut Theorem states that:
    A) The maximum flow value is equal to the capacity of the minimum s-t cut.
    B) The maximum flow value is always less than the minimum cut capacity.
    C) The minimum cut capacity is equal to the sum of all edge capacities.
    D) The maximum flow path is the shortest path in the residual graph.
    *   **Answer:** A
    *   **Explanation:** This is a fundamental theorem connecting the maximum flow achievable from source 's' to sink 't' and the minimum capacity of a set of edges whose removal disconnects 's' from 't'.

**17. Lower-Bound Theory and Limitations of Algorithmic Power**

1.  **[Conceptual]** The notation Ω(n log n) for comparison-based sorting algorithms represents:
    A) The average-case time complexity.
    B) The best-case time complexity.
    C) A theoretical lower bound on the worst-case time complexity.
    D) The space complexity.
    *   **Answer:** C
    *   **Explanation:** Lower-bound theory establishes the minimum amount of work any algorithm of a certain type (e.g., comparison sorts) must perform in the worst case. Ω notation provides this asymptotic lower bound.

2.  **[Conceptual]** A problem is considered "undecidable" if:
    A) It belongs to the complexity class P.
    B) No algorithm can solve all instances of the problem correctly in any finite amount of time.
    C) It belongs to the complexity class NP.
    D) Only exponential-time algorithms exist for it.
    *   **Answer:** B
    *   **Explanation:** Undecidable problems, like the Halting Problem, are fundamentally impossible to solve algorithmically for all possible inputs.

3.  **[Conceptual]** P versus NP is a major unsolved question in computer science. If P=NP, it would imply that:
    A) All problems can be solved in polynomial time.
    B) Problems whose solutions can be verified quickly can also be solved quickly.
    C) NP-complete problems are actually undecidable.
    D) Greedy algorithms are always optimal.
    *   **Answer:** B
    *   **Explanation:** P is the class of problems solvable in polynomial time. NP is the class of problems whose solutions can be verified in polynomial time. If P=NP, it means any problem whose solution is easy to check is also easy to solve.

4.  **[Application]** When faced with an NP-hard optimization problem for which finding the absolute optimal solution is computationally infeasible for large inputs, a common practical strategy is to use:
    A) A greedy algorithm (which might not be optimal).
    B) An approximation algorithm (which guarantees a solution within some factor of optimal).
    C) A backtracking algorithm (guaranteed to find optimal, but potentially slow).
    D) Both A and B are common strategies.
    *   **Answer:** D
    *   **Explanation:** Both simple greedy heuristics and more sophisticated approximation algorithms (with performance guarantees) are employed when exact solutions to NP-hard problems are too slow to compute in practice. Backtracking is often too slow for large NP-hard instances.

---

**Unit V – Backtracking**

**18. n-Queens Problem**

1.  **[Conceptual]** The n-Queens problem is an example of which type of problem paradigm?
    A) Divide and Conquer
    B) Greedy Algorithm
    C) Dynamic Programming
    D) Backtracking / Constraint Satisfaction
    *   **Answer:** D
    *   **Explanation:** It involves satisfying constraints (non-attacking positions) and explores potential solutions incrementally, backtracking when a constraint is violated.

2.  **[Numerical]** In a 4x4 board, if a queen is placed at (1, 1) (using 0-based indexing), which of the following positions is *safe* for placing another queen?
    A) (0, 2)
    B) (2, 0)
    C) (3, 3)
    D) (2, 3)
    *   **Answer:** D
    *   **Explanation:**
        *   (0, 2): Unsafe, diagonal conflict `abs(0-1) == abs(2-1)`.
        *   (2, 0): Unsafe, diagonal conflict `abs(2-1) == abs(0-1)`.
        *   (3, 3): Unsafe, diagonal conflict `abs(3-1) == abs(3-1)`.
        *   (2, 3): Row 2 != 1, Col 3 != 1, `abs(2-1)=1`, `abs(3-1)=2`. Safe.

3.  **[Code - Logic]** The `isSafe(board, row, col)` function in the typical backtracking solution for N-Queens (where `board[c]` holds the row for queen in column `c`) primarily needs to check for conflicts in:
    A) The same row, same column, and both diagonals for `prev_col > col`.
    B) The same row and both diagonals for `prev_col < col`.
    C) The same column only for `prev_col < col`.
    D) All other `n*n` squares.
    *   **Answer:** B
    *   **Explanation:** Since queens are placed column by column, we only need to check against queens in previous columns (`prev_col < col`). Column conflicts are implicitly avoided. We check for queens in the same row (`board[prev_col] == row`) and on the same diagonals (`abs(board[prev_col] - row) == abs(prev_col - col)`).

4.  **[Conceptual]** Backtracking for N-Queens explores a state-space tree. What does pruning the tree correspond to?
    A) Finding a complete solution.
    B) Deciding not to place a queen in a square because it is attacked by a previously placed queen.
    C) Running out of columns to place queens in.
    D) Sorting the rows before attempting placement.
    *   **Answer:** B
    *   **Explanation:** Pruning means abandoning a branch of the search because the current partial solution violates constraints (`isSafe` returns false), making it impossible for that branch to lead to a valid complete solution.

**19. Hamiltonian Circuit Problem**

1.  **[Conceptual]** A necessary (but not sufficient) condition for a graph to have a Hamiltonian Circuit is that the graph must be:
    A) Bipartite
    B) Acyclic
    C) Complete
    D) Connected
    *   **Answer:** D
    *   **Explanation:** A Hamiltonian Circuit must visit every vertex. If the graph is disconnected, it's impossible to visit vertices in different components within a single circuit.

2.  **[Numerical]** Consider a path currently built by the backtracking algorithm: `[0, 1, 3]`. If the next vertex to consider is 2, and the neighbors of 3 are {0, 4}, can vertex 2 be added next? (Assume a graph where 0-1, 1-3, 0-3, 3-4 edges exist).
    A) Yes, if vertex 2 hasn't been visited.
    B) No, because vertex 2 is not adjacent to vertex 3.
    C) No, because vertex 0 has already been visited.
    D) Yes, because vertex 2 creates a cycle.
    *   **Answer:** B
    *   **Explanation:** The algorithm tries to extend the path from the *last* vertex added (vertex 3 in this case). Since 2 is not adjacent to 3 according to the neighbours list, it cannot be added directly after 3.

3.  **[Code - Logic]** In the backtracking algorithm for the Hamiltonian Circuit problem, when does the algorithm typically backtrack?
    A) Only when a complete circuit is found.
    B) When the current path length equals the number of vertices.
    C) When the algorithm tries to add a vertex `v` that is either already visited or not adjacent to the current end of the path.
    D) When all possible next vertices have been explored from the current end of the path, and none led to a solution.
    *   **Answer:** D
    *   **Explanation:** Backtracking occurs when a dead end is reached – the current path cannot be extended further according to the rules (adjacent, unvisited) and the base case (a full circuit) has not been met. C describes conditions where *a specific choice* is rejected, but backtracking occurs after *all choices* from a state fail.

4.  **[Conceptual]** The Hamiltonian Circuit problem is known to be:
    A) Solvable in polynomial time using Dynamic Programming.
    B) Solvable in logarithmic time.
    C) NP-complete.
    D) Undecidable.
    *   **Answer:** C
    *   **Explanation:** Finding a Hamiltonian Circuit is a classic NP-complete problem, meaning no known polynomial-time algorithm exists, and it's suspected that none does. Backtracking is an exponential-time approach.

**20. Subset-Sum Problem**

1.  **[Conceptual]** The two main recursive choices considered for each element in the standard backtracking algorithm for the Subset Sum problem are:
    A) Include the element twice OR exclude it.
    B) Include the element OR exclude the element.
    C) Include the element OR move to the next element with the same sum.
    D) Include the element with positive sign OR include with negative sign.
    *   **Answer:** B
    *   **Explanation:** For each element, the algorithm explores the consequences of including it in the potential subset (adding its value to the current sum) and the consequences of excluding it (leaving the sum unchanged), moving to the next element in both cases.

2.  **[Numerical]** Given the set S = {2, 5, 3} and target sum T = 7. Which subset, if any, sums to T?
    A) {2, 5}
    B) {2, 3}
    C) {5, 3}
    D) No subset sums to 7.
    *   **Answer:** A
    *   **Explanation:** 2 + 5 = 7.

3.  **[Code - Python]** Analyze the following backtracking snippet for Subset Sum:
    ```python
    def solve(S, T, i, current_sum):
        if current_sum == T: return True
        if i == len(S) or current_sum > T: return False
        # Recursive calls missing
        return # ???
    ```
    What logical combination should replace `# ???`?
    A) `solve(S, T, i+1, current_sum + S[i]) AND solve(S, T, i+1, current_sum)`
    B) `solve(S, T, i+1, current_sum + S[i]) OR solve(S, T, i+1, current_sum)`
    C) `solve(S, T, i, current_sum + S[i])`
    D) `solve(S, T, i+1, current_sum)`
    *   **Answer:** B
    *   **Explanation:** A solution exists if *either* including the current element `S[i]` leads to a solution *OR* excluding it leads to a solution.

4.  **[Conceptual]** Why is the Subset Sum problem (decision version) often solved using Dynamic Programming in practice, even though a backtracking solution exists?
    A) Backtracking cannot guarantee finding a solution.
    B) Dynamic Programming can handle negative numbers, unlike backtracking.
    C) Backtracking explores redundant subproblems (overlapping subproblems), which DP avoids via memoization or tabulation.
    D) Dynamic Programming has a better space complexity.
    *   **Answer:** C
    *   **Explanation:** The state `(index, current_sum)` can be reached through many different combinations of including/excluding earlier elements. Pure backtracking recalculates these, while DP stores the result (True/False) for each state, drastically improving efficiency for many inputs.

---