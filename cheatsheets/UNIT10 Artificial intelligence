# UGC NET – Unit 10: Artificial Intelligence (AI)

---

## 1. Approaches to AI

### 1.1 Turing Test

- Proposed by **Alan Turing (1950)** in "Computing Machinery and Intelligence."
- A human interrogator communicates via text with a human and a machine.
- If the interrogator cannot distinguish the machine from the human, the machine is considered **intelligent**.
- **Capabilities required:** Natural language processing, knowledge representation, reasoning, learning.
- **Criticism:** Tests only behavioural imitation, not understanding (Chinese Room Argument by Searle).

### 1.2 Rational Agent Approach

- An **agent** is anything that perceives its environment via sensors and acts via actuators.
- A **rational agent** selects actions that maximize its expected performance measure based on percept history and built-in knowledge.
- **PEAS framework:** Performance measure, Environment, Actuators, Sensors.

**Environment Types:**

| Property | Types |
|---|---|
| Observability | Fully vs Partially observable |
| Determinism | Deterministic vs Stochastic |
| Episodes | Episodic vs Sequential |
| Dynamism | Static vs Dynamic |
| Continuity | Discrete vs Continuous |
| Agents | Single vs Multi-agent |

### 1.3 State Space Representation

- A problem is represented as a **state space graph.**
- **Components:**
  - **Initial State:** Starting configuration.
  - **State Space:** Set of all states reachable from the initial state.
  - **Operators/Actions:** Functions that transform one state into another.
  - **Goal Test:** Condition that determines if a state is the goal.
  - **Path Cost:** Numeric cost assigned to each path.

- **Solution:** A sequence of actions leading from the initial state to a goal state.
- **Optimal Solution:** A solution with the lowest path cost.

**Example — 8-Puzzle:**
- State: Configuration of 8 tiles on a 3×3 grid.
- Operators: Move blank Up, Down, Left, Right.
- Goal: Specific tile arrangement.

### 1.4 Search Strategies

**Uninformed (Blind) Search:**

| Algorithm | Data Structure | Complete | Optimal | Time | Space |
|---|---|---|---|---|---|
| BFS | Queue | Yes | Yes (unit cost) | O(b^d) | O(b^d) |
| DFS | Stack | No | No | O(b^m) | O(b×m) |
| DLS | Stack | No | No | O(b^l) | O(b×l) |
| IDDFS | Stack | Yes | Yes (unit cost) | O(b^d) | O(b×d) |
| UCS | Priority Queue | Yes | Yes | O(b^(1+C*/ε)) | O(b^(1+C*/ε)) |
| Bidirectional | Queue | Yes | Yes | O(b^(d/2)) | O(b^(d/2)) |

Where: b = branching factor, d = depth of shallowest solution, m = maximum depth, l = depth limit, C* = optimal cost, ε = minimum step cost.

### 1.5 Heuristic Search Techniques

A **heuristic function** `h(n)` estimates the cost from node n to the goal.

**Properties:**
- **Admissible:** `h(n) ≤ h*(n)` for all n, where h*(n) is the true cost. Guarantees optimality in A*.
- **Consistent (Monotone):** `h(n) ≤ c(n, a, n') + h(n')` for every successor n'. Implies admissibility.

**Greedy Best-First Search:**
- Expands node with smallest `h(n)`.
- Not optimal; not complete (may loop).
- Evaluation function: `f(n) = h(n)`

**A* Search:**
- Evaluation function: `f(n) = g(n) + h(n)`
  - `g(n)` = actual cost from start to n.
  - `h(n)` = estimated cost from n to goal.
  - `f(n)` = estimated total cost of path through n.
- Complete and optimal if h(n) is admissible.
- With consistent h(n), A* never re-expands a node.
- Time/Space complexity: O(b^d) in worst case.

**Common Heuristics:**
- **Misplaced Tiles:** Count of tiles not in goal position. (Admissible)
- **Manhattan Distance:** `h(n) = Σ |row_current - row_goal| + |col_current - col_goal|` (Admissible, more informed)

**IDA* (Iterative Deepening A*):**
- Like IDDFS but uses f(n) = g(n) + h(n) as the cutoff.
- Linear space complexity: O(b×d).

**Hill Climbing:**
- Move to best neighbouring state; stop when no better neighbour.
- Problems: Local maxima, plateaus, ridges.
- **Simulated Annealing:** Accepts worse states with probability `e^(ΔE/T)` where T decreases over time (temperature schedule). Escapes local optima.

**Beam Search:**
- Keep only the best k states at each level.
- Not complete or optimal; uses less memory than BFS.

### 1.6 Game Playing

- **Two-player, zero-sum, perfect information games** (e.g., Chess, Tic-Tac-Toe).
- Zero-sum: One player's gain is the other's loss.

### 1.7 Min-Max Search

- Models game as a tree; **MAX** player maximises score; **MIN** player minimises score.
- **Terminal state:** Game over; evaluated by utility/payoff function.

**Algorithm:**
```
MINIMAX(node, depth, isMaximising):
    if terminal(node) or depth == 0:
        return UTILITY(node)
    if isMaximising:
        value = -∞
        for each child of node:
            value = max(value, MINIMAX(child, depth-1, False))
        return value
    else:
        value = +∞
        for each child of node:
            value = min(value, MINIMAX(child, depth-1, True))
        return value
```

- **Time complexity:** O(b^m)
- **Space complexity:** O(b×m)

### 1.8 Alpha-Beta Cutoff (Pruning)

