# UGC NET – Unit 7: Data Structures and Algorithms
 
 
## 1. Data Structures
 
### 1.1 Arrays and Applications
 
- **Array:** Contiguous block of memory storing elements of the same type.
- **1D:** `A[n]`; element `A[i]` at address `base + i × size`.
- **2D (Row-major):** `A[m][n]`; `A[i][j]` at `base + (i × n + j) × size`.
- **2D (Column-major):** `A[i][j]` at `base + (j × m + i) × size`.
- **k-D:** General formula — multiply index by product of remaining dimensions.
**Applications:** Polynomial representation, matrix operations, lookup tables, heaps, hash tables.
 
### 1.2 Sparse Matrix
 
- Matrix with most elements zero.
- **Dense storage wastes memory** when non-zero elements are very few.
**Representations:**
- **Triplet (Coordinate) form:** List of `(row, col, value)` for each non-zero.
  - Extra row 0: `(total_rows, total_cols, total_nonzero)`.
  - Space: `O(t)` where t = number of non-zeros.
- **Compressed Sparse Row (CSR):**
  - `values[]`: non-zero values row by row.
  - `col_index[]`: column index of each value.
  - `row_ptr[]`: index in values[] where each row starts; `row_ptr[m+1] = t`.
  - Space: `O(m + t)`.
- **Linked representation:** Circular linked lists for rows and columns.
**Sparse Matrix Transpose (Triplet form):**
```
For each column c (0 to n-1):
    For each element (r, c, v) in row order:
        Output (c, r, v)
```
Time: `O(n × t)` naive; `O(n + t)` with column counts.
 
### 1.3 Stacks
 
- **LIFO (Last In First Out).**
- **Operations:** `push(x)`, `pop()`, `peek()/top()`, `isEmpty()`, `isFull()`.
- **Array implementation:** Top pointer; O(1) for all operations.
- **Linked list implementation:** Push/pop at head; O(1).
**Applications:**
- Function call management (call stack / activation records).
- Expression evaluation and conversion (infix → postfix).
- Balanced parentheses checking.
- DFS (iterative), undo operations, backtracking.
**Infix to Postfix (Shunting-Yard Algorithm):**
```
For each token in infix:
    if operand: output
    if '(': push
    if ')': pop and output until '(' encountered; pop '('
    if operator op:
        while stack not empty AND top is operator with
              higher or equal precedence (left-assoc):
            pop and output
        push op
After all tokens: pop and output remaining operators
```
 
**Postfix Evaluation:**
```
For each token:
    if operand: push
    if operator: pop two operands; apply; push result
Result = top of stack
```
 
### 1.4 Queues
 
- **FIFO (First In First Out).**
- **Operations:** `enqueue(x)`, `dequeue()`, `front()`, `rear()`, `isEmpty()`.
**Circular Queue (Array):**
- Avoids false overflow of linear queue.
- `rear = (rear + 1) % MAX_SIZE` on enqueue.
- `front = (front + 1) % MAX_SIZE` on dequeue.
- Full condition: `(rear + 1) % MAX_SIZE == front`.
- Empty condition: `front == rear`.
- **Useful slots:** `MAX_SIZE - 1` (one slot wasted to distinguish full from empty).
**Double-Ended Queue (Deque):** Insert/delete at both ends.
- Input-restricted: Insert only at rear.
- Output-restricted: Delete only at front.
**Applications:** OS scheduling, BFS, print spooling, producer-consumer buffer.
 
### 1.5 Priority Queues
 
- Each element has a priority; highest-priority element dequeued first.
- **Implementation:** Binary heap (most common), Fibonacci heap, sorted array/list.
**Binary Max-Heap:**
- Complete binary tree; parent ≥ children.
- Stored in array: root at index 1 (or 0).
  - Index 1-based: parent of i = `⌊i/2⌋`; left child = `2i`; right child = `2i+1`.
  - Index 0-based: parent = `⌊(i-1)/2⌋`; left = `2i+1`; right = `2i+2`.
- **Insert:** Add at end; `sift-up (heapify-up)` — O(log n).
- **Extract-Max:** Replace root with last; `sift-down (heapify-down)` — O(log n).
- **Build-Heap:** Apply sift-down to all non-leaf nodes from bottom — O(n).
- **Heap Sort:** Build-heap O(n); extract n elements O(n log n) → Total O(n log n).
**Fibonacci Heap (amortised costs):**
- Insert: O(1), Extract-min: O(log n), Decrease-key: O(1) amortised.
- Used in Dijkstra's and Prim's for better asymptotic performance.
### 1.6 Linked Lists
 
**Singly Linked List:**
- Node: `data | next_pointer`.
- Head pointer to first node; last node's next = NULL.
- Insert at head: O(1). Insert at tail (with tail pointer): O(1). Search: O(n). Delete: O(n) (find predecessor).
**Doubly Linked List:**
- Node: `prev | data | next`.
- Delete given node: O(1) (no need to find predecessor).
**Circular Linked List:**
- Last node's next points to first node.
- Singly or doubly circular.
- Useful for round-robin scheduling.
**Operations Summary:**
 
| Operation | Singly LL | Doubly LL | Array |
|---|---|---|---|
| Insert at head | O(1) | O(1) | O(n) |
| Insert at tail | O(n)/O(1)* | O(1) | O(1)* |
| Delete by value | O(n) | O(n) | O(n) |
| Delete given node | O(n) | O(1) | O(n) |
| Search | O(n) | O(n) | O(1) |
| Access by index | O(n) | O(n) | O(1) |
 
*with tail pointer
 
### 1.7 Trees
 
**Terminology:**
- **Root:** Top node; no parent.
- **Leaf:** No children.
- **Degree of node:** Number of children.
- **Degree of tree:** Maximum degree of any node.
- **Height/Depth of tree:** Length of longest path from root to leaf.
- **Height of node:** Length of longest path from node to leaf.
- **Depth of node:** Length of path from root to node.
- **Level:** Root at level 0 (or 1).
- **Internal node:** Non-leaf node.
- **Ancestor/Descendant:** Nodes on the path to root/descendant.
- **Subtree:** Node and all its descendants.
**Properties of Binary Trees:**
- At most `2^i` nodes at level i (0-indexed).
- At most `2^(h+1) - 1` nodes in a tree of height h.
- Minimum height for n nodes: `h_min = ⌈log₂(n+1)⌉ - 1`.
- For full binary tree with L leaves: internal nodes = L - 1.
- For n nodes: `n = 2L - 1` (full binary tree).
- Number of null pointers in a binary tree with n nodes: `n + 1`.
### 1.8 Forest
 
- **Forest:** Collection of disjoint trees.
- **Conversion (Forest → Binary Tree):**
  - Left child of each node = first child in forest.
  - Right child of each node = next sibling in forest.
- **Conversion (Binary Tree → Forest):** Reverse of above.
- A forest of k trees with n total nodes → binary tree with n nodes where root's right subtree chain has k-1 nodes.
### 1.9 Binary Tree
 
**Types:**
- **Full Binary Tree:** Every node has 0 or 2 children. Leaves = (internal nodes) + 1.
- **Complete Binary Tree:** All levels full except possibly last; last level filled left to right.
- **Perfect Binary Tree:** All internal nodes have 2 children; all leaves at same level. `n = 2^(h+1) - 1`.
- **Skewed Tree:** All nodes have only left (or only right) children; height = n-1.
**Binary Tree Traversals:**
```
Preorder:  Root → Left → Right
Inorder:   Left → Root → Right  (gives sorted order for BST)
Postorder: Left → Right → Root
```
 
**Level Order (BFS):** Use queue; visit node, enqueue children.
 
**Reconstruction from Traversals:**
- Preorder + Inorder → unique binary tree.
- Postorder + Inorder → unique binary tree.
- Preorder + Postorder → NOT unique (unless full binary tree).
**Iterative Traversal:**
- Inorder: Push nodes while going left; pop and visit; go right.
- Preorder: Visit, push right then left.
### 1.10 Threaded Binary Tree
 
