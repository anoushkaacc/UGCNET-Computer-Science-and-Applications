# UGC NET – Unit 1: Discrete Structures and Optimization
---

## 1. Mathematical Logic

### 1.1 Propositional Logic

A **proposition** is a declarative statement that is either TRUE (T) or FALSE (F).

**Logical Connectives:**

| Symbol | Name | Meaning |
|---|---|---|
| `¬p` | Negation | NOT p |
| `p ∧ q` | Conjunction | p AND q |
| `p ∨ q` | Disjunction | p OR q |
| `p → q` | Implication | if p then q |
| `p ↔ q` | Biconditional | p if and only if q |

**Implication equivalences (critical for exams):**
- `p → q ≡ ¬p ∨ q`
- Contrapositive: `p → q ≡ ¬q → ¬p` (logically equivalent)
- Converse: `q → p` (NOT equivalent)
- Inverse: `¬p → ¬q` (NOT equivalent)

### 1.2 Propositional Equivalences

| Law | Expression |
|---|---|
| Identity | `p ∧ T ≡ p`, `p ∨ F ≡ p` |
| Domination | `p ∨ T ≡ T`, `p ∧ F ≡ F` |
| Idempotent | `p ∨ p ≡ p`, `p ∧ p ≡ p` |
| Double Negation | `¬(¬p) ≡ p` |
| De Morgan's | `¬(p ∧ q) ≡ ¬p ∨ ¬q` ; `¬(p ∨ q) ≡ ¬p ∧ ¬q` |
| Absorption | `p ∨ (p ∧ q) ≡ p` ; `p ∧ (p ∨ q) ≡ p` |
| Distributive | `p ∧ (q ∨ r) ≡ (p ∧ q) ∨ (p ∧ r)` |

### 1.3 Normal Forms

- **DNF (Disjunctive Normal Form):** OR of AND clauses. Example: `(p ∧ q) ∨ (¬p ∧ r)`
- **CNF (Conjunctive Normal Form):** AND of OR clauses. Example: `(p ∨ q) ∧ (¬p ∨ r)`
- **Minterm:** A conjunction where every variable appears exactly once (used in DNF).
- **Maxterm:** A disjunction where every variable appears exactly once (used in CNF).
- **Full DNF / Full CNF** – obtained by expanding all minterms/maxterms from truth table.

### 1.4 Predicate Logic

- **Predicate:** A function returning T/F. Example: `P(x)` = "x is even"
- **Universal Quantifier:** `∀x P(x)` — P(x) is true for all x
- **Existential Quantifier:** `∃x P(x)` — P(x) is true for at least one x