- Prunes branches that cannot influence the final decision, reducing search space.
- **α (alpha):** Best value MAX can guarantee along current path (initialized to -∞).
- **β (beta):** Best value MIN can guarantee along current path (initialized to +∞).

**Pruning Conditions:**
- At a MIN node: if current value ≤ α → prune remaining children (α cut-off).
- At a MAX node: if current value ≥ β → prune remaining children (β cut-off).

```
ALPHA-BETA(node, depth, α, β, isMaximising):
    if terminal(node) or depth == 0:
        return UTILITY(node)
    if isMaximising:
        value = -∞
        for each child of node:
            value = max(value, ALPHA-BETA(child, depth-1, α, β, False))
            α = max(α, value)
            if α ≥ β: break   -- β cut-off
        return value
    else:
        value = +∞
        for each child of node:
            value = min(value, ALPHA-BETA(child, depth-1, α, β, True))
            β = min(β, value)
            if α ≥ β: break   -- α cut-off
        return value
```

- **Best case (perfect ordering):** O(b^(m/2)) — doubles search depth for same computation.
- **Worst case:** O(b^m) — same as minimax.

---

## 2. Knowledge Representation

### 2.1 Logic-Based Representation

**Propositional Logic:**
- Facts represented as propositions; connectives: ∧, ∨, ¬, →, ↔.
- Limited expressiveness; cannot represent objects and relationships.

**First-Order Logic (FOL) / Predicate Logic:**
- Uses predicates, constants, variables, functions, and quantifiers (∀, ∃).
- Example: `∀x (Human(x) → Mortal(x))`
- **Inference Rules:** Modus Ponens, Resolution, Unification.

**Unification:** Finding a substitution θ such that two expressions become identical.
- `Unify(Knows(John, x), Knows(John, Jane))` → `{x/Jane}`

**Resolution Principle:**
- `(P ∨ Q)` and `(¬P ∨ R)` → resolve to `(Q ∨ R)`.
- For automated theorem proving; convert to CNF first.

### 2.2 Semantic Networks

- Graph-based representation of knowledge.
- **Nodes:** Concepts/objects.
- **Arcs:** Relationships (IS-A, HAS-A, PART-OF, etc.).
- **IS-A arc:** Represents inheritance/class hierarchy.
- **Inheritance:** Properties propagate from superclass to subclass.
- **Limitation:** Difficult to represent complex relationships, negation, quantification.

### 2.3 Frames

- Proposed by **Marvin Minsky (1975)**.
- A frame is a data structure with **slots** (attributes) and **fillers** (values).
- Supports **default values**, **inheritance**, and **procedural attachment** (if-needed, if-added demons).

```
Frame: Car
  Slots:
    IS-A:     Vehicle
    Has-Engine: True  (default)
    Colour:   (ask-user)
    No-of-Wheels: 4 (default)
```

### 2.4 Rules (Production Systems)

- Knowledge represented as **IF-THEN** rules.
- `IF condition THEN action`
- **Components:** Working memory (current facts), Rule base (knowledge), Inference engine.
- **Forward Chaining (Data-Driven):** Start from facts; apply rules; derive conclusions. Used in planning.
- **Backward Chaining (Goal-Driven):** Start from goal; find rules that conclude it; satisfy conditions. Used in diagnosis.

### 2.5 Scripts

- Proposed by **Roger Schank**.
- Describe stereotyped sequences of events in specific contexts.
- **Components of a Script:**
  - **Entry Conditions:** What must be true before script starts.
  - **Roles:** Participants.
  - **Props:** Objects involved.
  - **Track:** Variant of the script.
  - **Scenes:** Sequence of events.
  - **Results:** What is true after script ends.

Example: Restaurant script — (Enter, Sit, Order, Eat, Pay, Leave).

### 2.6 Conceptual Dependency (CD)

- Proposed by **Schank** to represent the meaning of natural language sentences in a language-independent form.
- Uses a small set of **primitive ACTs:**

| Primitive | Meaning |
|---|---|
| ATRANS | Transfer of abstract relationship (ownership) |
| PTRANS | Physical transfer of object |
| MTRANS | Transfer of mental information |
| MBUILD | Construct new information |
| PROPEL | Apply force to object |
| MOVE | Move body part |
| INGEST | Take in substance |
| EXPEL | Expel substance |
| SPEAK | Produce sound |
| ATTEND | Focus sense organ |

### 2.7 Ontologies

- A formal, explicit specification of a shared conceptualisation.
- Defines concepts, properties, relationships, constraints, and axioms in a domain.
- **Components:** Classes (concepts), Properties (slots), Individuals (instances), Axioms (rules).
- **Example:** OWL (Web Ontology Language), RDF (Resource Description Framework).
- **Upper Ontology:** General ontology for all domains (e.g., Cyc, SUMO).
- **Domain Ontology:** Specific to a field (medical, legal, etc.).

### 2.8 Expert Systems

- AI systems that emulate decision-making of a human expert.
- **Components:**
  - **Knowledge Base:** Domain-specific facts and rules.
  - **Inference Engine:** Applies rules using forward/backward chaining.
  - **Working Memory:** Current problem state.
  - **User Interface:** Interaction with user.
  - **Explanation Facility:** Explains reasoning (WHY, HOW questions).
  - **Knowledge Acquisition Facility:** Adds/updates knowledge.

**Examples:** MYCIN (medical diagnosis), DENDRAL (chemical analysis), XCON (computer configuration).

**Limitations:** Cannot learn, brittle at knowledge boundaries, knowledge acquisition bottleneck.