- Replace NULL pointers with threads (links to inorder predecessor/successor).
- **Right thread:** Points to inorder successor.
- **Left thread:** Points to inorder predecessor.
- **Header node:** Dummy node as root; left points to tree; right points to itself.
- Enables inorder traversal without stack or recursion.
- Thread indicator bits (boolean) per pointer distinguish threads from actual links.
**Types:**
- **Right-threaded:** Only right threads.
- **Left-threaded:** Only left threads.
- **Fully-threaded:** Both left and right threads.
**Inorder successor in right-threaded tree:**
```
If right_thread(p): successor = right(p)
Else: go to right child; follow left links until left_thread is set
```
 
### 1.11 Binary Search Tree (BST)
 
**Property:** For every node n:
- All keys in left subtree < key(n).
- All keys in right subtree > key(n).
**Operations:**
- **Search:** Compare key; go left if smaller, right if larger. O(h).
- **Insert:** Search for position; insert as leaf. O(h).
- **Delete:**
  - Node is leaf: Remove directly.
  - Node has one child: Replace node with child.
  - Node has two children: Replace with inorder successor (leftmost node in right subtree) or inorder predecessor; delete that node.
**Performance:**
- Average case: `O(log n)` for random keys.
- Worst case: `O(n)` for sorted input (degenerates to linked list).
### 1.12 AVL Tree
 
- **Self-balancing BST** (Adelson-Velsky and Landis, 1962).
- **Balance Factor (BF):** `BF(node) = height(left subtree) - height(right subtree)`.
- **AVL property:** `BF ∈ {-1, 0, +1}` for every node.
- All operations: O(log n) guaranteed.
**Rotations (to restore balance after insert/delete):**
 
**Case 1 — Right-Right (RR):** BF of node = -2; BF of right child = -1 or 0.
- **Left rotation** about node.
**Case 2 — Left-Left (LL):** BF of node = +2; BF of left child = +1 or 0.
- **Right rotation** about node.
**Case 3 — Left-Right (LR):** BF of node = +2; BF of left child = -1.
- **Left rotation** about left child, then **right rotation** about node.
**Case 4 — Right-Left (RL):** BF of node = -2; BF of right child = +1.
- **Right rotation** about right child, then **left rotation** about node.
**Height of AVL tree:** At most `1.44 log₂(n+2)` — O(log n).
 
**Minimum nodes for AVL tree of height h:**
```
N(h) = N(h-1) + N(h-2) + 1
N(0) = 1, N(1) = 2
N(h) ≈ φ^(h+2) / √5  where φ = (1 + √5)/2 ≈ 1.618 (golden ratio)
```
 
### 1.13 B-Tree (Order m)
 
- **Self-balancing multi-way search tree**; used in databases and file systems.
- **Properties (B-Tree of order m):**
  - Every node has at most m children.
  - Every non-root, non-leaf node has at least `⌈m/2⌉` children.
  - Root has at least 2 children (if not a leaf).
  - All leaves at the same level.
  - A node with k children has k-1 keys.
  - Keys within each node are sorted.
**Height:** `h ≤ log_{⌈m/2⌉}((n+1)/2)` → O(log n).
 
**Operations:**
- **Search:** O(log n) comparisons.
- **Insert:** Insert in appropriate leaf; if overflow (m keys in node) → split node; propagate split upward.
- **Delete:** Find key; if in leaf → delete; if in internal node → replace with inorder predecessor/successor from leaf, then delete from leaf; fix underflow by borrowing from sibling or merging.
**Split on overflow (insert):**
- Median key promoted to parent; node split into two nodes with keys before and after median.
### 1.14 B+ Tree
 
- **Variant of B-tree:** All data records at leaves; internal nodes contain only keys for routing.
- **Leaf nodes linked** in a doubly (or singly) linked list for sequential access.
- Internal nodes: At most m-1 keys, m pointers.
- Leaf nodes: At most m-1 key-value pairs, one pointer to next leaf.
**Advantages over B-tree:**
- Efficient range queries (traverse leaf linked list).
- More keys per internal node (no data pointers) → less height → faster search.
- Widely used in RDBMS (MySQL InnoDB, PostgreSQL).
**Properties (B+ Tree of order m):**
- Internal: `⌈m/2⌉ - 1` to `m-1` keys.
- Leaf: `⌈(m-1)/2⌉` to `m-1` keys.
### 1.15 B* Tree
 
- Variant of B-tree; **delay splitting by redistributing** among siblings.
- Non-root nodes at least 2/3 full (vs 1/2 in B-tree).
- Split only when both a node and its sibling are full; then split two nodes into three.
- **Better space utilisation** than B-tree; fewer splits; similar search performance.
### 1.16 Data Structure for Sets
 
**Disjoint Set Union (Union-Find):**
- Maintain collection of disjoint sets; support `find(x)` and `union(x, y)`.
**Implementations:**
- **Array (representative/parent array):** Each element points to representative.
  - `find(x)`: follow parent pointers to root.
  - `union(x, y)`: make root of one a child of root of other.
**Optimisations:**
- **Union by Rank:** Always attach smaller-rank tree under larger-rank tree.
  - Rank ≈ upper bound on height.
- **Union by Size:** Attach smaller tree under larger tree.
- **Path Compression:** During `find`, make all nodes on path point directly to root.
**Combined complexity (Union by Rank + Path Compression):**
- Amortised per operation: `O(α(n))` where `α` = inverse Ackermann function.
- `α(n) ≤ 4` for all practical n; effectively O(1).
**Operations without optimisations:** O(n) worst case.
**With union by rank only:** O(log n).
**With path compression only:** O(log n) amortised.
**With both:** O(α(n)) amortised.
 
**Applications:** Kruskal's MST, connected components, network connectivity, image labelling.
 
### 1.17 Graphs
 
**Definitions:**
- **Graph G = (V, E):** Set of vertices V and edges E.
- **Directed (Digraph):** Edges have direction.
- **Undirected:** Edges have no direction.
- **Weighted:** Edges have weights.
- **Degree:** Number of edges incident to vertex. In digraph: in-degree and out-degree.
- **Handshaking Lemma:** `Σ deg(v) = 2|E|` (undirected).
- **Path:** Sequence of vertices connected by edges.
- **Simple path:** No repeated vertices.
- **Cycle:** Path with same start and end.
- **Connected:** Path exists between every pair of vertices.
- **Strongly Connected (digraph):** Path in both directions between every pair.
**Graph Representations:**
 
**Adjacency Matrix:**
- `A[i][j] = 1` if edge (i,j) exists; 0 otherwise (weight for weighted graph).
- Space: O(V²). Edge check: O(1). Enumerating neighbours: O(V).
**Adjacency List:**
- Array of lists; `adj[i]` = list of neighbours of vertex i.
- Space: O(V + E). Edge check: O(degree). Enumerating neighbours: O(degree).
| Representation | Space | Edge Check | Add Edge | Neighbours |
|---|---|---|---|---|
| Adjacency Matrix | O(V²) | O(1) | O(1) | O(V) |
| Adjacency List | O(V+E) | O(degree) | O(1) | O(degree) |
 
**Types of Graphs:**
- Complete graph Kₙ: `|E| = n(n-1)/2`.
- Bipartite: Vertices partitioned into two sets; edges only between sets.
- DAG (Directed Acyclic Graph): Directed graph with no cycles; enables topological sort.
- Planar: Can be drawn without edge crossings. Euler: V - E + F = 2.
---
 
## 2. Sorting Algorithms
 
### 2.1 Comparison-Based Sorting
 
