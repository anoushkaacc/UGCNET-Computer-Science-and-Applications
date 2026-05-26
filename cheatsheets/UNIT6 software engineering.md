#  UGC NET – Unit 6: Software Engineering


---

## 1. Software Process Models

### 🔹 Software Process
A structured set of activities required to develop a software system (specification, design, implementation, validation, evolution).

### 🔹 Generic Process Model
| Component | Description |
|---|---|
| **Framework Activity** | Broad tasks like Communication, Planning, Modelling, Construction, Deployment |
| **Task Set** | Specific work tasks, milestones, and deliverables within each activity |
| **Process Patterns** | Reusable solutions to recurring software process problems |

### 🔹 Process Lifecycle
Covers the complete span from conception → development → maintenance → retirement.

---

### 🔹 Prescriptive Process Models

| Model | Key Idea |
|---|---|
| **Waterfall** | Linear sequential; each phase complete before next begins |
| **Incremental** | System built and delivered in increments |
| **RAD (Rapid Application Development)** | Short iteration cycles; component-based construction |
| **Spiral** | Risk-driven; combines iterative + waterfall; 4 quadrants |
| **V-Model** | Verification & Validation at each stage; testing runs parallel to development |

### 🔹 Component Based Development (CBD)
Builds software from pre-existing, reusable components. Reduces time and cost; promotes reusability.

### 🔹 Aspect-Oriented Software Development (AOSD)
Separates **cross-cutting concerns** (logging, security, transactions) from core business logic using **aspects**.

### 🔹 Formal Methods
Mathematically-based techniques for software specification and verification (e.g., Z notation, VDM). Used in safety-critical systems.

---

### 🔹 Agile Process Models

| Model | Key Characteristics |
|---|---|
| **XP (Extreme Programming)** | Pair programming, TDD, continuous integration, small releases, refactoring |
| **Adaptive Software Development (ASD)** | Speculate → Collaborate → Learn; embraces change |
| **Scrum** | Sprints (2–4 weeks), Product Backlog, Sprint Backlog, Daily Standup, Scrum Master |
| **DSDM (Dynamic Systems Development Model)** | Timeboxing, MoSCoW prioritization, active user involvement |
| **Feature Driven Development (FDD)** | Builds feature list, plans/designs/builds by feature; short iterations |
| **Crystal** | Family of methods scaled by team size and criticality; focuses on people & interaction |
| **Web Engineering** | Adapts agile/prescriptive practices for web app development; addresses hypermedia & UI |

---

## 2. Software Requirements

### 🔹 Types of Requirements

| Type | Description | Example |
|---|---|---|
| **Functional** | What the system should do | "User shall be able to login" |
| **Non-Functional** | Quality constraints | Performance, security, reliability, scalability |

### 🔹 Eliciting Requirements
Techniques: Interviews, Questionnaires, Observation, Prototyping, JAD (Joint Application Development), Brainstorming.

### 🔹 Use Cases
- Describe interactions between **actors** and the **system**
- Components: Actor, Use Case, Relationships (include, extend, generalization)

### 🔹 Requirement Analysis & Modelling
- **Structured Analysis:** DFDs, ERDs, State diagrams
- **Object-Oriented Analysis:** Use case diagrams, class diagrams, sequence diagrams

### 🔹 Requirements Review
Formal inspection of SRS to detect errors, ambiguities, and inconsistencies early.

### 🔹 SRS Document (IEEE 830)
Contains: Purpose, Scope, Definitions, Overall Description, Specific Requirements (functional + non-functional), Appendices.

---

## 3. Software Design

### 🔹 Core Design Concepts

| Concept | Meaning |
|---|---|
| **Abstraction** | Hiding complexity; showing only essential details |
| **Architecture** | High-level structure; components and their relationships |
| **Patterns** | Reusable design solutions (e.g., MVC, Singleton) |
| **Separation of Concerns** | Each module addresses a distinct concern |
| **Modularity** | Dividing system into manageable, independent modules |
| **Information Hiding** | Internal details of module hidden from outside |
| **Functional Independence** | Modules perform a single, well-defined function |

### 🔹 Cohesion vs Coupling

| Metric | Goal | Types (Best → Worst) |
|---|---|---|
| **Cohesion** | HIGH cohesion | Functional > Sequential > Communicational > Procedural > Temporal > Logical > Coincidental |
| **Coupling** | LOW coupling | Data < Stamp < Control < External < Common < Content |

### 🔹 Design Levels