### 2.9 Handling Uncertainty in Knowledge

**Certainty Factors (CF) — used in MYCIN:**
- `CF(H, E)` = measure of belief in hypothesis H given evidence E. Range: [-1, 1].
- `CF > 0`: Evidence supports hypothesis.
- `CF < 0`: Evidence contradicts hypothesis.
- **Combining CFs (same hypothesis, different evidence):**
  - If both positive: `CF(H, E1 ∧ E2) = CF1 + CF2 × (1 - CF1)`
  - If both negative: `CF(H, E1 ∧ E2) = CF1 + CF2 × (1 + CF1)`
  - If opposite signs: `CF(H, E1 ∧ E2) = (CF1 + CF2) / (1 - min(|CF1|, |CF2|))`

**Bayesian Networks (Belief Networks):**
- Directed Acyclic Graph (DAG) where nodes = random variables; edges = conditional dependencies.
- Each node has a **Conditional Probability Table (CPT):** `P(Xᵢ | Parents(Xᵢ))`.
- **Joint Probability:**
  - `P(X₁, X₂, ..., Xₙ) = Π P(Xᵢ | Parents(Xᵢ))`
- **Inference:** Compute `P(query | evidence)` using marginalization or belief propagation.

**Dempster-Shafer Theory:**
- Generalizes Bayesian reasoning; assigns belief to sets of hypotheses rather than single hypotheses.
- **Basic Probability Assignment (BPA / mass):** `m: 2^Ω → [0, 1]`, `Σ m(A) = 1`.
- **Belief:** `Bel(A) = Σ_{B⊆A} m(B)` (lower bound on probability).
- **Plausibility:** `Pl(A) = 1 - Bel(Ā)` (upper bound on probability).

---

## 3. Planning

### 3.1 Components of a Planning System

- **Initial State:** Logical description of the world at start.
- **Goal State:** Desired logical description to achieve.
- **Actions/Operators:** Each defined by:
  - **Preconditions:** Must be true before action executes.
  - **Effects (Add list / Delete list):** What becomes true/false after action.
- **Plan:** Ordered (or partially ordered) sequence of actions from initial to goal state.

### 3.2 STRIPS (Stanford Research Institute Problem Solver)

- Formal language for specifying planning problems.
- Uses **First-Order Predicate Logic** to represent states and operators.
- **Operator format:**
  ```
  Operator: MOVE(x, y, z)   -- Move block x from y to z
    Preconditions:  On(x, y) ∧ Clear(x) ∧ Clear(z)
    Add List:       On(x, z) ∧ Clear(y)
    Delete List:    On(x, y) ∧ Clear(z)
  ```
- **Closed World Assumption (CWA):** Anything not stated is assumed false.

**STRIPS Assumption:** Actions have no indirect side effects; the rest of the world remains unchanged (frame problem addressed partially).

### 3.3 Goal Stack Planning

- Uses a **stack** of goals and operators.
- **Algorithm:**
  1. Push goal onto stack.
  2. If top of stack is satisfied in current state, pop it.
  3. If top of stack is a conjunct, push each sub-goal.
  4. If top is an operator, apply it (check preconditions, update state).
  5. If top is an unsatisfied goal, find an operator that achieves it and push operator + its preconditions.
- **Issue:** Sussman Anomaly — interleaved goals cannot always be solved independently.

**Sussman Anomaly Example (Blocks World):**
- Goal: On(A,B) ∧ On(B,C)
- Independent sub-plans conflict; solving one undoes the other.
- Solution requires **interleaved planning.**

### 3.4 Linear vs Non-Linear Planning

| Aspect | Linear Planning | Non-Linear Planning |
|---|---|---|
| Approach | Solves one goal completely before the next | Interleaves steps for multiple goals |
| Issue | Sussman Anomaly — subgoals conflict | More complex but avoids anomaly |
| Example | Goal Stack Planning | Partial Order Planning |

### 3.5 Hierarchical Planning (HTN — Hierarchical Task Networks)

- Decomposes **abstract tasks** into lower-level subtasks recursively until primitive actions are reached.
- **Primitive task:** Can be executed directly.
- **Compound task:** Must be decomposed using **methods.**
- **Method:** A decomposition schema for a compound task.
- More practical for complex real-world domains.

### 3.6 Partial Order Planning (POP)

- Plans represented as **partially ordered** sets of actions (not fully committed to ordering).
- Only adds ordering constraints when necessary to avoid conflicts.
- **Plan representation:** `{steps, ordering constraints, causal links, open preconditions}`
- **Causal Link:** `Sᵢ →_p Sⱼ` — Step Sᵢ achieves precondition p for Sⱼ.
- **Threat:** Step Sₖ might delete condition p in causal link `Sᵢ →_p Sⱼ`.
- **Conflict Resolution:**
  - **Demotion:** Order Sₖ before Sᵢ.
  - **Promotion:** Order Sₖ after Sⱼ.
- Avoids Sussman Anomaly naturally; more flexible than linear planning.

---

## 4. Natural Language Processing (NLP)

### 4.1 Grammar and Language

- **Formal Grammar:** A quadruple `G = (V, T, P, S)` where:
  - V = set of variables (non-terminals)
  - T = set of terminals
  - P = set of production rules
  - S = start symbol

**Chomsky Hierarchy:**

| Type | Grammar | Automaton | Language |
|---|---|---|---|
| Type 0 | Unrestricted | Turing Machine | Recursively Enumerable |
| Type 1 | Context-Sensitive | LBA | Context-Sensitive |
| Type 2 | Context-Free (CFG) | PDA | Context-Free |
| Type 3 | Regular | Finite Automaton | Regular |