**Bubble Sort:**
- Repeatedly swap adjacent elements if out of order.
- Passes: n-1; each pass bubbles largest unsorted element to end.
- Time: O(n²) worst and average; O(n) best (already sorted with early termination).
- Space: O(1) in-place.
- Stable.
**Selection Sort:**
- Find minimum in unsorted portion; swap with first unsorted element.
- Time: O(n²) always.
- Space: O(1).
- Not stable (in standard form).
**Insertion Sort:**
- Insert each element into its correct position among already-sorted elements.
- Time: O(n²) worst; O(n) best (sorted input); O(nk) for nearly sorted (k inversions per element).
- Space: O(1).
- Stable. Efficient for small n or nearly sorted arrays.
**Shell Sort:**
- Generalisation of insertion sort with gaps.
- Compare elements at gap h; reduce h over passes (Hibbard, Knuth, Sedgewick gap sequences).
- Time: O(n^(3/2)) to O(n log²n) depending on gap sequence; O(n log n) best (Sedgewick).
- Not stable.
**Merge Sort:**
- Divide array in half; recursively sort; merge two sorted halves.
- **Recurrence:** `T(n) = 2T(n/2) + O(n)` → `T(n) = O(n log n)`.
- Time: O(n log n) all cases.
- Space: O(n) auxiliary.
- Stable. Best for linked lists. External sorting.
**Quick Sort:**
- Choose pivot; partition array (elements < pivot left; > pivot right); recurse.
- **Best/Average:** `T(n) = 2T(n/2) + O(n)` → O(n log n).
- **Worst:** `T(n) = T(n-1) + O(n)` → O(n²) (sorted input with poor pivot).
- Space: O(log n) avg (recursion stack); O(n) worst.
- Not stable (standard). In-place.
- **Pivot strategies:** First/last element (poor), median-of-three (good), random (expected O(n log n)).
- **Expected with random pivot:** O(n log n); probability of O(n²) exponentially small.
**Heap Sort:**
- Build max-heap; extract maximum n times.
- Time: O(n log n) all cases.
- Space: O(1) in-place.
- Not stable.
**Comparison of Sorting Algorithms:**
 
| Algorithm | Best | Average | Worst | Space | Stable |
|---|---|---|---|---|---|
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | No |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | Yes |
| Shell Sort | O(n log n) | O(n^1.5) | O(n²) | O(1) | No |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| Heap Sort | O(n log n) | O(n log n) | O(n log n) | O(1) | No |
| Counting Sort | O(n+k) | O(n+k) | O(n+k) | O(k) | Yes |
| Radix Sort | O(d(n+k)) | O(d(n+k)) | O(d(n+k)) | O(n+k) | Yes |
 
### 2.2 Non-Comparison Sorting (Linear Time)
 
