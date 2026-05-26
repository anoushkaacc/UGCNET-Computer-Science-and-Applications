# UGC NET – Unit 4: Database Management Systems
---

## 1. Database System Concepts and Architecture

### 1.1 Data Models

A **data model** is a collection of concepts that describe the structure of a database.

| Model | Description |
|---|---|
| **Relational Model** | Data in tables (relations); most widely used |
| **Hierarchical Model** | Tree structure; parent-child relationships |
| **Network Model** | Graph structure; records linked via sets |
| **Entity-Relationship (ER) Model** | Conceptual design using entities and relationships |
| **Object-Oriented Model** | Data as objects with attributes and methods |
| **Semi-structured (XML)** | Flexible schema; self-describing data |

### 1.2 Schemas and Instances

- **Schema:** The description/structure of the database (metadata). Does not change frequently.
- **Instance (Database State):** The actual data stored at a given point in time. Changes with every DML operation.
- **Intension:** Schema (what the database looks like).
- **Extension:** Instance (what data is in the database right now).

### 1.3 Three-Schema Architecture (ANSI/SPARC)

```
External Level   →  Multiple User Views (External Schemas)
        |
Conceptual Level →  Logical structure of entire DB (Conceptual Schema)
        |
Internal Level   →  Physical storage structure (Internal Schema)
```

**Data Independence:**
- **Logical Data Independence:** Ability to change the conceptual schema without changing external schemas or application programs.
- **Physical Data Independence:** Ability to change the internal schema (storage) without changing the conceptual schema.

### 1.4 Database Languages and Interfaces

| Language | Purpose |
|---|---|
| **DDL (Data Definition Language)** | Define schemas: CREATE, ALTER, DROP |
| **DML (Data Manipulation Language)** | Manipulate data: SELECT, INSERT, UPDATE, DELETE |
| **DCL (Data Control Language)** | Access control: GRANT, REVOKE |
| **TCL (Transaction Control Language)** | Transaction management: COMMIT, ROLLBACK, SAVEPOINT |
| **VDL (View Definition Language)** | Define user views |
| **SDL (Storage Definition Language)** | Define internal storage structures |

**Interfaces:** Menu-based, Form-based, Graphical, Natural Language, Speech, Web-based.

### 1.5 Centralized vs Client/Server Architecture

| Aspect | Centralized | Client/Server |
|---|---|---|
| Processing | Single machine | Distributed between client and server |
| Types | Mainframe | Two-tier, Three-tier, N-tier |
| Two-tier | — | Client directly contacts DB server |
| Three-tier | — | Client → Application Server → DB Server |

---

## 2. Data Modeling

### 2.1 Entity-Relationship (ER) Diagram

**Components:**

| Component | Symbol | Description |
|---|---|---|
| Entity | Rectangle | Real-world object |
| Weak Entity | Double Rectangle | Depends on another entity for identity |
| Attribute | Ellipse | Property of an entity |
| Key Attribute | Underlined Ellipse | Uniquely identifies an entity |
| Multivalued Attribute | Double Ellipse | Can have multiple values |
| Derived Attribute | Dashed Ellipse | Computed from other attributes |
| Relationship | Diamond | Association between entities |
| Identifying Relationship | Double Diamond | Links weak entity to its owner |

**Cardinality Ratios:** 1:1, 1:N, M:N

**Participation:**
- **Total (mandatory):** Double line — every entity must participate.
- **Partial (optional):** Single line — entity may or may not participate.

**Extended ER (EER):**
- **Generalization:** Bottom-up; subclasses combined into superclass.
- **Specialization:** Top-down; superclass divided into subclasses.
- **Aggregation:** Treating a relationship as a higher-level entity.
- **Constraints:** Disjoint (d) vs Overlapping (o); Total vs Partial.

### 2.2 Relational Model

- **Relation:** A table with rows (tuples) and columns (attributes).
- **Tuple:** A single row.
- **Attribute:** A column with a domain (set of allowed values).
- **Degree:** Number of attributes.
- **Cardinality:** Number of tuples.

**Relational Database Schema:** `R(A₁, A₂, ..., Aₙ)` where each Aᵢ is an attribute with domain `dom(Aᵢ)`.

### 2.3 Relational Constraints

| Constraint | Description |
|---|---|
| **Domain Constraint** | Attribute values must be within defined domain |
| **Key Constraint** | Key uniquely identifies each tuple; no two tuples have same key |
| **Entity Integrity** | Primary key cannot be NULL |
| **Referential Integrity** | Foreign key value must exist in the referenced relation or be NULL |
| **Semantic Integrity** | Application-specific business rules |

**Update Operations and Constraint Violations:**
- **INSERT:** May violate domain, key, entity integrity, referential integrity.
- **DELETE:** May violate referential integrity (cascading options: RESTRICT, CASCADE, SET NULL).
- **UPDATE:** May violate any constraint; treated as DELETE + INSERT.

### 2.4 Relational Algebra

A **procedural** query language; operations on relations return relations.

**Fundamental Operations:**

| Operation | Notation | Description |
|---|---|---|
| Selection | `σ_condition(R)` | Selects tuples satisfying condition (horizontal) |
| Projection | `π_attrs(R)` | Selects specific attributes (vertical); removes duplicates |
| Union | `R ∪ S` | All tuples in R or S; R and S must be union-compatible |
| Set Difference | `R − S` | Tuples in R but not in S; union-compatible |
| Cartesian Product | `R × S` | All combinations of tuples from R and S |
| Rename | `ρ_name(R)` | Renames a relation or attributes |