**Context-Free Grammar (CFG) for NLP:**
```
S  → NP VP
NP → Det N | N
VP → V NP | V
Det → the | a
N  → cat | mat
V  → sat
```

### 4.2 Parsing Techniques

**Top-Down Parsing:**
- Start from the root (S); expand non-terminals using production rules.
- **Recursive Descent Parser:** Apply rules top-down; backtrack on failure.
- Problem: Left recursion causes infinite loops.

**Bottom-Up Parsing:**
- Start from input words (leaves); reduce using rules to reach S.
- **Shift-Reduce Parsing:** Shift words onto stack; reduce using grammar rules.

**Chart Parsing (Earley Parser):**
- Dynamic programming approach; handles ambiguous and left-recursive grammars.
- Complete, sound for any CFG.
- Time: O(n³) for ambiguous grammars; O(n²) for unambiguous.

**CYK (Cocke-Younger-Kasami) Algorithm:**
- Requires grammar in **Chomsky Normal Form (CNF):** Rules of form `A → BC` or `A → a`.
- Bottom-up DP; fills an n×n triangular table.
- Time: O(n³ × |G|) where |G| = number of grammar rules.

**Probabilistic/Statistical Parsing:**
- **PCFG (Probabilistic CFG):** Each rule has a probability. `P(rule: A → α) = probability`.
- `P(tree) = Π P(rule used at each node)`
- Best parse = parse tree with highest probability.

### 4.3 Semantic Analysis

- **Goal:** Determine the meaning of a sentence, not just its structure.
- **Approaches:**
  - **Semantic Grammar:** Grammar encodes semantic information directly.
  - **Case Grammar:** Identifies semantic roles: Agent, Patient, Instrument, Location.
  - **Lambda Calculus:** Compositional semantics; meaning of phrase = function of meanings of parts.
    - Example: `run'(john')` represents "John runs."
  - **Semantic Nets / Frames:** Map sentence to frame-based or net-based representation.

**Word Sense Disambiguation (WSD):** Determining the correct sense of a polysemous word using context.

**Named Entity Recognition (NER):** Identifying proper nouns as persons, organizations, locations.

### 4.4 Pragmatics

- **Goal:** Understanding language in context; meaning beyond literal sentence meaning.
- **Speech Acts (Austin, Searle):** Utterances as actions — Assertive, Directive, Commissive, Expressive, Declarative.
- **Discourse Analysis:** Understanding multi-sentence text; reference resolution, discourse structure.
- **Anaphora Resolution:** Linking pronouns/references to their antecedents.
  - Example: "Alice met Bob. She greeted him." → She = Alice, him = Bob.
- **Gricean Maxims:** Cooperative communication principles — Quantity, Quality, Relation, Manner.
- **Presupposition:** What is assumed to be true before an utterance.

---

## 5. Multi-Agent Systems (MAS)

### 5.1 Agents and Objects

| Aspect | Object | Agent |
|---|---|---|
| Action | Invoked by method calls | Acts autonomously based on goals |
| Control | Passive (controlled externally) | Active (self-directed) |
| Goal | None | Has goals and intentions |
| Reactivity | Reactive only | Reactive, proactive, social |

**Properties of Intelligent Agents:**
- **Reactivity:** Responds to environment changes.
- **Proactivity:** Goal-directed initiative.
- **Social Ability:** Communicates with other agents.
- **Autonomy:** Operates without direct human control.

**BDI Model (Belief-Desire-Intention):**
- **Beliefs:** Agent's knowledge about the world.
- **Desires:** Goals the agent wants to achieve.
- **Intentions:** Goals the agent has committed to pursuing.

### 5.2 Agents and Expert Systems

| Aspect | Expert System | Agent |
|---|---|---|
| Operation | Static; invoked on demand | Continuous; autonomous |
| Adaptability | Fixed knowledge base | Can learn and adapt |
| Environment | Closed | Open, dynamic |
| Interaction | Single user-system | Multi-agent interaction |

### 5.3 Generic Structure of Multi-Agent System

- **Agent Layer:** Individual agents with perception, reasoning, action.
- **Communication Layer:** Message passing (ACL — Agent Communication Language).
- **Middleware:** Facilitates agent discovery, naming, directory services.
- **Environment:** Shared world that agents perceive and act upon.

**Agent Architectures:**
- **Reactive (Subsumption):** No internal state; direct stimulus-response (Brooks).
- **Deliberative (BDI):** Symbolic reasoning with beliefs, desires, intentions.
- **Hybrid:** Reactive + Deliberative layers.

### 5.4 Semantic Web

- Extension of the World Wide Web with machine-readable semantics.
- **Layers (Semantic Web Stack):**
  ```
  Trust
  Proof
  Logic (OWL, Rules)
  Ontology (OWL)
  Data Interchange (RDF, RDFS)
  Syntax (XML, XML Schema)
  URI / IRI
  ```
- **RDF (Resource Description Framework):** Triples of `(subject, predicate, object)`.
  - Example: `(John, hasAge, 30)`, `(John, knows, Mary)`
- **OWL (Web Ontology Language):** Richer ontology language; supports reasoning.
- **SPARQL:** Query language for RDF data.

### 5.5 Agent Communication