**Counting Sort:**
- Count occurrences of each key; compute prefix sums; place elements.
- Time: O(n + k) where k = range of values.
- Space: O(k).
- Stable. Requires integer keys in small range.
**Radix Sort:**
- Sort by each digit (LSD: least significant first; MSD: most significant first).
- Use stable sort (counting sort) for each digit.
- Time: O(d × (n + k)) where d = digits, k = base (usually 10 or 256).
- Space: O(n + k).
- Stable.
**Bucket Sort:**
- Distribute elements into buckets; sort each bucket (e.g., with insertion sort); concatenate.
- Time: O(n) average for uniformly distributed input; O(n²) worst.
- Space: O(n).
**Lower Bound for Comparison Sorting:** `Ω(n log n)`.
- Any comparison-based sorting algorithm requires at least `n log₂ n` comparisons.
- Decision tree has n! leaves; height ≥ log₂(n!) = Ω(n log n) (by Stirling's approximation: `log₂(n!) ≈ n log₂ n - n log₂ e`).
---
 
## 3. Searching Algorithms
 
### 3.1 Linear Search
 
- Scan all elements; return index of first match.
- Time: O(n) worst and average; O(1) best.
- No prerequisite (works on unsorted arrays).
### 3.2 Binary Search
 
- **Requires sorted array.**
- Compare target with middle element; eliminate half.
- **Recurrence:** `T(n) = T(n/2) + O(1)` → O(log n).
- Time: O(log n) worst and average; O(1) best.
```
lo = 0; hi = n-1
while lo <= hi:
    mid = lo + (hi - lo) / 2    // avoid overflow vs (lo+hi)/2
    if A[mid] == target: return mid
    else if A[mid] < target: lo = mid + 1
    else: hi = mid - 1
return -1
```
 
### 3.3 Hashing
 
- Map keys to indices via hash function; O(1) average search, insert, delete.
**Hash Function Properties:**
- Deterministic, fast to compute.
- Uniform distribution of keys.
- `h(k) ∈ [0, m-1]` where m = table size.
**Common Hash Functions:**
- **Division method:** `h(k) = k mod m`. Choose m = prime, not power of 2.
- **Multiplication method:** `h(k) = ⌊m × (k × A mod 1)⌋` where A = (√5-1)/2 ≈ 0.618 (Knuth).
- **Universal Hashing:** Randomly chosen from family of functions; low collision probability.
- **Polynomial rolling hash (strings):** `h = (c₀ + c₁p + c₂p² + ... + cₙpⁿ) mod m`.
**Collision Resolution:**
 
**Separate Chaining:**
- Each slot holds a linked list of colliding elements.
- **Load factor:** `α = n/m` (n = keys, m = slots).
- Average search time: `O(1 + α)`. If α = O(1), then O(1).
- Worst case: O(n) (all keys hash to same slot).
**Open Addressing (Probing):**
- All elements stored in hash table; on collision, probe alternate slots.
| Method | Probe Sequence | Issue |
|---|---|---|
| **Linear Probing** | `h(k, i) = (h'(k) + i) mod m` | Primary clustering |
| **Quadratic Probing** | `h(k, i) = (h'(k) + c₁i + c₂i²) mod m` | Secondary clustering |
| **Double Hashing** | `h(k, i) = (h₁(k) + i·h₂(k)) mod m` | Best distribution |
 
- **Primary clustering (linear):** Long runs of occupied slots form; slows future searches.
- **Secondary clustering (quadratic):** Same initial hash → same probe sequence.
- **Double hashing:** Requires `h₂(k) ≠ 0` and `gcd(h₂(k), m) = 1` (ensure m is prime).
**Load factor and performance (open addressing):**
- Expected probes for successful search: `(1/α) ln(1/(1-α))`
- Expected probes for unsuccessful search: `1/(1-α)`
- Must keep `α < 1`; performance degrades as α → 1.
**Perfect Hashing:** O(1) worst case; two-level scheme; requires knowing all keys in advance.
 
**Dynamic Perfect Hashing / Cuckoo Hashing:** O(1) worst case lookup; amortised O(1) insert.
 
---
 
## 4. Performance Analysis of Algorithms and Recurrences
 
### 4.1 Time and Space Complexities
 
- **Time complexity:** Number of primitive operations as function of input size n.
- **Space complexity:** Amount of memory used as function of n (auxiliary space + input).
**Counting operations:** Focus on dominant term; ignore constants.
 
### 4.2 Asymptotic Notations
 
**Big-O (Upper Bound):** `f(n) = O(g(n))` if ∃ c > 0, n₀ > 0 such that `f(n) ≤ c·g(n)` ∀ n ≥ n₀.
 
**Big-Omega (Lower Bound):** `f(n) = Ω(g(n))` if ∃ c > 0, n₀ > 0 such that `f(n) ≥ c·g(n)` ∀ n ≥ n₀.
 
**Big-Theta (Tight Bound):** `f(n) = Θ(g(n))` if `f(n) = O(g(n))` and `f(n) = Ω(g(n))`.
 
**Little-o:** `f(n) = o(g(n))` if `lim_{n→∞} f(n)/g(n) = 0` (f grows strictly slower).
 
**Little-omega:** `f(n) = ω(g(n))` if `lim_{n→∞} f(n)/g(n) = ∞` (f grows strictly faster).
 
**Common Complexity Classes (increasing order):**
```
O(1) < O(log log n) < O(log n) < O(√n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2^n) < O(n!) < O(n^n)
```
 
**Properties:**
- `f(n) = Θ(g(n)) ⟺ g(n) = Θ(f(n))`.
- Transitivity: `f = O(g)` and `g = O(h)` ⟹ `f = O(h)`.
- `O(f(n) + g(n)) = O(max(f(n), g(n)))`.
- `log₂(n!) = Θ(n log n)` (Stirling: `n! ≈ √(2πn)(n/e)^n`).
### 4.3 Recurrence Relations
 
**Solving Methods:**
 
**Substitution Method:**
1. Guess form of solution.
2. Prove by mathematical induction.
Example: `T(n) = 2T(n/2) + n`. Guess `T(n) = O(n log n)`. Prove: `T(n) ≤ cn log n`.
 
**Recursion Tree Method:**
- Draw tree of recursive calls; sum work at each level.
- Total cost = (cost per level) × (number of levels).
Example: `T(n) = 2T(n/2) + n`:
- Level 0: n; Level 1: 2×n/2 = n; ...; Level log n: n leaves × O(1) = n.
- Total: n × (log n + 1) = O(n log n).
**Master Theorem:**
For `T(n) = aT(n/b) + f(n)` where a ≥ 1, b > 1:
 
Let `c = log_b(a)`.
 
| Case | Condition | Solution |
|---|---|---|
| Case 1 | `f(n) = O(n^(c-ε))` for some ε > 0 | `T(n) = Θ(n^c)` |
| Case 2 | `f(n) = Θ(n^c · log^k n)` for k ≥ 0 | `T(n) = Θ(n^c · log^(k+1) n)` |
| Case 3 | `f(n) = Ω(n^(c+ε))` for some ε > 0 AND regularity condition: `af(n/b) ≤ δf(n)` for δ < 1 | `T(n) = Θ(f(n))` |
 
**Common Recurrences:**
 
| Recurrence | Algorithm | Solution |
|---|---|---|
| `T(n) = T(n/2) + O(1)` | Binary Search | O(log n) |
| `T(n) = T(n-1) + O(1)` | Linear scan | O(n) |
| `T(n) = 2T(n/2) + O(n)` | Merge Sort | O(n log n) |
| `T(n) = 2T(n/2) + O(1)` | Tree traversal | O(n) |
| `T(n) = T(n-1) + O(n)` | Selection Sort | O(n²) |
| `T(n) = 2T(n-1) + O(1)` | Tower of Hanoi | O(2^n) |
| `T(n) = 4T(n/2) + O(n)` | — | O(n²) |
| `T(n) = 4T(n/2) + O(n²)` | — | O(n² log n) |
| `T(n) = 3T(n/2) + O(n)` | Karatsuba Multiply | O(n^(log₂3)) ≈ O(n^1.585) |
 
**Akra-Bazzi Method:** Generalises Master Theorem for unequal splits.
```
T(n) = Σ aᵢ T(n/bᵢ) + f(n)
Find p such that Σ aᵢ/bᵢᵖ = 1
T(n) = Θ(nᵖ(1 + ∫₁ⁿ f(u)/u^(p+1) du))
```
 
---
 
## 5. Design Techniques
 
### 5.1 Divide and Conquer
 
- **Strategy:** Divide problem into subproblems; solve recursively; combine solutions.
- Subproblems must be smaller and of same type.
**Algorithm Template:**
```
D&C(P):
    if |P| ≤ threshold: solve directly; return
    Divide P into P₁, P₂, ..., Pₖ
    for each Pᵢ: Sᵢ = D&C(Pᵢ)
    Combine S₁, S₂, ..., Sₖ to solve P
    return solution
```
 
**Examples:**
 
**Merge Sort:** Divide in half, sort each, merge. `T(n) = 2T(n/2) + O(n)` → O(n log n).
 
**Quick Sort:** Partition around pivot, recurse on parts. O(n log n) average.
 
**Binary Search:** Eliminate half each step. O(log n).
 
**Strassen's Matrix Multiplication:**
- Standard: O(n³). Strassen: 7 multiplications instead of 8.
- `T(n) = 7T(n/2) + O(n²)` → O(n^(log₂7)) ≈ O(n^2.807).
**Karatsuba Multiplication (large integers):**
- `T(n) = 3T(n/2) + O(n)` → O(n^log₂3) ≈ O(n^1.585).
**Finding Max and Min:**
- Naive: 2(n-1) comparisons.
- D&C: `T(n) = 2T(n/2) + 2`; total `≤ ⌈3n/2⌉ - 2` comparisons.
**Closest Pair of Points:**
- `T(n) = 2T(n/2) + O(n log n)` → O(n log² n); with careful merge O(n log n).
### 5.2 Dynamic Programming (DP)
 
- **Principle of Optimality (Bellman):** Optimal solution contains optimal solutions to subproblems.
- **Overlapping Subproblems:** Same subproblems solved multiple times.
- Store solutions to avoid recomputation: **memoisation** (top-down) or **tabulation** (bottom-up).
**Steps:**
1. Define subproblem and its optimal value.
2. Write recurrence relation.
3. Identify base cases.
4. Compute bottom-up (tabulation) or top-down (memoisation).
5. Reconstruct solution if needed.
**Classic DP Problems:**
 
**Fibonacci:**
```
F(n) = F(n-1) + F(n-2); F(0)=0, F(1)=1
O(n) time, O(n) space (O(1) with space optimisation)
```
 
**0/1 Knapsack:**
```
dp[i][w] = max profit using first i items with capacity w
dp[i][w] = max(dp[i-1][w], dp[i-1][w-wᵢ] + vᵢ)  if wᵢ ≤ w
           dp[i-1][w]                                otherwise
Time: O(nW); Space: O(nW) or O(W) with rolling array.
```
 
**Longest Common Subsequence (LCS):**
```
LCS[i][j] = LCS[i-1][j-1] + 1            if X[i] == Y[j]
           = max(LCS[i-1][j], LCS[i][j-1])  otherwise
Time: O(mn); Space: O(mn).
```
 
**Matrix Chain Multiplication:**
```
m[i][j] = min cost to multiply Aᵢ...Aⱼ
m[i][j] = min_{i≤k<j} { m[i][k] + m[k+1][j] + pᵢ₋₁·pₖ·pⱼ }
Time: O(n³); Space: O(n²).
```
 
**Longest Increasing Subsequence (LIS):**
```
L[i] = length of LIS ending at index i
L[i] = 1 + max{L[j] : j < i and A[j] < A[i]}
Time: O(n²); O(n log n) with patience sorting / binary search.
```
 
**Edit Distance (Levenshtein):**
```
dp[i][j] = edit distance between X[1..i] and Y[1..j]
dp[i][j] = dp[i-1][j-1]               if X[i] == Y[j]
          = 1 + min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) otherwise
Time: O(mn).
```
 
**Floyd-Warshall (All-pairs shortest paths):**
```
D[i][j][k] = shortest path from i to j using vertices 1..k
D[i][j][k] = min(D[i][j][k-1], D[i][k][k-1] + D[k][j][k-1])
Time: O(V³); Space: O(V²).
```
 
**Bellman-Ford:**
```
dist[v] = shortest distance from source s to v
Relax all edges n-1 times.
dist[v] = min(dist[v], dist[u] + w(u,v))
Time: O(VE). Handles negative weights; detects negative cycles.
```
 
**Coin Change:**
```
dp[i] = min coins to make amount i
dp[i] = min{dp[i-cⱼ] + 1} for all coins cⱼ ≤ i
Time: O(n·k) where k = number of coin types.
```
 
**Optimal Binary Search Tree:**
```
e[i][j] = expected search cost for keys kᵢ...kⱼ
w[i][j] = Σ pₗ + Σ qₗ (sum of probabilities)
e[i][j] = min_{i≤r≤j} {e[i][r-1] + e[r+1][j] + w[i][j]}
Time: O(n³); Knuth optimisation → O(n²).
```
 
### 5.3 Greedy Algorithms
 
- Make locally optimal choice at each step; hope for global optimum.
- Works when problem has **greedy choice property** and **optimal substructure**.
- No backtracking; efficient (usually O(n log n) or better).
**Activity Selection Problem:**
- Sort activities by finish time; always pick activity finishing earliest that doesn't conflict.
- Gives maximum number of non-overlapping activities.
- Proof by exchange argument.
**Fractional Knapsack:**
- Sort items by value/weight ratio; take greedily (fractions allowed).
- O(n log n). Greedy works; 0/1 Knapsack requires DP.
**Huffman Coding:**
- Build optimal prefix code for compression.
- **Algorithm:** Use min-heap; repeatedly extract two nodes with smallest frequency; create parent with combined frequency; insert back.
- Time: O(n log n).
- **Optimal:** Huffman code achieves entropy within 1 bit per symbol.
- Expected code length: `Σ fᵢ · lᵢ` where `fᵢ` = frequency, `lᵢ` = code length.
- Shannon entropy lower bound: `H = -Σ pᵢ log₂ pᵢ`.
**Dijkstra's Shortest Path:**
- Greedy; always relax edge from vertex with minimum tentative distance.
- O((V + E) log V) with binary heap; O(V² + E) with array.
- Only correct for non-negative weights.
**Prim's MST:**
- Greedy; grow tree one edge at a time; always add minimum-weight edge connecting tree to non-tree vertex.
- O(E log V) with binary heap.
**Kruskal's MST:**
- Sort edges by weight; add edge if it doesn't create a cycle (use Union-Find).
- O(E log E) = O(E log V).
**Job Sequencing with Deadlines:**
- Maximise profit; each job takes 1 unit; deadline = last slot it can be scheduled.
- Greedy: Sort by profit descending; schedule in latest available slot ≤ deadline.
### 5.4 Backtracking
 
- Systematic search; explore all possibilities; abandon (prune) partial solutions that cannot lead to valid solution.
- State space tree; DFS traversal with pruning.
**Template:**
```
backtrack(state):
    if state is solution: record/return
    for each choice c in generate_choices(state):
        if is_valid(state, c):
            apply(state, c)
            backtrack(state)
            undo(state, c)    // backtrack
```
 
**Classic Problems:**
 
**N-Queens:**
- Place N queens on N×N board; no two attack each other.
- Place one queen per row; prune when column or diagonal conflict.
- Time: O(N!) backtracking; with pruning much faster.
**Sum of Subsets:**
- Find subsets summing to target W.
- Prune if current sum exceeds W or remaining elements cannot reach W.
**Graph Coloring:**
- Colour vertices with k colours; adjacent vertices different colours.
- Pruning: If no valid colour available for vertex → backtrack.
**Hamiltonian Cycle:**
- Visit every vertex exactly once; return to start.
- Backtrack if no unvisited adjacent vertex.
### 5.5 Branch and Bound
 
- Extension of backtracking; used for **optimisation** problems.
- Maintain **upper bound (minimisation: lower bound)** on best solution found.
- **Prune** subtree if its bound cannot improve best known solution.
- Uses BFS or best-first search (unlike DFS in backtracking).
**Bounding Function:**
- Must be computable quickly.
- Must be a valid bound (never worse than actual optimal for that subtree).
**Example — 0/1 Knapsack:**
- Upper bound: Fractional knapsack relaxation on remaining items.
- Branch on each item (include or exclude).
- Prune node if `current_profit + upper_bound ≤ best_so_far`.
**Travelling Salesman Problem (TSP):**
- Lower bound: Minimum spanning tree of unvisited cities + cheapest edges from current and start.
- Branch on next city to visit.
- Time: Exponential but much faster than exhaustive search in practice.
---
 
## 6. Lower Bound Theory
 
### 6.1 Comparison Trees
 
- Model computation as binary decision tree where each internal node is a comparison.
- Each leaf corresponds to one possible outcome (e.g., permutation for sorting).
- **Height of tree = worst-case number of comparisons.**
**Lower Bound for Sorting:**
- n! possible permutations → n! leaves in decision tree.
- Binary tree height ≥ `⌈log₂(n!)⌉` = `Ω(n log n)`.
- **Stirling's Approximation:** `log₂(n!) = n log₂ n - n log₂ e + O(log n) = Ω(n log n)`.
- Therefore, any comparison-based sort requires `Ω(n log n)` comparisons.
**Lower Bound for Searching:**
- Sorted array search: `Ω(log n)` comparisons.
- Unsorted: `Ω(n)`.
**Lower Bound for Finding Maximum:**
- Any algorithm must make at least `n - 1` comparisons (each non-maximum element must lose at least once).
**Lower Bound for Median:**
- `Ω(n)` comparisons required.
- Linear median (Blum et al.): Exact O(n); QuickSelect: O(n) expected.
### 6.2 Lower Bounds through Reductions
 
- If problem A reduces to problem B (A ≤ B), then lower bound of A applies to B.
- `LB(A) ≤ time(B)` → lower bound for B is at least LB(A).
**Example:**
- Sorting ≤ Convex Hull: An O(n log n) lower bound for sorting implies O(n log n) lower bound for convex hull.
- Sorting ≤ Element Uniqueness ≤ Closest Pair: O(n log n) lower bound.
**Adversary Argument:** Adversary maintains consistent assignment to force algorithm into worst case; prove adversary can always maintain consistency for enough steps.
 
---
 
## 7. Graph Algorithms
 
### 7.1 Breadth-First Search (BFS)
 
```
BFS(G, s):
    colour[v] = WHITE for all v; colour[s] = GRAY
    d[s] = 0; π[s] = NULL; queue Q = {s}
    while Q not empty:
        u = dequeue(Q)
        for each neighbour v of u:
            if colour[v] == WHITE:
                colour[v] = GRAY; d[v] = d[u] + 1; π[v] = u
                enqueue(Q, v)
        colour[u] = BLACK
```
 
- **Time:** O(V + E).
- **Discovers:** All vertices reachable from s; shortest paths (unweighted).
- **BFS Tree:** `π[v]` pointers form a tree.
- `d[v]` = shortest path distance (number of edges) from s to v.
**Applications:** Shortest path (unweighted), bipartite testing, connected components, level-order tree traversal.
 
### 7.2 Depth-First Search (DFS)
 
```
DFS(G):
    colour[v] = WHITE for all v; time = 0
    for each v: if colour[v] == WHITE: DFS_VISIT(v)
 
DFS_VISIT(u):
    colour[u] = GRAY; time++; d[u] = time
    for each v adjacent to u:
        if colour[v] == WHITE: π[v] = u; DFS_VISIT(v)
    colour[u] = BLACK; time++; f[u] = time
```
 
- **Time:** O(V + E).
- `d[u]` = discovery time; `f[u]` = finish time.
- **DFS Forest:** Set of DFS trees.
**Edge Classification in DFS:**
- **Tree edge:** Edge (u,v) where v was WHITE when discovered via u.
- **Back edge:** (u,v) where v is ancestor of u (GRAY); indicates cycle.
- **Forward edge:** (u,v) where v is descendant of u (BLACK); only in directed graphs.
- **Cross edge:** All other (u,v) where v is in different DFS tree or already finished.
**Undirected graphs:** Only tree edges and back edges (no forward or cross).
 
**Applications:**
- **Topological Sort:** Run DFS; output vertices in reverse finish time order.
  - Valid only for DAGs. Time: O(V + E).
- **Strongly Connected Components (SCC):** Kosaraju's or Tarjan's algorithm.
**Kosaraju's SCC Algorithm:**
1. Run DFS on G; record finish times.
2. Compute Gᵀ (transpose graph).
3. Run DFS on Gᵀ in decreasing finish time order.
4. Each DFS tree in step 3 = one SCC.
Time: O(V + E).
**Tarjan's SCC Algorithm:**
- Single DFS pass; uses discovery time and low-link values; stack-based.
- Time: O(V + E).
### 7.3 Shortest Paths
 
**Single-Source Shortest Paths:**
 
**Dijkstra's Algorithm (non-negative weights):**
```
dist[s] = 0; dist[v] = ∞ for all v ≠ s
PQ = {(dist[v], v) for all v}
while PQ not empty:
    u = extract_min(PQ)
    for each (u, v) with weight w:
        if dist[u] + w < dist[v]:
            dist[v] = dist[u] + w
            update PQ
```
- Time: O((V + E) log V) with binary heap; O(V² + E) with array; O(V log V + E) with Fibonacci heap.
**Bellman-Ford (handles negative weights):**
```
dist[s] = 0; dist[v] = ∞ for v ≠ s
Repeat V-1 times:
    for each edge (u, v, w):
        if dist[u] + w < dist[v]: dist[v] = dist[u] + w
// Check for negative cycles:
for each edge (u, v, w):
    if dist[u] + w < dist[v]: "negative cycle exists"
```
- Time: O(VE). Detects negative weight cycles.
**DAG Shortest Path:**
- Topological sort; relax edges in topological order.
- Time: O(V + E). Works with negative weights (no cycles).
**All-Pairs Shortest Paths:**
 
**Floyd-Warshall:**
```
D⁰[i][j] = w[i][j] (0 if i==j; ∞ if no edge)
For k = 1 to V:
    For i = 1 to V:
        For j = 1 to V:
            D^k[i][j] = min(D^(k-1)[i][j], D^(k-1)[i][k] + D^(k-1)[k][j])
```
- Time: O(V³). Space: O(V²).
- Works with negative weights; detects negative cycles (D[i][i] < 0).
**Johnson's Algorithm:**
- Reweighting to make all weights non-negative; then run Dijkstra from each vertex.
- Time: O(V² log V + VE). Better than Floyd-Warshall for sparse graphs.
### 7.4 Maximum Flow
 
**Definitions:**
- **Flow network:** Directed graph with capacity `c(u,v)` on each edge.
- **Flow f(u,v):** Satisfies capacity constraint `0 ≤ f(u,v) ≤ c(u,v)` and flow conservation (`flow in = flow out` at non-source/sink vertices).
- **Max flow:** Maximum total flow from source s to sink t.
**Ford-Fulkerson Method:**
```
Initialise f(u,v) = 0 for all edges
while augmenting path p from s to t exists in residual graph Gf:
    c_f(p) = min residual capacity on p
    augment flow along p by c_f(p)
```
- **Residual capacity:** `c_f(u,v) = c(u,v) - f(u,v)` (forward); `c_f(v,u) = f(u,v)` (backward).
- **Residual graph:** Graph of edges with positive residual capacity.
- **Time:** O(E × |f*|) where |f*| = max flow value. Might not terminate for irrational capacities.
**Edmonds-Karp Algorithm:**
- Ford-Fulkerson with BFS to find shortest augmenting path (fewest edges).
- Time: O(VE²). Always terminates; polynomial.
**Max-Flow Min-Cut Theorem:**
- Value of max flow = capacity of min cut.
- **Cut (S, T):** Partition of V with s ∈ S, t ∈ T. Capacity = `Σ c(u,v)` for u ∈ S, v ∈ T.
- Min cut has minimum capacity among all cuts.
**Applications:** Bipartite matching, network reliability, circulation problems.
 
**Push-Relabel Algorithm:**
- O(V² E) or O(V³) with FIFO selection.
- Maintains preflow (can exceed conservation temporarily).
### 7.5 Minimum Spanning Trees (MST)
 
**Definition:** Spanning tree of weighted undirected connected graph with minimum total edge weight.
 
**Generic MST Algorithm (cut property):**
- At each step, add the minimum-weight edge that crosses a cut (S, V-S) where S is a safe set (partial MST).
**Kruskal's Algorithm:**
```
Sort all edges by weight
MST = {}
for each edge (u, v, w) in sorted order:
    if find(u) ≠ find(v):   // not in same component
        MST.add(edge)
        union(u, v)
```
- Time: O(E log E) = O(E log V).
- Uses Union-Find; processes sparse graphs well.
**Prim's Algorithm:**
```
key[v] = ∞ for all v; key[s] = 0; parent[s] = NULL
PQ = all vertices
while PQ not empty:
    u = extract_min(PQ)
    for each (u, v, w):
        if v in PQ and w < key[v]:
            parent[v] = u; key[v] = w; decrease_key(PQ, v)
```
- Time: O((V + E) log V) with binary heap; O(V² + E) with array; O(E + V log V) with Fibonacci heap.
- Works well for dense graphs (adjacency matrix: O(V²)).
**Uniqueness of MST:** MST is unique if all edge weights are distinct.
 
**Number of MSTs:** Can be exponential; determined by cycle matroid structure.
 
---
 
## 8. Complexity Theory
 
### 8.1 Complexity Classes
 
**P (Polynomial Time):**
- Set of decision problems solvable in polynomial time by a deterministic Turing Machine.
- `P = ∪_{k≥0} DTIME(n^k)`.
- Examples: Sorting, shortest path, MST, 2-SAT, bipartite matching.
**NP (Non-deterministic Polynomial Time):**
- Set of decision problems whose solutions are **verifiable** in polynomial time.
- Equivalently: Solvable in polynomial time by a non-deterministic TM.
- `NP = ∪_{k≥0} NTIME(n^k)`.
- Verification: Given certificate (witness), check in polynomial time.
- Examples: SAT, Clique, Vertex Cover, Hamiltonian Cycle, TSP (decision).
**co-NP:**
- Complement of NP. A problem L ∈ co-NP if the complement of L ∈ NP.
- Example: TAUTOLOGY (is every assignment satisfying?).
- `NP ∩ co-NP ⊇ P`. Whether NP = co-NP is open.
**Relationships:**
```
P ⊆ NP ∩ co-NP ⊆ NP ∪ co-NP ⊆ PSPACE ⊆ EXPTIME
P ⊂ EXPTIME (proven)
P = NP? — Open (Millennium Prize Problem)
```
 
### 8.2 NP-Completeness
 
**Polynomial-Time Reduction (A ≤_p B):**
- Problem A reduces to B: Transform any instance of A to instance of B in polynomial time such that YES-instance of A → YES-instance of B, and vice versa.
- If `A ≤_p B` and B solvable in poly time → A solvable in poly time.
**NP-Hard:**
- Problem X is NP-hard if every problem in NP reduces to X.
- `∀ L ∈ NP: L ≤_p X`.
**NP-Complete:**
- X is NP-complete if X ∈ NP and X is NP-hard.
- All NP-complete problems are polynomial-time equivalent.
**Cook-Levin Theorem (1971):** SAT (Boolean satisfiability) is NP-complete.
- First problem proven NP-complete (first NP-hard; trivially in NP).
**Key NP-Complete Problems and Reductions:**
```
SAT
  ↓ (reduce SAT to 3-SAT)
3-SAT
  ↓ ↓ ↓
CLIQUE  VERTEX COVER  INDEPENDENT SET  (all inter-reducible)
  ↓
HAMILTONIAN CYCLE
  ↓
TRAVELLING SALESMAN (TSP)
 
Also NP-complete:
- SUBSET SUM
- PARTITION
- 3-COLORING
- INTEGER PROGRAMMING
- EXACT COVER
```
 
**Reduction Techniques:**
- Show X ∈ NP: Give polynomial-time verifier.
- Show X is NP-hard: Reduce known NP-complete problem Y to X (Y ≤_p X).
**Karp's 21 NP-Complete Problems (1972):** Established core NP-complete set.
 
### 8.3 Implications
 
- If any NP-complete problem is in P → P = NP (all NP problems in P).
- If any NP-complete problem is not in P → P ≠ NP.
- Current consensus: P ≠ NP, but unproven.
**Dealing with NP-hard problems:**
- **Approximation algorithms:** Find near-optimal solution in polynomial time.
- **Parameterised algorithms:** Efficient for small parameter values.
- **Heuristics:** No guarantee but work well in practice.
- **Special cases:** Polynomial for restricted inputs.
---
 
## 9. Selected Topics
 
### 9.1 Number Theoretic Algorithms
 
**GCD (Euclidean Algorithm):**
```
gcd(a, b):
    if b == 0: return a
    return gcd(b, a mod b)
```
- Time: O(log(min(a,b))).
- `gcd(a,b) × lcm(a,b) = a × b`.
**Extended Euclidean Algorithm:**
- Finds x, y such that `ax + by = gcd(a,b)`.
- Used for modular inverse computation.
**Modular Arithmetic:**
- `(a + b) mod m = ((a mod m) + (b mod m)) mod m`.
- `(a × b) mod m = ((a mod m) × (b mod m)) mod m`.
- **Modular Inverse:** `a⁻¹ mod m` exists iff `gcd(a, m) = 1`.
  - Found via Extended Euclidean or Fermat's little theorem.
**Fermat's Little Theorem:** If p is prime and gcd(a,p)=1: `a^(p-1) ≡ 1 (mod p)`.
- Modular inverse: `a⁻¹ ≡ a^(p-2) (mod p)`.
**Euler's Theorem:** `a^φ(n) ≡ 1 (mod n)` if `gcd(a,n) = 1`.
- `φ(n)` = Euler's totient = number of integers 1..n coprime to n.
- `φ(p) = p-1` for prime p.
- `φ(pq) = (p-1)(q-1)` for distinct primes p, q.
**Chinese Remainder Theorem (CRT):**
- System `x ≡ aᵢ (mod mᵢ)` for pairwise coprime `mᵢ` has unique solution mod `M = Πmᵢ`.
- `x = Σ aᵢ × Mᵢ × (Mᵢ⁻¹ mod mᵢ)` where `Mᵢ = M/mᵢ`.
**Modular Exponentiation (Fast Power):**
```
power(base, exp, mod):
    result = 1
    base = base mod mod
    while exp > 0:
        if exp is odd: result = (result * base) mod mod
        exp = exp >> 1
        base = (base * base) mod mod
    return result
```
- Time: O(log exp).
**Primality Testing:**
- **Trial division:** Check divisibility by all primes up to √n. O(√n).
- **Sieve of Eratosthenes:** Find all primes up to n. O(n log log n), Space O(n).
```
  Mark all composites: for each prime p, mark p², p²+p, p²+2p, ...
```
- **Miller-Rabin (probabilistic):** O(k log² n log log n) with k rounds; probability of false positive ≤ 4^(-k).
- **AKS (deterministic):** O(log^12 n) — polynomial but impractical.
**RSA Cryptosystem:**
1. Choose distinct large primes p, q.
2. Compute n = pq, φ(n) = (p-1)(q-1).
3. Choose e: `1 < e < φ(n)`, `gcd(e, φ(n)) = 1`.
4. Compute d: `d·e ≡ 1 (mod φ(n))`.
5. Public key: (e, n). Private key: (d, n).
6. Encrypt: `C = M^e mod n`. Decrypt: `M = C^d mod n`.
- Security based on difficulty of factoring n.
### 9.2 Polynomial Arithmetic
 
**Representation:**
- Coefficient form: `A(x) = Σ aᵢxⁱ`, stored as array `[a₀, a₁, ..., aₙ₋₁]`.
- Value form: `{(x₀, y₀), (x₁, y₁), ..., (xₙ₋₁, yₙ₋₁)}`.
**Degree-n polynomial uniquely determined by n+1 points.**
 
**Polynomial Addition:** O(n). Coefficient-wise.
 
**Naive Polynomial Multiplication:**
```
C[k] = Σ_{j=0}^{k} A[j] × B[k-j]
```
- Time: O(n²).
**Fast Multiplication via FFT:** O(n log n).
 
### 9.3 Fast Fourier Transform (FFT)
 
**Discrete Fourier Transform (DFT):**
```
A^[k] = Σ_{j=0}^{n-1} aⱼ · ωₙ^(jk)    for k = 0, 1, ..., n-1
where ωₙ = e^(2πi/n) (primitive nth root of unity)
```
 
**Inverse DFT:**
```
aⱼ = (1/n) Σ_{k=0}^{n-1} A^[k] · ωₙ^(-jk)
```
 
**Cooley-Tukey FFT (Radix-2):**
- Requires n = power of 2.
- Divide polynomial into even and odd coefficient parts:
```
  A(x) = A_even(x²) + x · A_odd(x²)
  A[k] = A_even[ωₙ²k] + ωₙ^k · A_odd[ωₙ²k]
  A[k + n/2] = A_even[ωₙ²k] - ωₙ^k · A_odd[ωₙ²k]
```
- Recurrence: `T(n) = 2T(n/2) + O(n)` → O(n log n).
**Application to Polynomial Multiplication:**
1. Evaluate A and B at n roots of unity via FFT: O(n log n).
2. Pointwise multiply: C[k] = A[k] × B[k]: O(n).
3. Interpolate C from point form via inverse FFT: O(n log n).
Total: O(n log n).
**Number Theoretic Transform (NTT):**
- FFT over finite fields (mod prime p); avoids floating-point errors.
- Used in competitive programming and cryptography.
### 9.4 String Matching Algorithms
 
**Naive (Brute Force):**
- Try all positions; compare pattern P against text T at each.
- Time: O((n-m+1)×m) = O(nm). Space: O(1).
**Rabin-Karp Algorithm:**
- Hash pattern; compute rolling hash for each window of text.
- Hash(T[s..s+m-1]) matches Hash(P): verify character by character.
- **Rolling hash:** Remove first char, add next char in O(1).
  `h(T[s+1..s+m]) = (d × (h(T[s..s+m-1]) - T[s] × d^(m-1)) + T[s+m]) mod q`
  where d = alphabet size, q = large prime.
- Time: O((n-m+1)×m) worst case (all spurious hits); O(n+m) expected with good hash.
**Knuth-Morris-Pratt (KMP):**
- Precompute **failure function** `π[i]` = length of longest proper prefix of `P[0..i]` that is also a suffix.
- On mismatch at text position j and pattern position k: set `k = π[k-1]` (no restart from 0).
```
Preprocessing π array: O(m)
Matching: O(n)
Total: O(n + m)
```
```
Compute π:
π[0] = 0; k = 0
for i = 1 to m-1:
    while k > 0 and P[k] ≠ P[i]: k = π[k-1]
    if P[k] == P[i]: k++
    π[i] = k
```
 
**Boyer-Moore Algorithm:**
- Right-to-left pattern matching; uses two heuristics:
  - **Bad character heuristic:** On mismatch, shift pattern so bad character aligns with last occurrence in pattern.
  - **Good suffix heuristic:** Shift based on matched suffix.
- Time: O(nm) worst case; O(n/m) best case (sublinear!); O(n + m) for English text.
**Finite Automaton String Matching:**
- Build DFA from pattern; process text in O(n) once built.
- Build time: O(m × |Σ|); matching: O(n). Total: O(m|Σ| + n).
**Aho-Corasick Algorithm:**
- Multi-pattern matching (k patterns simultaneously).
- Build trie + failure links (like KMP for trie).
- Time: O(Σ|Pᵢ| + n + number of matches). Space: O(Σ|Pᵢ| × |Σ|).
**Z-algorithm:**
- `Z[i]` = length of longest substring starting at position i that matches a prefix of string.
- Compute all Z values in O(n).
- Pattern matching: Concatenate P + $ + T; find Z[i] = |P| for i > |P|.
---
 
## 10. Advanced Algorithms
 
### 10.1 Parallel Algorithms
 
**Models:**
- **PRAM (Parallel Random Access Machine):** p processors; shared memory; synchronous.
  - EREW: Exclusive Read Exclusive Write.
  - CREW: Concurrent Read Exclusive Write.
  - CRCW: Concurrent Read Concurrent Write.
**Metrics:**
- **Work W(n):** Total operations = p × T(n) (sequential equivalent).
- **Depth D(n) (Span):** Longest dependency chain = parallel time.
- **Speedup:** `S = T_seq / T_parallel`.
- **Brent's Theorem:** `T_p ≤ D(n) + W(n)/p`.
**Parallel Sorting:**
 
**Parallel Merge Sort:**
- Divide: O(1) parallel. Sort two halves in parallel: `D = O(log n)` stages.
- Parallel merge: O(log n) depth.
- Total depth: O(log² n). Work: O(n log n).
**Bitonic Sort:**
- Sort sequences that are bitonic (first increasing, then decreasing).
- `D(n) = O(log² n)`. Work: `W(n) = O(n log² n)`.
- Perfectly regular; easy to implement in hardware/GPU.
- **Bitonic sequence:** Can be rotated to be monotone.
**Parallel Searching:**
- Parallel binary search on sorted arrays: O(log n / log p) with p processors.
- Parallel search in unsorted: Divide into p chunks; search in O(n/p) = O(n/p).
**Parallel Merging:**
- Merge two sorted arrays of size n: O(log n) depth with n processors.
- Rank each element of one array in other using binary search; merge in O(1) parallel.
**Odd-Even Merge Sort:**
- O(log² n) comparators; O(log² n) depth.
- More practical for hardware than bitonic.
### 10.2 Approximation Algorithms
 
Used for NP-hard optimisation problems; find near-optimal solution in polynomial time.
 
**Approximation Ratio:**
- `ρ(n) = max(A(I)/OPT(I), OPT(I)/A(I))` (for min or max problems).
- A ρ-approximation algorithm guarantees `A(I) ≤ ρ × OPT(I)` (minimisation).
**Vertex Cover (2-approximation):**
```
C = {}
While there exists uncovered edge (u,v):
    Add both u and v to C
Return C
```
- `|C| ≤ 2 × OPT` since optimal must cover all chosen edges.
**Set Cover (H_n approximation):**
- Greedy: Pick set covering most uncovered elements.
- Approximation ratio: `H_n = 1 + 1/2 + ... + 1/n = Θ(log n)`.
- `|C| ≤ H_n × OPT` where `H_n` = n-th harmonic number.
**TSP with Triangle Inequality (1.5-approximation, Christofides):**
1. Compute MST T.
2. Find O = set of odd-degree vertices in T.
3. Find minimum weight perfect matching M on O.
4. Form Euler circuit on T ∪ M.
5. Shortcut repeated vertices.
- Approximation ratio: 1.5.
- Better bound: Christofides-Vaizirani-Mömke (for metric TSP).
**TSP without Triangle Inequality:**
- No polynomial-time constant-factor approximation unless P = NP.
**PTAS (Polynomial Time Approximation Scheme):**
- For any ε > 0, (1+ε)-approximation in time polynomial in n (may be exponential in 1/ε).
- Example: Euclidean TSP (Arora), bin packing.
**FPTAS (Fully Polynomial Time Approximation Scheme):**
- (1+ε)-approximation in time polynomial in both n and 1/ε.
- Example: Knapsack FPTAS: `O(n²/ε)` time.
**Scheduling (Makespan Minimisation):**
- List scheduling: Greedy assignment. Ratio: 2 - 1/m for m machines.
- LPT (Longest Processing Time first): Ratio ≤ 4/3 - 1/(3m).
### 10.3 Randomized Algorithms
 
- Use random numbers to make decisions; provide probabilistic guarantees.
**Types:**
- **Monte Carlo:** Always fast; answer may be incorrect with small probability.
- **Las Vegas:** Always correct; expected runtime is polynomial.
**Randomised QuickSort:**
- Choose pivot uniformly at random.
- Expected time: O(n log n) regardless of input.
- Probability of O(n²): Exponentially small.
**Expected Time Analysis:**
- Let `X_{ij}` = 1 if elements i and j compared; 0 otherwise.
- `E[comparisons] = Σᵢ<ⱼ P[i and j compared] = Σᵢ<ⱼ 2/(j-i+1)`.
- This telescopes to `Σₖ₌₂ⁿ 2/k = O(log n)` per element, total `O(n log n)`.
**Randomised Selection (QuickSelect):**
- Find k-th smallest element.
- Expected time: O(n). Worst case: O(n²).
**Karger's Min-Cut Algorithm:**
- Randomly contract edges; expected O(n²) time; find min cut with probability `≥ 2/n²`.
- Repeat O(n² log n) times; failure probability negligible.
- Full algorithm: O(n² log n) with O(1) success probability.
**Randomised Primality Testing (Miller-Rabin):**
- For each round: Choose random a; test if a is witness to compositeness.
- If composite: at least 3/4 of choices expose it.
- k rounds: probability of false positive ≤ 4^(-k).
**Hashing (Universal):**
- Choose hash function randomly from universal family.
- Collision probability for any two distinct keys ≤ 1/m.
**Skip Lists:**
- Randomised data structure; O(log n) expected search, insert, delete.
- Level of each element chosen randomly (geometric distribution).
- Space: O(n) expected.
**Reservoir Sampling:**
- Sample k items from stream of unknown size n uniformly at random.
- Process first k; for item i > k: include with probability k/i; replace random existing.
- Produces uniform random sample of k items.
---
 
## Quick Recap Table
 
| Topic | Key Formulas / Concepts |
|---|---|
| AVL BF | `BF = h(left) - h(right) ∈ {-1, 0, +1}` |
| AVL Min Nodes | `N(h) = N(h-1) + N(h-2) + 1`; `N(0)=1`, `N(1)=2` |
| B-Tree Order m | ≤ m children; ≥ ⌈m/2⌉ children (non-root); all leaves same level |
| Heap parent/child | 1-indexed: parent=⌊i/2⌋; left=2i; right=2i+1 |
| Build-Heap | O(n) (apply sift-down from bottom); Heap Sort O(n log n) |
| Union-Find (both opt.) | O(α(n)) amortised ≈ O(1) |
| Sorting lower bound | Ω(n log n); from n! leaves in decision tree |
| Master Theorem | `T(n)=aT(n/b)+f(n)`; compare `f(n)` with `n^(log_b a)` |
| Big-O definition | `f(n) ≤ cg(n)` ∀n ≥ n₀; some c,n₀ > 0 |
| Merge Sort | `T(n)=2T(n/2)+O(n)` → O(n log n); stable; O(n) space |
| Quick Sort | O(n log n) avg; O(n²) worst; O(log n) space avg |
| Counting Sort | O(n+k); stable; requires integer keys in [0,k] |
| BFS | O(V+E); shortest path (unweighted); uses queue |
| DFS | O(V+E); topological sort; SCC; uses stack/recursion |
| Dijkstra | O((V+E) log V); non-negative weights only |
| Bellman-Ford | O(VE); handles negative weights; detects negative cycles |
| Floyd-Warshall | O(V³); all-pairs; handles negative weights |
| Kruskal's MST | O(E log E); sort + union-find |
| Prim's MST | O((V+E) log V); priority queue based |
| Ford-Fulkerson | O(E × |f*|); Edmonds-Karp (BFS): O(VE²) |
| Max-Flow Min-Cut | max flow value = min cut capacity |
| KMP | O(n+m) using failure function π |
| Rabin-Karp | O(n+m) expected; rolling hash |
| FFT | O(n log n); polynomial multiplication in O(n log n) |
| Cook-Levin | SAT is first NP-complete problem |
| NP-Complete reductions | SAT → 3-SAT → CLIQUE → Vertex Cover |
| Vertex Cover approx | 2-approximation; greedy edge cover |
| Set Cover approx | H_n = Θ(log n) approximation |
| Christofides TSP | 1.5-approximation (metric TSP) |
| Randomised QuickSort | O(n log n) expected; Las Vegas |
| Miller-Rabin | Monte Carlo; false positive ≤ 4^(-k) per k rounds |
| Huffman | Optimal prefix code; uses min-heap; O(n log n) |
| GCD (Euclid) | O(log(min(a,b))); `gcd(a,b) × lcm(a,b) = ab` |
| Modular Exponentiation | O(log exp) via repeated squaring |
| Fermat's Little | `a^(p-1) ≡ 1 (mod p)` for prime p; gives modular inverse |