**Derived Operations:**

| Operation | Notation | Definition |
|---|---|---|
| Intersection | `R ∩ S` | `R − (R − S)` |
| Natural Join | `R ⋈ S` | Join on common attributes; removes duplicate columns |
| Theta Join | `R ⋈_θ S` | `σ_θ(R × S)` |
| Equi-Join | Theta join with = condition only | — |
| Left Outer Join | `R ⟕ S` | All tuples of R, NULLs for non-matching S tuples |
| Right Outer Join | `R ⟖ S` | All tuples of S, NULLs for non-matching R tuples |
| Full Outer Join | `R ⟗ S` | All tuples from both; NULLs for non-matching |
| Division | `R ÷ S` | Tuples in R associated with all tuples in S |
| Aggregate | `_grouping γ_function(R)` | COUNT, SUM, AVG, MIN, MAX grouped by attributes |

**Union Compatibility:** Two relations are union-compatible if they have the same number of attributes and corresponding attributes have compatible domains.

### 2.5 Relational Calculus

A **non-procedural** (declarative) query language; specifies what, not how.

**Tuple Relational Calculus (TRC):**
```
{ t | P(t) }
```
- `t` is a tuple variable; `P(t)` is the condition (formula).
- `{ t | EMPLOYEE(t) ∧ t.SALARY > 50000 }`

**Domain Relational Calculus (DRC):**
```
{ <x₁, x₂, ..., xₙ> | P(x₁, x₂, ..., xₙ) }
```
- Variables range over domain values (individual attribute values).
- **QBE (Query By Example)** is based on DRC.

**Safe Expression:** A calculus expression is safe if all values in the result come from the domain of the expression (avoids infinite results).