- **ACL (Agent Communication Language):** FIPA-ACL, KQML.
- **Performatives (Speech Acts in ACL):** INFORM, REQUEST, QUERY-IF, AGREE, REFUSE, PROPOSE, SUBSCRIBE.
- **Message Structure:** Sender, Receiver, Performative, Content, Language, Ontology.

**Coordination Mechanisms:**
- **Contract Net Protocol:** Manager broadcasts task; agents bid; manager awards contract.
- **Auctions:** English, Dutch, Vickrey auction mechanisms.
- **Blackboard Architecture:** Shared data structure (blackboard) that agents read/write.

### 5.6 Knowledge Sharing using Ontologies

- **Common ontology** enables agents to share and interpret knowledge uniformly.
- **KIF (Knowledge Interchange Format):** Logic-based language for knowledge exchange.
- **OKBC (Open Knowledge Base Connectivity):** Protocol to access knowledge bases.
- Ontologies define shared vocabulary and semantics for inter-agent communication.

### 5.7 Agent Development Tools

| Tool | Description |
|---|---|
| **JADE (Java Agent DEvelopment Framework)** | FIPA-compliant; widely used; provides AMS, DF services |
| **NetLogo** | Multi-agent simulation environment |
| **Repast** | Agent-based simulation toolkit |
| **ZEUS** | Collaborative agent-building toolkit |
| **AgentSpeak / Jason** | BDI agent programming language |

---

## 6. Fuzzy Sets

### 6.1 Notion of Fuzziness

- Classical (crisp) set: element either belongs (1) or does not (0).
- **Fuzzy Set:** An element belongs with a **degree of membership** in [0, 1].
- Introduced by **Lotfi Zadeh (1965).**
- Models imprecision and vagueness in human reasoning.

### 6.2 Membership Functions

A fuzzy set A in universe X is defined by:
`A = {(x, μ_A(x)) | x ∈ X}` where `μ_A(x) : X → [0, 1]`

**Common Membership Function Shapes:**

| Shape | Formula |
|---|---|
| Triangular | `max(0, min((x-a)/(b-a), (c-x)/(c-b)))` for parameters a ≤ b ≤ c |
| Trapezoidal | `max(0, min((x-a)/(b-a), 1, (d-x)/(d-c)))` for a ≤ b ≤ c ≤ d |
| Gaussian | `μ(x) = e^(-(x-c)²/(2σ²))` |
| Sigmoidal | `μ(x) = 1/(1 + e^(-a(x-c)))` |
| Bell-shaped | `μ(x) = 1/(1 + |(x-c)/a|^(2b))` |

**Key Terms:**
- **Support:** `{x ∈ X | μ_A(x) > 0}`
- **Core:** `{x ∈ X | μ_A(x) = 1}`
- **Alpha-cut (α-cut):** `A_α = {x ∈ X | μ_A(x) ≥ α}`
- **Height:** `h(A) = max μ_A(x)`
- **Normal Fuzzy Set:** h(A) = 1.

### 6.3 Operations on Fuzzy Sets

For fuzzy sets A and B in universe X:

| Operation | Formula |
|---|---|
| **Union** | `μ_(A∪B)(x) = max(μ_A(x), μ_B(x))` |
| **Intersection** | `μ_(A∩B)(x) = min(μ_A(x), μ_B(x))` |
| **Complement** | `μ_Ā(x) = 1 - μ_A(x)` |
| **Algebraic Product** | `μ_(A·B)(x) = μ_A(x) × μ_B(x)` |
| **Algebraic Sum** | `μ_(A+B)(x) = μ_A(x) + μ_B(x) - μ_A(x)·μ_B(x)` |
| **Bounded Product** | `μ_(A⊗B)(x) = max(0, μ_A(x) + μ_B(x) - 1)` |
| **Bounded Sum** | `μ_(A⊕B)(x) = min(1, μ_A(x) + μ_B(x))` |

**De Morgan's Laws hold for fuzzy sets:**
- `¬(A ∪ B) = ¬A ∩ ¬B`
- `¬(A ∩ B) = ¬A ∪ ¬B`

**Laws that do NOT hold (unlike crisp sets):**
- `A ∩ Ā ≠ ∅` (law of contradiction fails)
- `A ∪ Ā ≠ X` (law of excluded middle fails)

### 6.4 Fuzzification and Defuzzification

**Fuzzification:** Convert crisp input values into fuzzy membership values.
- Apply membership functions to input variable.

**Defuzzification:** Convert fuzzy output set into a single crisp value.

| Method | Formula | Notes |
|---|---|---|
| **Centroid (COG)** | `x* = ∫ x·μ(x)dx / ∫ μ(x)dx` | Most widely used |
| **Bisector** | Value dividing area under curve into two equal halves | — |
| **MOM (Mean of Maxima)** | Mean of all x where μ(x) is maximum | — |
| **LOM (Largest of Maxima)** | Largest x where μ(x) is maximum | — |
| **SOM (Smallest of Maxima)** | Smallest x where μ(x) is maximum | — |
| **Weighted Average** | `x* = Σ μ(xᵢ)·xᵢ / Σ μ(xᵢ)` | For symmetrical sets |

### 6.5 Fuzzy Relations

- A fuzzy relation R on X × Y is a fuzzy set: `R = {((x,y), μ_R(x,y)) | x ∈ X, y ∈ Y}`
- **Composition of Fuzzy Relations:**
  - **Max-Min Composition:** `μ_(R∘S)(x, z) = max_y [min(μ_R(x,y), μ_S(y,z))]`
  - **Max-Product Composition:** `μ_(R∘S)(x, z) = max_y [μ_R(x,y) × μ_S(y,z)]`