- **Architectural Design** – System structure; subsystems and their interactions (e.g., layered, client-server, pipe-filter)
- **Data Design** – Transforms data models into data structures; ER diagram → DB schema
- **Object-Oriented Design** – Classes, objects, inheritance, polymorphism, design patterns
- **User Interface Design** – Principles: consistency, feedback, error prevention (e.g., Shneiderman's 8 Golden Rules)
- **Component-Level Design** – Detailed logic for each component; pseudocode or flowcharts

---

## 4. Software Quality

### 🔹 McCall's Quality Factors (3 Categories)

| Category | Factors |
|---|---|
| **Product Operation** | Correctness, Reliability, Efficiency, Integrity, Usability |
| **Product Revision** | Maintainability, Flexibility, Testability |
| **Product Transition** | Portability, Reusability, Interoperability |

### 🔹 ISO 9126 Quality Factors
Functionality, Reliability, Usability, Efficiency, Maintainability, Portability.
> Updated by **ISO 25010** (adds Security, Compatibility).

### 🔹 Quality Control vs Quality Assurance

| QC | QA |
|---|---|
| Product-focused | Process-focused |
| Detect defects in output | Prevent defects via process improvement |
| Testing, inspection | Audits, standards, process reviews |

### 🔹 Risk Management – RMMM

| Step | Description |
|---|---|
| **Risk Identification** | List potential risks (project, technical, business) |
| **Risk Mitigation** | Strategies to reduce probability or impact |
| **Risk Monitoring** | Track risk indicators throughout project |
| **Risk Management** | Contingency planning and response |

### 🔹 Software Reliability
- Probability that software operates without failure for a specified time
- Metrics: **MTTF** (Mean Time To Failure), **MTTR** (Mean Time To Repair), **MTBF** (Mean Time Between Failures)

---

## 5. Estimation and Scheduling

### 🔹 Software Sizing

| Metric | Description |
|---|---|
| **LOC (Lines of Code)** | Count source lines; machine/language dependent |
| **Function Points (FP)** | Language-independent; based on inputs, outputs, inquiries, files, interfaces |

### 🔹 Cost & Effort Estimation Models

- **COCOMO (Constructive Cost Model)** – Barry Boehm, 1981
  - *Basic COCOMO:* `E = a × (KLOC)^b` → Organic, Semi-detached, Embedded modes
  - *Intermediate COCOMO:* Adds 15 cost drivers
  - *Detailed COCOMO:* Phase-level estimates
- **COCOMO II** – Updated for modern processes (reuse, OO, prototyping)

### 🔹 Project Scheduling & Staffing
- **WBS (Work Breakdown Structure):** Decomposes project into tasks
- **Critical Path Method (CPM):** Identifies longest path = minimum project duration
- **PERT:** Probabilistic time estimation `t = (O + 4M + P) / 6`
- **Staffing:** Based on effort estimate and timeline; avoid Brook's Law pitfall (*"Adding manpower to a late project makes it later"*)

### 🔹 Timeline Charts
- **Gantt Chart** – Bar chart showing task durations and schedule
- **Milestone Chart** – Marks key deliverable completion points

---

## 6. Software Testing

### 🔹 Key Terminology

| Term | Meaning |
|---|---|
| **Error** | Human mistake causing incorrect code |
| **Fault/Bug** | Manifestation of an error in the code |
| **Failure** | Deviation of software from expected behavior at runtime |

### 🔹 Verification vs Validation

| | Verification | Validation |
|---|---|---|
| **Question** | "Are we building the product right?" | "Are we building the right product?" |
| **Focus** | Process, intermediate products | Final product vs requirements |
| **Activities** | Reviews, walkthroughs, inspections | Testing |

### 🔹 Testing Levels

| Level | Scope |
|---|---|
| **Unit Testing** | Individual components/functions tested in isolation |
| **Integration Testing** | Interfaces between modules (Top-down, Bottom-up, Big Bang) |
| **System Testing** | End-to-end testing of the complete system |
| **Acceptance Testing** | Validates against user requirements |

### 🔹 White-box vs Black-box Testing

| White-box | Black-box |
|---|---|
| Internal structure/code known | Internal structure unknown |
| Basis Path, Control Structure Testing | Equivalence Partitioning, Boundary Value Analysis |
| Developer-centric | Requirement-centric |

### 🔹 White-box Techniques
- **Basis Path Testing** – Derive cyclomatic complexity `V(G) = E – N + 2P`; create independent paths
- **Control Structure Testing** – Condition testing, loop testing, data flow testing

### 🔹 Special Testing Types

| Type | Purpose |
|---|---|
| **Alpha Testing** | Done by developers/internal team before release |
| **Beta Testing** | Done by select end-users in real environment |
| **Regression Testing** | Re-test after changes to ensure no new bugs introduced |
| **Performance Testing** | Evaluate response time, throughput under normal load |
| **Stress Testing** | Push system beyond limits to find breaking point |

---

## 7. Software Configuration Management (SCM)

### 🔹 Change Control
- Formal process to evaluate, approve, and track changes to software
- **CCB (Change Control Board):** Approves or rejects change requests
- **Baseline:** A formally reviewed and approved software configuration item

### 🔹 Version Control
- Tracks revisions of source code over time
- Tools: Git, SVN, CVS
- Concepts: Repository, Branching, Merging, Check-in/Check-out

### 🔹 Software Reuse
- Reusing existing components, libraries, or designs to reduce effort
- Types: Code reuse, Design reuse, Concept reuse

### 🔹 Software Re-engineering
Restructuring or rewriting existing legacy systems to improve quality without changing functionality.
- Stages: Inventory Analysis → Document Restructuring → Reverse Engineering → Code/Data Restructuring → Forward Engineering

### 🔹 Reverse Engineering
Analyzing existing software to extract design and requirement information (going from code → design → specification).
> Opposite of forward engineering; useful for understanding undocumented legacy systems.

---

## 🔑 Quick Recap Table

| Topic | Must-Know Keywords |
|---|---|
| Process Models | Waterfall, Spiral, Scrum, XP, DSDM, FDD |
| Requirements | Functional/Non-Functional, SRS, Use Cases |
| Design | Cohesion, Coupling, Modularity, Abstraction |
| Quality | McCall's factors, ISO 9126, RMMM, MTTF |
| Estimation | LOC, FP, COCOMO, Gantt, CPM, PERT |
| Testing | White/Black-box, Basis Path, V(G), Alpha/Beta |
| SCM | Version Control, Re-engineering, Reverse Engineering |

---
*Notes prepared for UGC NET Computer Science – Unit 6*
