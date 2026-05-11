## Database

| Term | Description |
|---|---|
| Database | Collection of related data |
| Facts | Represents known facts |
| Nature | Data should be logically connected |

### Implicit Properties of Database

| Property | Meaning |
|---|---|
| Miniworld | Represents a subset of the real world |
| Logical Coherence | Data has inherent meaning |
| Specific Purpose | Built for a particular application |

---

# DBMS (Database Management System)

| Feature | Description |
|---|---|
| Definition | Collection of programs |
| Type | General purpose software |
| Functions | Defining, constructing, manipulating and sharing databases |

---

## Metadata

| Term | Meaning |
|---|---|
| Metadata | Information about the database |

---

# Characteristics of Database Approach

| Characteristic | Description |
|---|---|
| Self-describing | Stores metadata along with data |
| Program-Data Insulation | Separation between programs and data |
| Data Abstraction | Hides implementation details |
| Multi-user Sharing | Multiple users can access data |

---

# DBA (Database Administrator)

| Responsibility | Work |
|---|---|
| Authorized Access | Controls permissions |
| Monitoring | Monitors database activities |
| Coordination | Coordinates users and operations |
| Resource Management | Acquires software and hardware |
| Accountability | Maintains security and responsibility |

---

# Database Design Concepts

## Database Design

| Aspect | Description |
|---|---|
| Purpose | Identify data to be stored |
| Structure Selection | Choose suitable representation structure |

---

## Database Schema

| Property | Description |
|---|---|
| Meaning | Overall description of database |
| Defined During | Database design phase |
| Change Frequency | Does not change frequently |

---

## Data Model

| Aspect | Description |
|---|---|
| Definition | Blueprint of database |
| Purpose | Collection of concepts for describing data |
| Additional Role | Provides abstraction |

---

## Instance and Database State

| Term | Meaning |
|---|---|
| Instance | Actual values stored |
| Database State | Data at a particular moment |
| Snapshot | Another name for database state |

---

# Database Architectures

## Three Schema Architecture

| Level | Purpose |
|---|---|
| External Level | User view |
| Conceptual Level | Overall logical structure |
| Internal Level | Physical storage |

### Main Goal
- Separation between user, application and physical database levels
- Provides abstraction and data independence

---

## Two Schema Architecture

| Feature | Description |
|---|---|
| Connection | Direct interaction between client and database |

---

# Mapping

| Term | Meaning |
|---|---|
| Mapping | Transformation of requests and results between schema levels |

---

# Data Independence

| Type | Description |
|---|---|
| Logical Data Independence | Change conceptual schema without affecting external schema |
| Physical Data Independence | Change internal schema without affecting conceptual schema |

> External schema changes may still occur in some cases.

# Data Models

| Model | Description |
|---|---|
| Relational Model | Data organized in the form of relations (tables) |
| Hierarchical Model | Tree-like structure with one-to-many relationship |
| Network Model | Supports many-to-many relationships |
| Object-Oriented Model | Data represented as objects |
| ER Model | Represents entities and relationships |

---

# ER (Entity Relationship) Model

## Entity

| Term | Description |
|---|---|
| Entity | Anything that exists in the real world |
| Types | Can exist physically or conceptually |

---

## Attributes

| Term | Description |
|---|---|
| Attribute | Property that defines an entity |
| Attribute Value | Particular value associated with an entity |

---

# Types of Attributes

## 1. Composite vs Simple Attribute

| Type | Description | Representation |
|---|---|---|
| Composite Attribute | Can be divided into subparts | `( )` |
| Simple Attribute | Atomic and non-divisible | Single value |

---

## 2. Single-valued vs Multi-valued Attribute

| Type | Description | Representation |
|---|---|---|
| Single-valued Attribute | Holds only one value | Single value |
| Multi-valued Attribute | Holds multiple values | `{ }` |

---

## 3. Stored vs Derived Attribute

| Type | Description |
|---|---|
| Stored Attribute | Fixed and directly stored |
| Derived Attribute | Obtained from another attribute |

---

## 4. Complex Attribute

| Type | Description | Representation |
|---|---|---|
| Complex Attribute | Both composite and multivalued | `{(_,_,_)}` |

---

# Relationship Set

## Degree of Relationship Set

| Degree | Description |
|---|---|
| Unary | One entity set participates |
| Binary | Two entity sets participate |
| Ternary | Three entity sets participate |

> Most relationships are binary.

---

# Cardinality Ratios for Binary Relationships

| Cardinality | Meaning |
|---|---|
| 1 : 1 | One entity related to one entity |
| 1 : N | One entity related to many entities |
| N : 1 | Many entities related to one entity |
| N : M | Many-to-many relationship |

---

# Participation Constraints

| Type | Description | Representation |
|---|---|---|
| Total Participation | Every entity participates in at least one relationship | Double line |
| Partial Participation | Some entities may not participate in any relationship | Single line |

---
> Total participation implies existence dependency.
> Partial participation allows independent existence of entities.