### 6.6 Fuzzy Functions and Linguistic Variables

- **Linguistic Variable:** A variable whose values are words/phrases in natural language.
- Proposed by **Zadeh.**
- Defined as a quintuple `(X, T(X), U, G, M)`:
  - X = variable name (e.g., "Temperature")
  - T(X) = set of linguistic values (e.g., {Cold, Warm, Hot})
  - U = universe of discourse (e.g., [0°, 100°])
  - G = grammar for generating terms
  - M = semantic rules (mapping terms to fuzzy sets)

**Linguistic Hedges:** Modifiers that adjust membership functions.
- **Very:** `μ_{very A}(x) = (μ_A(x))²` (concentration)
- **Somewhat/Fairly:** `μ_{fairly A}(x) = (μ_A(x))^{0.5}` (dilation)
- **Not:** `μ_{not A}(x) = 1 - μ_A(x)`
- **More or less:** `μ(x) = (μ_A(x))^{1/3}`

### 6.7 Fuzzy Rules and Fuzzy Inference

- **Fuzzy Rule:** `IF x is A THEN y is B` (fuzzy conditional)
- **Fuzzy Implication:** `μ_(A→B)(x,y) = min(μ_A(x), μ_B(y))` (Mamdani)

**Inference Methods:**

**Mamdani Method:**
1. Fuzzify inputs.
2. Apply fuzzy operators (AND = min, OR = max) to evaluate rule antecedents.
3. Apply implication (clip/scale output fuzzy set by rule strength).
4. Aggregate all rule outputs.
5. Defuzzify (typically centroid).

**Sugeno (Takagi-Sugeno) Method:**
- Rule consequent is a **crisp function** of inputs: `IF x is A THEN y = f(x)` (usually linear).
- Output is weighted average: `y* = Σ wᵢ·yᵢ / Σ wᵢ` where wᵢ = firing strength of rule i.
- Computationally efficient; no defuzzification step needed for crisp output.

### 6.8 Fuzzy Control System and Fuzzy Rule-Based Systems

- **Fuzzy Controller Components:**
  ```
  Crisp Input → Fuzzifier → Inference Engine ← Rule Base
                                    ↓           ← Database
              Crisp Output ← Defuzzifier
  ```

- **Rule Base:** Collection of fuzzy IF-THEN rules (expert knowledge).
- **Database:** Membership function definitions.
- **Inference Engine:** Applies rules using fuzzy logic.
- **Applications:** Temperature control, washing machines, anti-lock brakes, image processing.

**Advantages over classical control:** Handles imprecision, does not require mathematical model of plant, easy to incorporate expert knowledge.

---

## 7. Genetic Algorithms (GA)

### 7.1 Overview

- Inspired by **Darwinian natural selection** and **genetics.**
- Search/optimization technique operating on a **population of candidate solutions.**
- Proposed by **John Holland (1975).**

### 7.2 Encoding Strategies

| Encoding | Representation | Example |
|---|---|---|
| **Binary** | String of 0s and 1s | `10110101` |
| **Real-Valued** | String of real numbers | `[3.14, 2.71, 1.41]` |
| **Integer** | String of integers | `[2, 5, 1, 4, 3]` |
| **Permutation** | Sequence of distinct integers | `[3, 1, 4, 2, 5]` (for TSP) |
| **Tree** | Parse tree (for GP) | Expression tree |

- **Chromosome:** Encoded representation of a candidate solution.
- **Gene:** Single element in a chromosome.
- **Allele:** Value of a gene.
- **Locus:** Position of a gene in the chromosome.

### 7.3 Fitness Function

- Evaluates how good a candidate solution is.
- Maps chromosome to a real number (fitness score).
- Higher fitness = better solution (for maximisation).
- **Properties:** Non-negative, problem-specific, computationally feasible.

**Example (maximising f(x) = x²):**
- Chromosome `1010` (binary) = 10 (decimal) → Fitness = 10² = 100.

### 7.4 Genetic Operators

**Selection:** Choose individuals for reproduction based on fitness.

| Method | Description |
|---|---|
| **Roulette Wheel (Fitness-Proportionate)** | `P(i) = f(i) / Σ f(j)` — probability proportional to fitness |
| **Tournament Selection** | Pick k individuals randomly; select best |
| **Rank Selection** | Rank by fitness; select by rank probability |
| **Elitism** | Always carry best individuals to next generation |

**Crossover (Recombination):** Combine genetic material from two parents.

| Type | Description |
|---|---|
| **Single-Point** | Pick one point; swap tails of two parents |
| **Two-Point** | Pick two points; swap segment between them |
| **Uniform** | Each gene independently chosen from either parent with probability 0.5 |
| **Arithmetic** | `child = α×parent1 + (1-α)×parent2` for real-valued encoding |
| **Order (OX)** | For permutation encoding; preserves relative order |

**Mutation:** Random alteration of genes; maintains genetic diversity; prevents premature convergence.

| Type | Description |
|---|---|
| **Bit Flip** | Flip a bit: 0→1 or 1→0 (binary) |
| **Swap** | Swap two genes in the chromosome |
| **Inversion** | Reverse a sub-sequence |
| **Gaussian** | Add Gaussian noise to real-valued gene |
| **Scramble** | Randomly shuffle a selected segment |

- **Crossover rate (Pc):** Typically 0.6–0.9.
- **Mutation rate (Pm):** Typically 0.001–0.01 (kept low to avoid random search).

### 7.5 GA Cycle