**Expressive Power:** Relational algebra and safe relational calculus are **equivalent in expressive power** (Codd's theorem).

### 2.6 Codd's Rules (12 Rules for RDBMS)

| Rule | Name | Description |
|---|---|---|
| 0 | Foundation | System must manage data using its relational capabilities |
| 1 | Information | All data represented as values in tables |
| 2 | Guaranteed Access | Every datum accessible via table name + primary key + column name |
| 3 | Systematic NULL | NULLs handled systematically (unknown/not applicable) |
| 4 | Active Online Catalog | Metadata stored in relational tables (data dictionary) |
| 5 | Comprehensive DML | At least one language for all data manipulation |
| 6 | View Updating | All theoretically updatable views must be updatable |
| 7 | High-level Insert/Update/Delete | Operations work on sets, not just single rows |
| 8 | Physical Data Independence | Physical changes don't affect programs |
| 9 | Logical Data Independence | Logical changes don't affect programs |
| 10 | Integrity Independence | Integrity constraints stored in catalog, not in programs |
| 11 | Distribution Independence | Application works regardless of data distribution |
| 12 | Non-subversion | Low-level access cannot bypass integrity constraints |

---

## 3. SQL

### 3.1 Data Definition and Data Types

```sql
CREATE TABLE Employee (
    EmpID    INT          PRIMARY KEY,
    Name     VARCHAR(50)  NOT NULL,
    DOB      DATE,
    Salary   DECIMAL(10,2) DEFAULT 0.00,
    DeptID   INT          REFERENCES Department(DeptID)
);

ALTER TABLE Employee ADD COLUMN Email VARCHAR(100);
ALTER TABLE Employee DROP COLUMN Email;
DROP TABLE Employee;
TRUNCATE TABLE Employee;   -- Removes all rows; faster than DELETE
```

**SQL Data Types:**

| Category | Types |
|---|---|
| Numeric | INT, SMALLINT, BIGINT, FLOAT, REAL, DOUBLE, DECIMAL(p,s), NUMERIC(p,s) |
| Character | CHAR(n), VARCHAR(n), TEXT, CLOB |
| Date/Time | DATE, TIME, DATETIME, TIMESTAMP, INTERVAL |
| Binary | BIT, BIT VARYING, BLOB, BINARY |
| Boolean | BOOLEAN |
| Other | XML, JSON, ARRAY, MULTISET |

### 3.2 Constraints

```sql
NOT NULL            -- Attribute cannot be NULL
UNIQUE              -- No duplicate values; NULL allowed
PRIMARY KEY         -- NOT NULL + UNIQUE
FOREIGN KEY         -- Referential integrity
CHECK (condition)   -- Attribute-level or tuple-level constraint
DEFAULT value       -- Default value when none specified
```

**Referential Actions:**
```sql
FOREIGN KEY (DeptID) REFERENCES Department(DeptID)
    ON DELETE CASCADE
    ON UPDATE SET NULL
```
Options: `CASCADE`, `SET NULL`, `SET DEFAULT`, `RESTRICT`, `NO ACTION`

### 3.3 Queries (SELECT)

```sql
SELECT  [DISTINCT] attribute_list
FROM    table_list
WHERE   condition
GROUP BY grouping_attrs
HAVING  group_condition
ORDER BY attribute [ASC|DESC]
LIMIT   n;
```

**Joins:**
```sql
-- Inner Join
SELECT * FROM A INNER JOIN B ON A.id = B.id;

-- Natural Join
SELECT * FROM A NATURAL JOIN B;

-- Left Outer Join
SELECT * FROM A LEFT OUTER JOIN B ON A.id = B.id;

-- Self Join
SELECT e1.Name, e2.Name AS Manager
FROM Employee e1, Employee e2
WHERE e1.ManagerID = e2.EmpID;
```

**Subqueries:**
```sql
-- IN / NOT IN
SELECT Name FROM Employee WHERE DeptID IN (SELECT DeptID FROM Department WHERE Loc='Delhi');

-- EXISTS / NOT EXISTS
SELECT Name FROM Employee e WHERE EXISTS (SELECT 1 FROM Dependent d WHERE d.EmpID = e.EmpID);

-- Correlated Subquery
SELECT Name FROM Employee e1 WHERE Salary > (SELECT AVG(Salary) FROM Employee e2 WHERE e1.DeptID = e2.DeptID);

-- WITH (Common Table Expression)
WITH HighEarners AS (SELECT * FROM Employee WHERE Salary > 80000)
SELECT * FROM HighEarners WHERE DeptID = 5;
```

**Aggregate Functions:** `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`
- `COUNT(*)` counts all rows; `COUNT(attr)` ignores NULLs.
- `HAVING` filters groups after `GROUP BY`; `WHERE` filters rows before grouping.

**Set Operations:**
```sql
SELECT ... UNION     SELECT ...   -- Removes duplicates
SELECT ... UNION ALL SELECT ...   -- Keeps duplicates
SELECT ... INTERSECT SELECT ...
SELECT ... EXCEPT    SELECT ...   -- (MINUS in Oracle)
```

### 3.4 Insert, Delete, Update

```sql
-- Insert
INSERT INTO Employee VALUES (101, 'Alice', '1990-01-01', 60000, 2);
INSERT INTO Employee (EmpID, Name) VALUES (102, 'Bob');
INSERT INTO Employee SELECT * FROM OldEmployee WHERE DeptID = 3;

-- Delete
DELETE FROM Employee WHERE EmpID = 101;
DELETE FROM Employee;   -- Deletes all rows

-- Update
UPDATE Employee SET Salary = Salary * 1.10 WHERE DeptID = 2;
UPDATE Employee SET DeptID = 3, Salary = 70000 WHERE EmpID = 101;
```

### 3.5 Views

- A **view** is a virtual table defined by a query; no physical storage.
- Provides logical data independence and security.

```sql
CREATE VIEW HighSalaryEmp AS
    SELECT EmpID, Name, Salary FROM Employee WHERE Salary > 70000;

SELECT * FROM HighSalaryEmp;

DROP VIEW HighSalaryEmp;
```

- **Updatable views:** Views on a single table without aggregates, DISTINCT, GROUP BY.
- **Materialized Views:** Physically stored result; must be refreshed.

### 3.6 Stored Procedures and Functions

```sql
-- Stored Procedure
CREATE PROCEDURE GiveRaise(IN dept INT, IN pct FLOAT)
BEGIN
    UPDATE Employee SET Salary = Salary * (1 + pct/100) WHERE DeptID = dept;
END;

CALL GiveRaise(2, 10);

-- Function
CREATE FUNCTION GetAvgSalary(dept INT) RETURNS DECIMAL(10,2)
BEGIN
    DECLARE avg_sal DECIMAL(10,2);
    SELECT AVG(Salary) INTO avg_sal FROM Employee WHERE DeptID = dept;
    RETURN avg_sal;
END;

SELECT GetAvgSalary(2);
```

**Difference:** Functions return a value and can be used in SELECT; procedures do not necessarily return a value.

### 3.7 Database Triggers

- A **trigger** is a procedure that executes automatically in response to an event.

```sql
CREATE TRIGGER CheckSalary
BEFORE INSERT ON Employee
FOR EACH ROW
BEGIN
    IF NEW.Salary < 0 THEN
        SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Salary cannot be negative';
    END IF;
END;
```

**Trigger Events:** INSERT, UPDATE, DELETE
**Trigger Timing:** BEFORE, AFTER, INSTEAD OF (for views)
**Granularity:** FOR EACH ROW (row-level), FOR EACH STATEMENT (statement-level)

### 3.8 SQL Injection

- An attack where malicious SQL code is inserted into input fields to manipulate the database.

**Vulnerable code (concatenation):**
```sql
query = "SELECT * FROM Users WHERE username='" + input + "'";
-- Input: ' OR '1'='1  → returns all rows
```

**Prevention:**
- Use **Prepared Statements / Parameterized Queries**.
- Use **Stored Procedures**.
- Input validation and escaping.
- Principle of least privilege for DB accounts.

```sql
-- Safe: Parameterized Query
PreparedStatement stmt = conn.prepareStatement("SELECT * FROM Users WHERE username = ?");
stmt.setString(1, input);
```

---

## 4. Normalization for Relational Databases

### 4.1 Functional Dependencies (FD)

- `X → Y` : Attribute set Y is **functionally dependent** on X; for any two tuples, same X value implies same Y value.
- **Trivial FD:** `X → Y` where `Y ⊆ X`.
- **Non-trivial FD:** `X → Y` where `Y ⊄ X`.

**Armstrong's Axioms (Sound and Complete):**

| Axiom | Rule |
|---|---|
| Reflexivity | If `Y ⊆ X`, then `X → Y` |
| Augmentation | If `X → Y`, then `XZ → YZ` |
| Transitivity | If `X → Y` and `Y → Z`, then `X → Z` |

**Derived Rules:**
- **Union:** `X→Y` and `X→Z` → `X→YZ`
- **Decomposition:** `X→YZ` → `X→Y` and `X→Z`
- **Pseudotransitivity:** `X→Y` and `WY→Z` → `WX→Z`

**Closure of X under F:** `X⁺` = all attributes functionally determined by X.
```
X⁺ = X
Repeat until no change:
    For each FD A→B in F:
        if A ⊆ X⁺ then X⁺ = X⁺ ∪ B
```

**Canonical Cover (Fc):** Minimal set of FDs equivalent to F.
- No extraneous attributes on left or right side.
- No redundant FDs.

### 4.2 Normal Forms

| Normal Form | Condition |
|---|---|
| **1NF** | All attributes have atomic (indivisible) values; no repeating groups |
| **2NF** | In 1NF + No partial dependency (non-prime attribute depends on entire primary key) |
| **3NF** | In 2NF + No transitive dependency (non-prime depends on non-prime) |
| **BCNF** | For every FD `X→Y`, X must be a superkey |
| **4NF** | In BCNF + No non-trivial multi-valued dependency unless left side is superkey |
| **5NF** | In 4NF + No non-trivial join dependency |

**Key Definitions:**
- **Prime Attribute:** Attribute that is part of any candidate key.
- **Non-prime Attribute:** Not part of any candidate key.
- **Partial Dependency:** Non-prime attribute depends on part of a composite primary key.
- **Transitive Dependency:** A → B and B → C, where B is not a candidate key.

**Multi-Valued Dependency (MVD):**
`X →→ Y` : For each value of X, the set of Y values is independent of the other attributes.

**Decomposition Properties:**
- **Lossless-Join Decomposition:** `R₁ ⋈ R₂ = R` (no spurious tuples). Test: `R₁ ∩ R₂ → R₁` or `R₁ ∩ R₂ → R₂`.
- **Dependency Preservation:** All FDs can be checked in the decomposed relations without joining.

**BCNF Decomposition Algorithm:**
```
While some relation R has FD X→Y violating BCNF:
    Decompose R into:
        R₁ = X ∪ Y
        R₂ = R − Y (keep X as the joining attribute)
```
Note: BCNF always gives lossless join but may not preserve dependencies.

**3NF Synthesis Algorithm:**
```
1. Find canonical cover Fc
2. For each FD X→Y in Fc, create relation schema XY
3. If no schema contains a candidate key of R, add one schema with a candidate key
4. Remove redundant schemas
```
Note: 3NF always preserves dependencies and gives lossless join.

### 4.3 Query Processing and Optimization

**Query Processing Steps:**
```
SQL Query → Parser → Relational Algebra Expression → Query Optimizer → Execution Plan → Query Executor → Result
```

**Query Optimization:**
- **Heuristic (Rule-based):** Apply transformation rules to get a better logical plan.
  - Perform `σ` (selection) as early as possible.
  - Perform `π` (projection) early to reduce tuple size.
  - Combine Cartesian product and selection into a join.
- **Cost-based:** Estimate cost (I/O, CPU, memory) for alternative plans; choose minimum.

**Join Algorithms:**
| Algorithm | Cost |
|---|---|
| Nested-Loop Join | `O(n × m)` block accesses |
| Block Nested-Loop | `O(n + n×m/B)` — B = buffer pages |
| Index Nested-Loop | Uses index on inner relation |
| Sort-Merge Join | Sort both, then merge: `O(n log n + m log m)` |
| Hash Join | Partition on join attribute: `O(n + m)` for large relations |

### 4.4 Transaction Processing

A **transaction** is a logical unit of work consisting of a sequence of operations.

**ACID Properties:**

| Property | Meaning |
|---|---|
| **Atomicity** | All operations complete or none do (all-or-nothing) |
| **Consistency** | Transaction brings DB from one consistent state to another |
| **Isolation** | Concurrent transactions appear to execute serially |
| **Durability** | Committed transactions persist despite failures |

**Transaction States:** Active → Partially Committed → Committed / Failed → Aborted

### 4.5 Concurrency Control Techniques

**Concurrency Problems:**

| Problem | Description |
|---|---|
| **Dirty Read** | Read uncommitted data of another transaction |
| **Non-repeatable Read** | Re-read gives different result due to update by another transaction |
| **Phantom Read** | Re-read returns new rows inserted by another transaction |
| **Lost Update** | Two transactions update same data; one update is lost |

**Schedules:**
- **Serial Schedule:** Transactions execute one after another; always consistent.
- **Serializable Schedule:** Equivalent to some serial schedule.
- **Conflict Serializability:** A schedule is conflict serializable if it can be transformed into a serial schedule by swapping non-conflicting operations.

**Precedence Graph (Serialization Graph):**
- Node for each transaction.
- Edge `Tᵢ → Tⱼ` if operation in Tᵢ conflicts with and precedes an operation in Tⱼ.
- Schedule is conflict serializable **if and only if** the precedence graph has **no cycles**.

**Two-Phase Locking (2PL):**
- **Growing Phase:** Acquire locks; no releases.
- **Shrinking Phase:** Release locks; no new acquires.
- 2PL guarantees conflict serializability.
- **Strict 2PL:** Release all exclusive locks only after commit/abort. Prevents dirty reads.
- **Rigorous 2PL:** Release all locks only after commit/abort.

**Lock Types:**
- **Shared (S) lock:** For read operations; multiple transactions can hold S-lock.
- **Exclusive (X) lock:** For write operations; only one transaction at a time.

**Lock Compatibility Matrix:**

|  | S | X |
|---|---|---|
| **S** | Compatible | Incompatible |
| **X** | Incompatible | Incompatible |

**Deadlock:**
- Circular waiting for locks.
- **Detection:** Wait-for graph; cycle = deadlock.
- **Prevention:** Order locks (wound-wait, wait-die protocols).
- **Avoidance:** Banker's algorithm.

**Timestamp Ordering:**
- Each transaction Tᵢ gets timestamp `TS(Tᵢ)`.
- Rules: If `TS(Tᵢ) < TS(Tⱼ)`, Tᵢ must access data before Tⱼ.
- `W-timestamp(Q)` and `R-timestamp(Q)` maintained for each data item Q.

**Multiversion Concurrency Control (MVCC):**
- Multiple versions of data maintained.
- Readers don't block writers; writers don't block readers.

**Isolation Levels (SQL Standard):**

| Level | Dirty Read | Non-repeatable Read | Phantom Read |
|---|---|---|---|
| Read Uncommitted | Possible | Possible | Possible |
| Read Committed | Not Possible | Possible | Possible |
| Repeatable Read | Not Possible | Not Possible | Possible |
| Serializable | Not Possible | Not Possible | Not Possible |

### 4.6 Database Recovery Techniques

**Types of Failures:** Transaction failure, System crash, Disk failure.

**Log-Based Recovery:**
- **Write-Ahead Log (WAL):** Log record written before data is written to disk.
- Log record format: `<T, X, old_value, new_value>`
- **Undo:** Restore old values for failed transactions.
- **Redo:** Re-apply new values for committed transactions.

**Recovery Algorithms:**

| Algorithm | Description |
|---|---|
| **Deferred Update (No-Undo/Redo)** | Changes not written to DB until commit; redo committed transactions |
| **Immediate Update (Undo/Redo)** | Changes written before commit; undo uncommitted, redo committed |
| **ARIES** | Industry standard; uses LSN (Log Sequence Number); Analysis → Redo → Undo phases |

**Checkpointing:**
- Periodically flush log and data to disk; write `<CHECKPOINT>` to log.
- On recovery, only process transactions after the last checkpoint.

**Shadow Paging:** Maintain two page tables (current and shadow); on commit, shadow becomes current.

### 4.7 Object and Object-Relational Databases

- **Object-Oriented DB (OODB):** Data stored as objects with attributes, methods, identity (OID), inheritance, encapsulation.
- **Object-Relational DB (ORDB):** Extends relational model with OO features — user-defined types (UDT), inheritance, complex attributes, methods.
- **OID:** Unique, system-generated object identifier; independent of attribute values.
- **Standards:** ODMG (Object Data Management Group) standard for OODB.

### 4.8 Database Security and Authorization

- **Authentication:** Verifying identity of users.
- **Authorization (Access Control):** Granting/revoking rights.
  - **Discretionary Access Control (DAC):** Owner grants privileges. SQL GRANT/REVOKE.
  - **Mandatory Access Control (MAC):** Based on security classifications (Top Secret, Secret, etc.).
  - **Role-Based Access Control (RBAC):** Permissions assigned to roles; users assigned roles.

```sql
GRANT SELECT, INSERT ON Employee TO user1 WITH GRANT OPTION;
REVOKE INSERT ON Employee FROM user1;
```

- **Grant Option:** Allows the grantee to grant the same privilege to others.
- **Authorization Graph:** Nodes = users/DBA; edges = grant relationships. Privilege revoked if no path from DBA exists.
- **Views for Security:** Restrict access to sensitive attributes by creating views.
- **Encryption:** AES, RSA for data at rest and in transit.
- **Audit Trail:** Log all DB access for monitoring.

---

## 5. Enhanced Data Models

### 5.1 Temporal Databases

- Store **time-varying data**; track history of changes.
- **Valid Time:** Time period when a fact is true in the real world.
- **Transaction Time:** Time period when a fact is stored in the database.
- **Bitemporal:** Both valid and transaction time tracked.
- Queries use temporal extensions like `AS OF`, `BETWEEN ... AND ...`.

### 5.2 Multimedia Databases

- Store and retrieve text, images, audio, video, graphics.
- Challenges: Large data size, complex similarity queries, real-time retrieval.
- **Content-Based Retrieval:** Retrieval based on content features (color, texture, shape), not metadata.
- Use specialized indexes: R-trees, KD-trees for spatial/multimedia data.

### 5.3 Deductive Databases

- Combine database capabilities with logic/rule inference.
- Use **Datalog** — a declarative logic programming language.
- **Extensional Database (EDB):** Base facts (stored relations).
- **Intensional Database (IDB):** Derived facts (rules).
- Can express recursive queries (e.g., transitive closure) that standard SQL cannot (without recursion extensions).

### 5.4 XML and Internet Databases

- **XML (eXtensible Markup Language):** Semi-structured, self-describing, hierarchical.
- **DTD / XML Schema:** Define structure/constraints of XML documents.
- **XPath:** Navigate XML document tree.
- **XQuery:** Query language for XML (like SQL for relational data).
- **XSLT:** Transform XML into other formats (HTML, plain text).
- **XML in RDBMS:** Store as CLOB, or shred into relational tables, or use native XML DB.

### 5.5 Mobile and Distributed Databases

**Mobile Databases:**
- Support disconnected operation; data cached on mobile device.
- Issues: Limited bandwidth, intermittent connectivity, power constraints.
- **Hoarding:** Prefetching data likely to be needed while disconnected.

**Geographic Information Systems (GIS):**
- Store and analyze spatial/geographic data.
- Data types: Point, Line, Polygon, Region.
- Operations: Spatial join, containment, proximity, overlay.
- **Spatial Indexes:** R-tree for multi-dimensional data.

**Genome Data Management:**
- Manage large-scale DNA/protein sequence data.
- Sequence alignment, pattern matching, biological queries.
- Specialized databases: GenBank, Swiss-Prot.

### 5.6 Distributed Databases

- Data distributed across multiple geographically separated sites.
- Connected via a network; appears as a single logical database.

**Advantages:** Improved reliability, performance, scalability, local autonomy.

**Transparency Levels:**
| Type | Meaning |
|---|---|
| **Fragmentation Transparency** | User unaware of how data is fragmented |
| **Replication Transparency** | User unaware of data copies |
| **Location Transparency** | User unaware of data location |

**Fragmentation:**
- **Horizontal:** Rows distributed across sites (like selection).
- **Vertical:** Columns distributed across sites (like projection; primary key kept in each fragment).
- **Mixed/Hybrid:** Combination of both.

**Distributed Query Processing:** Minimize data transfer cost across network.

**Distributed Concurrency Control:**
- **Distributed 2PL:** Lock coordinator at each site.
- **Timestamp ordering** across sites.

**Distributed Recovery:**
- **Two-Phase Commit (2PC):**
  - Phase 1 (Voting): Coordinator sends PREPARE; participants vote YES or NO.
  - Phase 2 (Commit): If all YES → COMMIT broadcast; else ABORT broadcast.

**CAP Theorem:** A distributed system can guarantee at most **2 of 3**:
- **C**onsistency — all nodes see same data.
- **A**vailability — every request gets a response.
- **P**artition Tolerance — system continues despite network partition.

---

## 6. Data Warehousing and Data Mining

### 6.1 Data Warehousing

- A **data warehouse** is a subject-oriented, integrated, time-variant, non-volatile collection of data for decision support.

**OLTP vs OLAP:**

| Aspect | OLTP | OLAP |
|---|---|---|
| Purpose | Day-to-day operations | Analysis and reporting |
| Data | Current, detailed | Historical, summarized |
| Operations | INSERT, UPDATE, DELETE | SELECT (complex queries) |
| Schema | Normalized | Denormalized (Star, Snowflake) |
| Users | Clerks, front-end users | Analysts, managers |
| Response Time | Milliseconds | Seconds to minutes |

**Data Warehouse Schema:**
- **Star Schema:** Central fact table connected to dimension tables. Simple, fast queries.
- **Snowflake Schema:** Dimension tables normalized into sub-dimensions. Saves space; complex joins.
- **Galaxy Schema (Fact Constellation):** Multiple fact tables sharing dimension tables.

**Fact Table:** Contains measures (quantitative data) and foreign keys to dimensions.
**Dimension Table:** Contains descriptive attributes (who, what, where, when).

### 6.2 Concept Hierarchy

- Organizes concepts at different levels of abstraction.
- Example: City → Province → Country → Continent.
- Enables **drill-down** (more detail) and **roll-up** (less detail) operations.

### 6.3 OLAP Operations

| Operation | Description |
|---|---|
| **Roll-up** | Aggregate data; climb up hierarchy (less detail) |
| **Drill-down** | Disaggregate data; move down hierarchy (more detail) |
| **Slice** | Select one dimension value; reduces dimensionality by 1 |
| **Dice** | Select range of values for 2+ dimensions; sub-cube |
| **Pivot (Rotate)** | Rotate data cube for alternative presentation |

**OLAP Types:**
- **MOLAP:** Multidimensional storage; fast; precomputed cubes.
- **ROLAP:** Relational storage; scalable; slower.
- **HOLAP:** Hybrid; summary in multidimensional, detail in relational.

### 6.4 Data Mining Techniques

**Association Rules:**
- Find correlations: `X ⟹ Y`
- **Support:** `sup(X ∪ Y) = (transactions containing both X and Y) / (total transactions)`
- **Confidence:** `conf(X ⟹ Y) = sup(X ∪ Y) / sup(X)`
- **Lift:** `lift(X ⟹ Y) = conf(X ⟹ Y) / sup(Y)` — values > 1 indicate positive correlation.
- **Apriori Algorithm:** Generate frequent itemsets using anti-monotone property (all subsets of a frequent itemset must be frequent).
- **FP-Growth:** Mines frequent patterns without candidate generation; uses FP-tree.

**Classification:**
- Predicts categorical class label for new instances.
- **Decision Tree (ID3, C4.5, CART):** Splits on attribute with highest information gain.
  - `Entropy(S) = −Σ pᵢ log₂ pᵢ`
  - `Information Gain(S, A) = Entropy(S) − Σ (|Sᵥ|/|S|) × Entropy(Sᵥ)`
- **Naive Bayes:** `P(C|X) ∝ P(C) × Π P(xᵢ|C)` — assumes attribute independence.
- **Neural Networks:** Multi-layer perceptrons; backpropagation learning.
- **Random Forest:** Ensemble of decision trees.

**Support Vector Machine (SVM):**
- Finds optimal hyperplane that maximizes the margin between classes.
- **Margin** = distance between hyperplane and nearest data points (support vectors).
- `Maximize: 2/||w||` subject to `yᵢ(w·xᵢ + b) ≥ 1` for all i.
- **Kernel trick:** Maps data to higher dimensions for non-linear classification. Kernels: Linear, Polynomial, RBF (Gaussian).

**K-Nearest Neighbour (K-NN):**
- Classify new point based on majority class of K nearest neighbours.
- Distance metrics: Euclidean `d = √Σ(xᵢ−yᵢ)²`, Manhattan `d = Σ|xᵢ−yᵢ|`.
- Lazy learner (no explicit training); sensitive to choice of K and irrelevant features.

**Clustering:**
- Unsupervised grouping of similar data points.
- **K-Means:**
  1. Initialize K centroids randomly.
  2. Assign each point to nearest centroid.
  3. Recompute centroids as mean of assigned points.
  4. Repeat until convergence.
  - Objective: Minimize `Σ Σ ||x − μᵢ||²`
- **Hierarchical Clustering:** Agglomerative (bottom-up) or Divisive (top-down); produces dendrogram.
- **DBSCAN:** Density-based; finds arbitrary shaped clusters; handles noise/outliers.

**Regression:**
- Predicts continuous numerical value.
- **Linear Regression:** `Y = β₀ + β₁X₁ + β₂X₂ + ... + βₙXₙ + ε`
- Minimize: `Σ(yᵢ − ŷᵢ)²` (least squares).
- **Logistic Regression:** For binary classification; uses sigmoid function `σ(z) = 1/(1 + e⁻ᶻ)`.

**Hidden Markov Model (HMM):**
- Statistical model for sequential/temporal data.
- States: hidden (unobservable); observations: visible.
- Defined by: Initial probabilities `π`, Transition probabilities `A = {aᵢⱼ}`, Emission probabilities `B = {bⱼ(k)}`.
- **Three problems:**
  1. **Evaluation:** P(observation | model) — Forward algorithm.
  2. **Decoding:** Best state sequence — Viterbi algorithm.
  3. **Learning:** Estimate model parameters — Baum-Welch (EM) algorithm.
- Applications: Speech recognition, NLP, bioinformatics.

**Other Data Mining Methods:**

| Method | Description |
|---|---|
| **Summarization** | Create compact descriptions of data subsets |
| **Dependency Modeling** | Find relationships/dependencies among variables; Bayesian networks |
| **Link Analysis** | Analyze relationships between entities; PageRank |
| **Sequence Analysis** | Mine patterns in ordered sequences (web clickstreams, time series) |
| **Social Network Analysis** | Study structure and properties of social graphs; centrality, community detection |

---

## 7. Big Data Systems

### 7.1 Big Data Characteristics (5 V's)

| V | Description |
|---|---|
| **Volume** | Massive amounts of data (petabytes, exabytes) |
| **Velocity** | Speed of data generation and processing |
| **Variety** | Structured, semi-structured, unstructured data types |
| **Veracity** | Uncertainty and trustworthiness of data |
| **Value** | Business value extracted from data |

### 7.2 Types of Big Data

- **Structured:** Relational tables, CSV.
- **Semi-structured:** XML, JSON, log files.
- **Unstructured:** Text, images, video, audio, social media.

### 7.3 Big Data Architecture

**Lambda Architecture:**
- **Batch Layer:** Processes all data; high latency but accurate.
- **Speed Layer:** Processes recent data in real-time; low latency.
- **Serving Layer:** Merges batch and real-time views for queries.

**Kappa Architecture:** Simplified; eliminates batch layer; everything processed as streams.

### 7.4 MapReduce

A programming model for processing large datasets in parallel across a cluster.

**Phases:**
1. **Map:** Input key-value pairs → intermediate key-value pairs. `(k₁, v₁) → list(k₂, v₂)`
2. **Shuffle and Sort:** Group intermediate values by key.
3. **Reduce:** Aggregate intermediate values per key → output. `(k₂, list(v₂)) → list(v₃)`

**Word Count Example:**
```
Map:    (doc, "the cat sat") → (the,1), (cat,1), (sat,1)
Reduce: (the, [1,1,1])      → (the, 3)
```

**Properties:** Fault-tolerant; scalable; data locality (move computation to data).

### 7.5 Hadoop Ecosystem

| Component | Role |
|---|---|
| **HDFS** | Distributed file system for storage |
| **MapReduce** | Batch processing framework |
| **YARN** | Resource management and job scheduling |
| **Hive** | SQL-like queries on Hadoop (HiveQL) |
| **Pig** | Data flow scripting language (Pig Latin) |
| **HBase** | Column-family NoSQL DB on top of HDFS |
| **Spark** | In-memory fast processing; 100x faster than MR |
| **Zookeeper** | Coordination and configuration management |
| **Sqoop** | Import/export between RDBMS and Hadoop |
| **Flume** | Log/event data ingestion into HDFS |

### 7.6 HDFS (Hadoop Distributed File System)

- Designed for large files on commodity hardware.
- **Block size:** Default 128 MB (earlier 64 MB).
- **Replication factor:** Default 3 copies.
- **NameNode:** Master; manages file system namespace and metadata.
- **DataNode:** Worker; stores actual data blocks.
- **Secondary NameNode:** Periodically merges edit log with fsimage; NOT a backup NameNode.

**Read:** Client → NameNode (get block locations) → DataNode (read blocks).
**Write:** Client → NameNode (create file) → pipeline of DataNodes → acknowledgment back.

**Fault Tolerance:** Block replication across different racks. NameNode detects DataNode failure via heartbeat.

---

## 8. NoSQL Databases

### 8.1 NoSQL Overview

- Not Only SQL; designed for scalability, flexibility, performance.
- Schema-less or flexible schema.
- Sacrifice some ACID properties for availability and performance.
- Follow **BASE:** Basically Available, Soft state, Eventual consistency.

**When to use NoSQL:** Large volumes, unstructured data, high scalability, rapid schema changes.

### 8.2 Types of NoSQL Databases

| Type | Storage | Examples | Use Case |
|---|---|---|---|
| **Key-Value** | Hash map of key-value pairs | Redis, Riak, DynamoDB | Sessions, caching, shopping carts |
| **Document** | JSON/BSON documents | MongoDB, CouchDB | Content management, catalogs |
| **Column-Family** | Column families (rows + dynamic columns) | HBase, Cassandra | Time-series, analytics, logging |
| **Graph** | Nodes and edges with properties | Neo4j, Amazon Neptune | Social networks, recommendation engines |

### 8.3 Querying NoSQL

- **Key-Value:** `GET key`, `SET key value`, `DELETE key` — no complex queries.
- **Document (MongoDB):**
```javascript
db.employees.find({ salary: { $gt: 50000 } })
db.employees.insertOne({ name: "Alice", salary: 60000 })
db.employees.updateOne({ name: "Alice" }, { $set: { salary: 70000 } })
db.employees.deleteOne({ name: "Alice" })
```
- **CQL (Cassandra Query Language):** SQL-like; but limited joins; partition key is critical.
- **Graph (Cypher for Neo4j):**
```
MATCH (a:Person)-[:FRIEND]->(b:Person) WHERE a.name = "Alice" RETURN b.name
```

### 8.4 Indexing and Ordering in NoSQL

- **Primary Index:** On partition/row key — automatic.
- **Secondary Index:** On non-key attributes — supported in MongoDB, Cassandra.
- **Composite Index:** Index on multiple fields.
- **Inverted Index:** Maps content to its location; used in full-text search (Elasticsearch).
- **Ordering:** Documents sorted by index or sort key; B-tree or LSM-tree (Log-Structured Merge-tree) used internally.

**LSM-Tree (used in Cassandra, HBase):**
- Writes go to in-memory MemTable → flushed to SSTable (Sorted String Table) on disk.
- Periodic compaction merges SSTables.
- Optimized for write-heavy workloads.

### 8.5 Query Optimization in NoSQL

- Choose right partition key to avoid hot spots.
- Design data model around query patterns (denormalization, embedding).
- Use compound indexes for multi-field queries.
- Avoid large scans; use pagination.
- Caching layers (Redis) to reduce DB load.

### 8.6 NoSQL in Cloud

| Cloud Provider | NoSQL Services |
|---|---|
| **AWS** | DynamoDB (key-value/document), Amazon Neptune (graph), ElastiCache (Redis) |
| **Google Cloud** | Firestore, Bigtable, Datastore |
| **Azure** | Cosmos DB (multi-model: key-value, document, graph, column-family) |

**Cloud NoSQL Features:**
- Auto-scaling, managed replication, global distribution.
- Pay-per-use pricing.
- Built-in backup and disaster recovery.
- Multi-region consistency levels (strong, eventual, session).

---

## Quick Recap Table

| Topic | Key Concepts |
|---|---|
| Architecture | Three-Schema, Data Independence, DDL/DML/DCL |
| ER Model | Entity, Attribute, Cardinality, EER (Generalization, Specialization) |
| Relational Algebra | σ, π, ∪, −, ×, ⋈, ÷ ; Conflict Serializability |
| Codd's Rules | 12 rules; Rule 0 (foundation) to Rule 12 (non-subversion) |
| SQL | DDL, DML, Views, Triggers, Stored Procedures, SQL Injection |
| Normalization | 1NF→2NF→3NF→BCNF; FD, Armstrong's Axioms, Closure, Canonical Cover |
| Decomposition | Lossless Join + Dependency Preservation |
| Transactions | ACID; Serial vs Serializable; 2PL; Deadlock; Isolation Levels |
| Recovery | WAL, Undo/Redo, Checkpoint, 2PC |
| Security | DAC, MAC, RBAC; GRANT/REVOKE; Encryption |
| Data Warehouse | Star/Snowflake schema; Roll-up, Drill-down, Slice, Dice, Pivot |
| Mining | Support/Confidence/Lift; Apriori; Decision Tree; SVM; K-Means; HMM |
| Big Data | 5 V's; Lambda Architecture; MapReduce; HDFS NameNode/DataNode |
| NoSQL | Key-Value, Document, Column-Family, Graph; BASE; CAP Theorem; LSM-Tree |

---

*Notes prepared for UGC NET Computer Science – Unit 4*