**Negation of Quantifiers (De Morgan's for predicates):**
```
¬(∀x P(x)) ≡ ∃x ¬P(x)
¬(∃x P(x)) ≡ ∀x ¬P(x)
```

### 1.5 Nested Quantifiers

- `∀x ∀y P(x,y)` — P holds for all pairs (x, y)
- `∀x ∃y P(x,y)` — For every x, there exists a y such that P(x,y) holds
- Order of quantifiers matters when they are of different types.

### 1.6 Rules of Inference

| Rule | Form | Name |
|---|---|---|
| Modus Ponens | `p, p→q ∴ q` | — |
| Modus Tollens | `¬q, p→q ∴ ¬p` | — |
| Hypothetical Syllogism | `p→q, q→r ∴ p→r` | — |
| Disjunctive Syllogism | `p∨q, ¬p ∴ q` | — |
| Addition | `p ∴ p∨q` | — |
| Simplification | `p∧q ∴ p` | — |
| Conjunction | `p, q ∴ p∧q` | — |
| Resolution | `p∨q, ¬p∨r ∴ q∨r` | — |

---

## 2. Sets and Relations

### 2.1 Set Operations

| Operation | Notation | Definition |
|---|---|---|
| Union | `A ∪ B` | Elements in A or B or both |
| Intersection | `A ∩ B` | Elements in both A and B |
| Difference | `A − B` | Elements in A but not in B |
| Complement | `A'` or `Ā` | Elements in U not in A |
| Symmetric Difference | `A ⊕ B` | `(A − B) ∪ (B − A)` |
| Cartesian Product | `A × B` | Set of all ordered pairs (a, b) |

**Important Identities:**
- `|A ∪ B| = |A| + |B| − |A ∩ B|`
- De Morgan's: `(A ∪ B)' = A' ∩ B'` ; `(A ∩ B)' = A' ∪ B'`

### 2.2 Relations

A relation R from A to B is a subset of `A × B`.

**Representation:** Matrix (0/1), Directed Graph (Digraph).

**Properties of Relations on a Set A:**

| Property | Condition |
|---|---|
| Reflexive | `(a, a) ∈ R` for all `a ∈ A` |
| Irreflexive | `(a, a) ∉ R` for all `a ∈ A` |
| Symmetric | `(a,b) ∈ R → (b,a) ∈ R` |
| Antisymmetric | `(a,b) ∈ R ∧ (b,a) ∈ R → a = b` |
| Transitive | `(a,b) ∈ R ∧ (b,c) ∈ R → (a,c) ∈ R` |

**Closure of Relations:**
- Reflexive closure: add `(a,a)` for all a
- Symmetric closure: add `(b,a)` for every `(a,b)`
- Transitive closure: use Warshall's algorithm

### 2.3 Equivalence Relations

A relation is an **Equivalence Relation** if it is Reflexive + Symmetric + Transitive.

- Partitions the set into **Equivalence Classes**: `[a] = {x ∈ A | xRa}`
- Equivalence classes are **disjoint** and their union is the entire set.

### 2.4 Partial Ordering

A relation is a **Partial Order (POSET)** if it is Reflexive + Antisymmetric + Transitive. Denoted `(A, ≤)`.

- **Hasse Diagram:** Simplified digraph for POSET (transitive and reflexive edges removed).
- **Total Order (Linear Order):** Every pair of elements is comparable.
- **Lattice:** A POSET where every pair has a **LUB (join)** and **GLB (meet)**.

---

## 3. Counting, Mathematical Induction, and Discrete Probability

### 3.1 Basics of Counting

- **Sum Rule:** If A and B are disjoint, `|A ∪ B| = |A| + |B|`
- **Product Rule:** If a task has m ways in step 1 and n ways in step 2: `m × n` ways total.

### 3.2 Pigeonhole Principle

If `n+1` objects are placed into `n` boxes, at least one box contains **2 or more** objects.

**Generalized:** If `N` objects into `k` boxes, at least one box has `⌈N/k⌉` objects.

### 3.3 Permutations and Combinations

- **Permutation (ordered):** `P(n, r) = n! / (n−r)!`
- **Combination (unordered):** `C(n, r) = n! / (r! × (n−r)!)`
- **Permutation with repetition:** `nʳ`
- **Combination with repetition:** `C(n+r−1, r)`
- **Circular permutation:** `(n−1)!`
- **Multinomial:** `n! / (n₁! × n₂! × ... × nₖ!)` for n objects of k types

### 3.4 Inclusion-Exclusion Principle

```
|A ∪ B ∪ C| = |A| + |B| + |C| − |A∩B| − |B∩C| − |A∩C| + |A∩B∩C|
```

General form for n sets:
```
|A₁ ∪ A₂ ∪ ... ∪ Aₙ| = Σ|Aᵢ| − Σ|Aᵢ∩Aⱼ| + Σ|Aᵢ∩Aⱼ∩Aₖ| − ... + (−1)ⁿ⁺¹|A₁∩...∩Aₙ|
```

### 3.5 Mathematical Induction

**Steps:**
1. **Base Case:** Prove P(1) is true.
2. **Inductive Hypothesis:** Assume P(k) is true.
3. **Inductive Step:** Prove P(k+1) is true using the hypothesis.

**Strong Induction:** Assume P(1), P(2), ..., P(k) are all true and prove P(k+1).

**Common results to remember:**
- `1 + 2 + ... + n = n(n+1)/2`
- `1² + 2² + ... + n² = n(n+1)(2n+1)/6`
- `1 + r + r² + ... + rⁿ = (rⁿ⁺¹ − 1)/(r − 1)` for r ≠ 1

### 3.6 Probability

- **Sample Space (S):** Set of all possible outcomes.
- `P(E) = |E| / |S|` for equally likely outcomes.
- `0 ≤ P(E) ≤ 1` ; `P(S) = 1` ; `P(∅) = 0`
- **Complementary:** `P(Ē) = 1 − P(E)`
- **Addition Rule:** `P(A ∪ B) = P(A) + P(B) − P(A ∩ B)`
- **Conditional Probability:** `P(A|B) = P(A ∩ B) / P(B)`
- **Independent Events:** `P(A ∩ B) = P(A) × P(B)`

### 3.7 Bayes' Theorem

```
P(Aᵢ|B) = P(B|Aᵢ) × P(Aᵢ) / Σ[P(B|Aⱼ) × P(Aⱼ)]
```

- `P(Aᵢ)` = Prior probability
- `P(B|Aᵢ)` = Likelihood
- `P(Aᵢ|B)` = Posterior probability

---

## 4. Group Theory

### 4.1 Algebraic Structures

| Structure | Closure | Associativity | Identity | Inverse | Commutativity |
|---|---|---|---|---|---|
| **Groupoid** | Yes | — | — | — | — |
| **Semigroup** | Yes | Yes | — | — | — |
| **Monoid** | Yes | Yes | Yes | — | — |
| **Group** | Yes | Yes | Yes | Yes | — |
| **Abelian Group** | Yes | Yes | Yes | Yes | Yes |

### 4.2 Subgroups

A non-empty subset H of group G is a **subgroup** if:
- Closure: `a, b ∈ H → ab ∈ H`
- Inverse: `a ∈ H → a⁻¹ ∈ H`

**Lagrange's Theorem:** Order of subgroup H divides order of group G. `|H|` divides `|G|`.

### 4.3 Product and Quotient Structures

- **Direct Product:** `G × H = {(g, h) | g ∈ G, h ∈ H}` is a group under componentwise operation.
- **Quotient Group (Factor Group):** `G/N` where N is a **normal subgroup** of G. Elements are cosets of N.
- **Normal Subgroup N:** `gN = Ng` for all `g ∈ G`.

### 4.4 Homomorphism, Isomorphism, Automorphism

| Term | Definition |
|---|---|
| **Homomorphism** | `f: G → H` such that `f(ab) = f(a)f(b)` |
| **Isomorphism** | Bijective homomorphism; G and H are structurally identical |
| **Automorphism** | Isomorphism from G to itself |
| **Kernel** | `ker(f) = {g ∈ G | f(g) = eH}` — always a normal subgroup |

### 4.5 Rings, Integral Domains, and Fields

| Structure | Definition |
|---|---|
| **Ring** | Abelian group under +, associative under ×, distributive |
| **Commutative Ring** | Ring where multiplication is commutative |
| **Integral Domain** | Commutative ring with unity, no zero divisors |
| **Field** | Integral domain where every non-zero element has a multiplicative inverse |

Hierarchy: Field ⊂ Integral Domain ⊂ Commutative Ring ⊂ Ring

### 4.6 Applications of Group Theory

- **Cryptography:** RSA relies on group structure of integers mod n.
- **Error-Correcting Codes:** Linear codes use group/field properties.
- **Symmetry Analysis:** Permutation groups model physical symmetry.
- **Rubik's Cube:** Moves form a group.

---

## 5. Graph Theory

### 5.1 Types of Graphs

| Type | Description |
|---|---|
| **Simple Graph** | Undirected, no self-loops, no multiple edges |
| **Multigraph** | Multiple edges between same pair of vertices allowed |
| **Weighted Graph** | Edges have associated weights/costs |
| **Directed Graph (Digraph)** | Edges have direction |
| **Complete Graph Kₙ** | Every pair of vertices connected; has `n(n−1)/2` edges |

**Handshaking Theorem:** `Σ deg(v) = 2|E|` (sum of all degrees = twice the number of edges)

### 5.2 Paths and Circuits

- **Path:** Sequence of vertices where each adjacent pair is connected by an edge.
- **Simple Path:** No repeated vertices.
- **Circuit/Cycle:** Path that starts and ends at the same vertex.

### 5.3 Shortest Paths in Weighted Graphs

- **Dijkstra's Algorithm:** Single-source shortest path for non-negative weights. `O(V²)` or `O(E log V)` with priority queue.
- **Bellman-Ford Algorithm:** Handles negative weights. `O(VE)`.
- **Floyd-Warshall Algorithm:** All-pairs shortest path. `O(V³)`.

### 5.4 Eulerian Paths and Circuits

- **Eulerian Path:** Visits every **edge** exactly once.
  - Exists if the graph has exactly **0 or 2 vertices of odd degree**.
- **Eulerian Circuit:** Eulerian path that starts and ends at the same vertex.
  - Exists if **all vertices have even degree** and the graph is connected.

### 5.5 Hamiltonian Paths and Circuits

- **Hamiltonian Path:** Visits every **vertex** exactly once.
- **Hamiltonian Circuit:** Hamiltonian path returning to the start.
- No simple necessary and sufficient condition known (NP-complete problem).
- **Dirac's Theorem:** If every vertex has degree `≥ n/2`, a Hamiltonian circuit exists.

### 5.6 Planar Graphs

- A graph is **planar** if it can be drawn without edge crossings.
- **Euler's Formula:** `V − E + F = 2` (V = vertices, E = edges, F = faces including outer face)
- For simple connected planar graphs: `E ≤ 3V − 6`
- **K₅** and **K₃,₃** are the minimal non-planar graphs (Kuratowski's theorem).

### 5.7 Graph Coloring

- **Chromatic Number χ(G):** Minimum colors needed to color vertices such that no adjacent vertices share a color.
- **Four Color Theorem:** Every planar graph has χ(G) ≤ 4.
- **Bipartite Graph:** χ(G) = 2 (if it has at least one edge).
- **Edge Coloring (Chromatic Index):** Minimum colors for edges so no two edges sharing a vertex have the same color.

### 5.8 Bipartite Graphs

- Vertices split into two disjoint sets U and V; every edge goes between U and V.
- A graph is bipartite if and only if it has **no odd-length cycles**.
- **Complete Bipartite Graph Kₘ,ₙ:** Every vertex in U connected to every vertex in V. Has `m × n` edges.

### 5.9 Trees

- A **tree** is a connected, acyclic undirected graph.
- A tree with n vertices has exactly **n − 1 edges**.
- A **rooted tree** has one designated root vertex; defines parent-child relationships.
- **Binary Tree:** Each node has at most 2 children.
- **Full Binary Tree:** Every node has 0 or 2 children.
- **Complete Binary Tree:** All levels full except possibly the last, filled left to right.

**Properties:**
- Height h binary tree has at most `2ʰ⁺¹ − 1` nodes.
- A binary tree with n leaves has `n − 1` internal nodes (full binary tree).

### 5.10 Prefix Codes and Huffman Coding

- **Prefix Code:** No codeword is a prefix of another; avoids ambiguity.
- Represented as a binary tree where codewords are paths from root to leaves.
- **Huffman Coding:** Greedy algorithm; builds optimal prefix code based on character frequencies. Minimizes total encoding length.

### 5.11 Tree Traversals

| Traversal | Order | Use |
|---|---|---|
| **Preorder** | Root → Left → Right | Copy tree, prefix expression |
| **Inorder** | Left → Root → Right | BST sorted output |
| **Postorder** | Left → Right → Root | Delete tree, postfix expression |
| **Level Order** | Level by level (BFS) | Shortest path in unweighted tree |

### 5.12 Spanning Trees and Cut-Sets

- **Spanning Tree:** A subgraph that includes all vertices and is a tree. Has `n − 1` edges.
- **Minimum Spanning Tree (MST):** Spanning tree with minimum total edge weight.
  - **Kruskal's Algorithm:** Sort edges by weight; add edge if it doesn't form a cycle. `O(E log E)`
  - **Prim's Algorithm:** Grow tree from a source; always add minimum-weight edge. `O(V²)` or `O(E log V)`
- **Cut-Set:** Minimal set of edges whose removal disconnects the graph.
- **Cut Vertex (Articulation Point):** Vertex whose removal disconnects the graph.

---

## 6. Boolean Algebra

### 6.1 Boolean Functions and Representations

- Variables take values 0 or 1; operations: AND (·), OR (+), NOT (')
- `A + A' = 1` ; `A · A' = 0` ; `A'' = A`
- **Truth Table → Boolean Expression:** Sum of minterms (SOM) or Product of maxterms (POM)
- **Minterm mᵢ:** Product term where variable is complemented if bit is 0.
- **Maxterm Mᵢ:** Sum term where variable is uncomplemented if bit is 0.
- `F = Σm(minterms)` or `F = ΠM(maxterms)`

### 6.2 Simplification of Boolean Functions

**Using Boolean Identities (algebraic method):**
Key identities: `A + AB = A`, `A + A'B = A + B`, `AB + A'C + BC = AB + A'C`

**Karnaugh Map (K-Map):**
- Grid-based graphical method; group 1s in powers of 2 (1, 2, 4, 8, 16).
- Groups called **implicants**; largest groups = **prime implicants**.
- Wrap-around grouping is allowed (edges are adjacent).
- **Essential Prime Implicant:** Covers at least one minterm not covered by any other prime implicant.

| K-Map grouping | Variables eliminated |
|---|---|
| Group of 2 | 1 variable |
| Group of 4 | 2 variables |
| Group of 8 | 3 variables |

**Quine-McCluskey Method:**
- Tabular minimization; suitable for functions with many variables (automated).
- Find all prime implicants → select minimum cover using prime implicant chart.

---

## 7. Optimization

### 7.1 Linear Programming (LP)

**Mathematical Model:**
- **Objective Function:** Maximize or Minimize `Z = c₁x₁ + c₂x₂ + ... + cₙxₙ`
- **Constraints:** Linear inequalities/equations in decision variables.
- **Non-negativity:** `x₁, x₂, ..., xₙ ≥ 0`

**Graphical Solution (2 variables):**
1. Plot constraint lines on x₁-x₂ plane.
2. Identify feasible region.
3. Evaluate objective function at each **corner (vertex)** of the feasible region.
4. Optimal solution lies at a corner point.

**Simplex Method:**
- Iterative algebraic method for LP with any number of variables.
- Convert inequalities to equations using **slack variables** (for ≤) and **surplus + artificial variables** (for ≥).
- **Basis:** Set of basic variables (= non-zero variables). Start with slack variables.
- **Pivot operation:** Select entering variable (most positive cⱼ − zⱼ for maximization) and leaving variable (minimum ratio test).
- Iterate until no positive `cⱼ − zⱼ` (optimality for maximization).

**Dual Simplex Method:**
- Start with infeasible but optimal (dual feasible) solution.
- Used when adding new constraints to an existing optimal solution.
- Pivot on the most negative basic variable.

**Sensitivity Analysis (Post-Optimality Analysis):**
- Studies effect of changes in objective coefficients (cⱼ), RHS values (bᵢ), or addition of new constraints/variables on the optimal solution.
- **Ranging:** Finding the range within which parameters can vary without changing the optimal basis.

### 7.2 Integer Programming

- LP where some or all decision variables must be integers.
- **Pure Integer Program:** All variables are integers.
- **Mixed Integer Program:** Some variables are integers, some continuous.
- **0-1 (Binary) Integer Program:** Variables restricted to 0 or 1.

**Solution Methods:**
- **Branch and Bound:** Solve LP relaxation; if solution is non-integer, branch by adding constraints (xⱼ ≤ ⌊xⱼ*⌋ and xⱼ ≥ ⌈xⱼ*⌉).
- **Cutting Plane (Gomory's Method):** Add cuts to eliminate fractional solutions without excluding integer ones.

### 7.3 Transportation Model

**Goal:** Minimize total transportation cost from m supply points to n demand points.

**Standard Form:**
- `Minimize Z = Σᵢ Σⱼ cᵢⱼ xᵢⱼ`
- Supply: `Σⱼ xᵢⱼ = aᵢ` ; Demand: `Σᵢ xᵢⱼ = bⱼ` ; `xᵢⱼ ≥ 0`
- **Balanced problem:** `Σaᵢ = Σbⱼ` (add dummy row/column if unbalanced)

**Initial Feasible Solution Methods:**
1. **North-West Corner Method:** Start from top-left; easy but ignores costs.
2. **Least Cost Method:** Allocate to cell with minimum cost first.
3. **Vogel's Approximation Method (VAM):** Uses penalty costs; gives better initial solution.

**Optimality Test:** **MODI Method (Modified Distribution Method)** — checks if current solution is optimal.

### 7.4 Assignment Model

**Goal:** Assign n jobs to n workers to minimize total cost (or maximize total profit). Special case of transportation.

- Cost matrix of size `n × n`.
- **Hungarian Algorithm:**
  1. Row reduction (subtract row minimum from each row).
  2. Column reduction (subtract column minimum from each column).
  3. Cover all zeros with minimum number of lines.
  4. If lines = n, optimal assignment found; else update matrix and repeat.

### 7.5 PERT and CPM

**Comparison:**

| Aspect | PERT | CPM |
|---|---|---|
| Type | Probabilistic | Deterministic |
| Focus | Time | Time + Cost |
| Activity times | 3 estimates | 1 estimate |
| Use case | R&D projects | Construction projects |

**PERT Time Estimates:**
- Optimistic time: `tₒ`
- Most likely time: `tₘ`
- Pessimistic time: `tₚ`
- **Expected time:** `tₑ = (tₒ + 4tₘ + tₚ) / 6`
- **Variance:** `σ² = ((tₚ − tₒ) / 6)²`

**Network Diagram:**
- **Activity-on-Arrow (AoA):** Arrows = activities; nodes = events.
- **Activity-on-Node (AoN):** Nodes = activities; arrows = precedence.
- **Dummy Activity:** Dashed arrow; zero duration; shows logical dependency only.

**Critical Path Calculations:**
- **ES (Earliest Start):** Forward pass — `ES(j) = max{EF(i)}` for all predecessors i
- **EF (Earliest Finish):** `EF = ES + duration`
- **LS (Latest Start):** Backward pass — `LS = LF − duration`
- **LF (Latest Finish):** `LF(i) = min{LS(j)}` for all successors j
- **Total Float:** `TF = LS − ES = LF − EF` (slack available)
- **Free Float:** `FF = ES(successor) − EF(activity)`
- **Critical Path:** Path of activities with **Total Float = 0**; determines minimum project duration.

**Resource Levelling:**
- Rescheduling activities within their float to smooth out resource usage peaks.
- Avoids over-allocation without extending the project duration.

**Cost Consideration (Crashing):**
- **Normal Time/Cost:** Least cost duration.
- **Crash Time/Cost:** Minimum possible duration at extra cost.
- **Cost Slope:** `(Crash Cost − Normal Cost) / (Normal Time − Crash Time)`
- Crash activities on critical path with lowest cost slope first.

---

## Quick Recap Table

| Topic | Key Formulas / Concepts |
|---|---|
| Logic | Modus Ponens, De Morgan's, Contrapositive, CNF/DNF |
| Sets | Inclusion-Exclusion, De Morgan's, Power Set = 2ⁿ |
| Relations | Equivalence = Reflexive + Symmetric + Transitive |
| POSET | Reflexive + Antisymmetric + Transitive; Hasse Diagram |
| Counting | P(n,r) = n!/(n−r)! ; C(n,r) = n!/(r!(n−r)!) |
| Induction | Base + Hypothesis + Step |
| Bayes | P(A\|B) = P(B\|A)P(A)/P(B) |
| Group | Closure + Assoc + Identity + Inverse |
| Lagrange | \|H\| divides \|G\| |
| Graph | Handshaking: Σdeg = 2\|E\| |
| Euler | All even degree → Eulerian Circuit |
| Planar | V − E + F = 2 |
| Tree | n vertices → n−1 edges |
| MST | Kruskal (sort edges) / Prim (grow from source) |
| K-Map | Group 2ᵏ ones; eliminate k variables |
| LP | Optimal at corner of feasible region |
| CPM | Float = 0 on critical path |
| PERT | tₑ = (tₒ + 4tₘ + tₚ)/6 |

---

*Notes prepared for UGC NET Computer Science – Unit 1*