```
1.  Initialize population randomly (size N)
2.  Evaluate fitness of each individual
3.  While termination condition not met:
    a.  Selection: Select parents based on fitness
    b.  Crossover: Apply crossover with probability Pc → offspring
    c.  Mutation: Apply mutation with probability Pm
    d.  Evaluate fitness of offspring
    e.  Replace old population with new generation
4.  Return best individual found
```

**Termination Conditions:** Maximum generations reached, fitness threshold met, population converged.

**Schema Theorem (Holland's Building Block Hypothesis):**
- Short, low-order, above-average schemata (building blocks) receive exponentially increasing trials.
- `m(H, t+1) ≥ m(H, t) × f(H)/f̄ × [1 - Pc × δ(H)/(L-1) - o(H) × Pm]`
  - m(H,t) = number of instances of schema H at time t
  - f(H) = average fitness of H
  - f̄ = average population fitness
  - δ(H) = defining length of schema
  - o(H) = order of schema
  - L = chromosome length

### 7.6 Problem Solving using GA

| Problem | Encoding |
|---|---|
| **Travelling Salesman (TSP)** | Permutation encoding; order crossover |
| **Function Optimisation** | Binary or real-valued encoding |
| **Scheduling** | Permutation or integer encoding |
| **Neural Network Weight Optimisation** | Real-valued encoding |
| **Feature Selection** | Binary encoding (1 = selected feature) |
| **Game Playing** | Strategy encoded as chromosome |

**Advantages:** Suitable for non-differentiable, multi-modal, discontinuous search spaces; parallelisable.
**Limitations:** No guarantee of global optimum; choice of encoding/parameters is non-trivial; computationally expensive.

---

## 8. Artificial Neural Networks (ANN)

### 8.1 Biological Motivation

- Inspired by biological neurons.
- **Artificial Neuron (McCulloch-Pitts, 1943):**
  - Inputs: `x₁, x₂, ..., xₙ`
  - Weights: `w₁, w₂, ..., wₙ`
  - Net Input: `net = Σ wᵢxᵢ + b` (where b = bias)
  - Output: `y = f(net)` where f = activation function.

**Activation Functions:**

| Function | Formula | Range | Use |
|---|---|---|---|
| Step | `f(x) = 1 if x≥0 else 0` | {0,1} | Binary classification |
| Sign | `f(x) = 1 if x≥0 else -1` | {-1,1} | Bipolar |
| Sigmoid | `f(x) = 1/(1+e^(-x))` | (0,1) | Hidden layers (older) |
| Tanh | `f(x) = (eˣ-e⁻ˣ)/(eˣ+e⁻ˣ)` | (-1,1) | Hidden layers |
| ReLU | `f(x) = max(0, x)` | [0,∞) | Deep networks (common) |
| Leaky ReLU | `f(x) = x if x>0 else αx` | (-∞,∞) | Avoids dying ReLU |
| Softmax | `f(xᵢ) = e^(xᵢ)/Σe^(xⱼ)` | (0,1) | Output (multiclass) |

### 8.2 Learning Types

| Type | Definition | Examples |
|---|---|---|
| **Supervised** | Learn from labelled input-output pairs | Perceptron, MLP, RBF |
| **Unsupervised** | Find patterns without labels | SOM, Autoencoders, Clustering |
| **Reinforcement** | Learn by reward/penalty from environment | Q-Learning, Actor-Critic |

**Hebbian Learning Rule:** "Neurons that fire together, wire together."
`Δwᵢⱼ = η × xᵢ × yⱼ`

**Delta Rule (Widrow-Hoff):**
`Δwᵢ = η × (t - y) × xᵢ`
where t = target, y = actual output, η = learning rate.

### 8.3 Single Layer Perceptron

- Proposed by **Frank Rosenblatt (1958).**
- Single layer of output neurons; no hidden layers.
- **Learning Algorithm:**
  1. Initialize weights randomly.
  2. For each training example (x, t):
     - Compute output: `y = f(w·x + b)`
     - Update: `wᵢ ← wᵢ + η(t - y)xᵢ` ; `b ← b + η(t - y)`
  3. Repeat until convergence.

- **Perceptron Convergence Theorem:** If data is linearly separable, perceptron learning algorithm converges in a finite number of steps.
- **Limitation:** Cannot solve XOR problem (not linearly separable). Proved by Minsky and Papert (1969).

### 8.4 Multi-Layer Perceptron (MLP) and Backpropagation

- Multiple layers: Input layer, one or more hidden layers, output layer.
- **Universal Approximation Theorem:** An MLP with at least one hidden layer and a non-linear activation function can approximate any continuous function on a compact subset of Rⁿ.

**Backpropagation Algorithm:**

**Forward Pass:**
```
For each layer l from 1 to L:
    z^l = W^l × a^(l-1) + b^l
    a^l = f(z^l)
Output: ŷ = a^L
```

**Loss Function:**
- Mean Squared Error (MSE): `L = (1/n) Σ (tᵢ - ŷᵢ)²`
- Cross-Entropy: `L = -Σ tᵢ log(ŷᵢ)` (for classification)

**Backward Pass (Gradient Computation):**
```
Output layer error:
    δ^L = (ŷ - t) ⊙ f'(z^L)

Hidden layer error (backpropagate):
    δ^l = ((W^(l+1))ᵀ δ^(l+1)) ⊙ f'(z^l)

Weight updates:
    W^l ← W^l - η × δ^l × (a^(l-1))ᵀ
    b^l ← b^l - η × δ^l
```

**Chain Rule (mathematical basis):**
`∂L/∂W^l = ∂L/∂a^L × ∂a^L/∂z^L × ∂z^L/∂a^(L-1) × ... × ∂a^l/∂z^l × ∂z^l/∂W^l`

**Optimisation Variants:**
- **Batch Gradient Descent:** Update after entire dataset.
- **Stochastic Gradient Descent (SGD):** Update after each sample.
- **Mini-Batch Gradient Descent:** Update after small batch (typical).
- **Momentum:** `v ← γv + η∇L` ; `W ← W - v`
- **Adam:** Adaptive learning rates using first and second moments of gradient.

**Vanishing Gradient Problem:** Gradients shrink exponentially in deep networks with sigmoid/tanh. Solved by ReLU, batch normalisation, skip connections.

### 8.5 Self-Organising Maps (SOM)

- Proposed by **Teuvo Kohonen (1982).**
- Unsupervised learning; maps high-dimensional data to low-dimensional (usually 2D) grid.
- Preserves **topological structure** of input data.

**Algorithm:**
1. Initialize weights `wᵢ` randomly for each neuron i.
2. For each input vector x:
   a. **Competition:** Find Best Matching Unit (BMU): `i* = argmin_i ||x - wᵢ||`
   b. **Cooperation:** Define neighbourhood function: `h(i, i*, t) = exp(-d²(i,i*)/(2σ(t)²))`
      where d(i, i*) = distance between neurons i and i* on the grid.
   c. **Adaptation:** Update weights:
      `wᵢ(t+1) = wᵢ(t) + η(t) × h(i, i*, t) × (x - wᵢ(t))`
3. Decrease η(t) and σ(t) over time.

**Parameters:**
- `η(t)` = learning rate (decreases over time).
- `σ(t)` = neighbourhood radius (decreases over time).
- `h(i, i*, t)` = neighbourhood function (Gaussian typically).

**Applications:** Dimensionality reduction, data visualisation, clustering.

### 8.6 Hopfield Network

- Proposed by **John Hopfield (1982).**
- **Recurrent network:** Fully connected, symmetric weights (`wᵢⱼ = wⱼᵢ`), no self-connections (`wᵢᵢ = 0`).
- Acts as **associative (content-addressable) memory.**
- Binary neurons: state `sᵢ ∈ {-1, +1}` or `{0, 1}`.

**Energy Function:**
`E = -½ Σᵢ Σⱼ wᵢⱼ sᵢ sⱼ - Σᵢ θᵢ sᵢ`
where θᵢ = threshold of neuron i.

- Network converges to a **local minimum** of E.
- Stored patterns are energy minima (**attractors**).

**Weight Learning (Hebbian):**
For storing p patterns `{ξ¹, ξ², ..., ξᵖ}`:
`wᵢⱼ = (1/N) Σ_μ ξᵢ^μ × ξⱼ^μ` for i ≠ j ; `wᵢᵢ = 0`

**Update Rule:**
`sᵢ(t+1) = sign(Σⱼ wᵢⱼ sⱼ(t) - θᵢ)`

- **Asynchronous update:** One neuron updates at a time; guaranteed convergence.
- **Synchronous update:** All neurons update simultaneously; may oscillate.

**Storage Capacity:**
- Maximum number of patterns: `p ≤ 0.138 × N` (approximately 0.15N)
- where N = number of neurons.
- Exceeding capacity leads to spurious states (false memories).

**Limitations:** Limited capacity, spurious attractors, slow retrieval for large patterns.

---

## Quick Recap Table

| Topic | Key Formulas / Concepts |
|---|---|
| A* Search | `f(n) = g(n) + h(n)` ; admissible: `h(n) ≤ h*(n)` |
| Alpha-Beta | Prune if `α ≥ β` ; best case O(b^(m/2)) |
| Minimax | MAX maximises, MIN minimises; O(b^m) |
| Unification | Substitution θ making two expressions identical |
| Resolution | `(P ∨ Q) ∧ (¬P ∨ R) → Q ∨ R` |
| Bayesian Net | `P(X₁...Xₙ) = Π P(Xᵢ\|Parents(Xᵢ))` |
| STRIPS | Preconditions, Add list, Delete list |
| POP | Causal links, threats resolved by demotion/promotion |
| Earley Parser | Any CFG; O(n³) ; dynamic programming |
| CYK | CNF grammar required; O(n³) |
| Fuzzy Union | `max(μ_A, μ_B)` |
| Fuzzy Intersection | `min(μ_A, μ_B)` |
| Centroid | `x* = ∫x·μ(x)dx / ∫μ(x)dx` |
| Max-Min Composition | `max_y[min(μ_R(x,y), μ_S(y,z))]` |
| Linguistic Hedge | Very: `μ²` ; Fairly: `μ^0.5` |
| GA Roulette | `P(i) = f(i)/Σf(j)` |
| Schema Theorem | Short, low-order, above-average schemata grow exponentially |
| Perceptron Update | `Δwᵢ = η(t-y)xᵢ` |
| Backpropagation | Chain rule; δ^L = (ŷ-t)⊙f'(z^L) |
| SOM BMU | `argmin ||x - wᵢ||` |
| Hopfield Energy | `E = -½ Σᵢⱼ wᵢⱼ sᵢ sⱼ` |
| Hopfield Capacity | `p ≤ 0.138N` |
| Hopfield Weights | `wᵢⱼ = (1/N) Σ_μ ξᵢ^μ ξⱼ^μ` |

---

*Notes prepared for UGC NET Computer Science – Unit 10*
