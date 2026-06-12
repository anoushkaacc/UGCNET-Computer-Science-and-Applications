# UGC NET – Unit 3: Programming Languages and Computer Graphics
---

## 1. Language Design and Translation Issues

### 1.1 Programming Language Concepts

- A **programming language** is a formal notation for expressing algorithms and data structures.
- **Syntax:** Rules governing structure of valid programs (grammar).
- **Semantics:** Meaning of syntactically valid programs.
- **Pragmatics:** Practical aspects — readability, writability, reliability, efficiency.

**Criteria for Language Design:**
- Simplicity and orthogonality (few concepts, freely combinable).
- Control and data abstraction.
- Program correctness and type checking.
- Efficient implementation.

### 1.2 Programming Paradigms and Models

| Paradigm | Key Concept | Examples |
|---|---|---|
| **Imperative (Procedural)** | Sequence of statements; state change | C, Pascal, Fortran |
| **Object-Oriented (OOP)** | Objects encapsulating data and methods | C++, Java, Python |
| **Functional** | Computation as evaluation of functions; no side effects | Haskell, Lisp, ML |
| **Logic (Declarative)** | State what to compute, not how; rules and facts | Prolog |
| **Concurrent** | Multiple computations simultaneously | Erlang, Go |
| **Scripting** | High-level glue code; interpreted | Python, JavaScript, Perl |
| **Event-Driven** | Flow determined by events | JavaScript, Visual Basic |

### 1.3 Programming Environments

- Collection of tools supporting software development.
- **Components:** Editor, Compiler/Interpreter, Linker, Loader, Debugger, Profiler, Version Control, Build System.
- **IDE (Integrated Development Environment):** All tools integrated (Eclipse, VS Code, IntelliJ).
- **REPL (Read-Eval-Print Loop):** Interactive shell for interpreted languages (Python shell, LISP REPL).

### 1.4 Virtual Computers and Binding Times

**Virtual Computer (Abstract Machine):**
- Interpreter for a language defines a virtual machine for that language.
- Each language has an implicit virtual machine that executes its operations.
- **Example:** JVM (Java Virtual Machine) — Java compiles to bytecode; JVM interprets/JIT-compiles bytecode.

**Binding:** Association of a name with a property (type, value, location, etc.).

**Binding Times:**

| Binding Time | When Bound | Example |
|---|---|---|
| **Language Design Time** | When language is defined | Meaning of `+` operator |
| **Language Implementation Time** | When compiler written | Integer size (often) |
| **Compile Time** | During compilation | Variable type in C/C++ |
| **Link Time** | During linking | Address of external function |
| **Load Time** | When program loaded | Base address of program |
| **Runtime** | During execution | Value of variable; dynamic dispatch |

**Static Binding:** Before runtime; faster; less flexible.
**Dynamic Binding:** At runtime; flexible; slower; basis of polymorphism.

### 1.5 Programming Language Syntax

**Formal Specification:**
- **BNF (Backus-Naur Form):** Grammar notation for syntax.
  - Terminal symbols: actual tokens (keywords, operators).
  - Non-terminals: syntactic categories (in angle brackets `<expr>`).
  - Productions: `<expr> ::= <expr> + <term> | <term>`
- **EBNF (Extended BNF):** Adds `{ }` (repetition), `[ ]` (optional), `( )` (grouping).
- **Syntax Diagrams (Railroad Diagrams):** Graphical equivalent of BNF.

**BNF Example for Expressions:**
```
<expr>   ::= <expr> + <term> | <expr> - <term> | <term>
<term>   ::= <term> * <factor> | <term> / <factor> | <factor>
<factor> ::= ( <expr> ) | <identifier> | <number>
```

**Ambiguous Grammar:** More than one parse tree for some string.
- Example: `<expr> ::= <expr> + <expr> | <expr> * <expr> | id` — ambiguous.
- Solution: Rewrite with precedence and associativity built in.

### 1.6 Stages in Translation

```
Source Code
    ↓
[Lexical Analysis (Scanner)] → Token stream
    ↓
[Syntax Analysis (Parser)] → Parse tree / AST
    ↓
[Semantic Analysis] → Annotated AST; type checking; symbol table
    ↓
[Intermediate Code Generation] → Three-address code / IR
    ↓
[Code Optimisation] → Optimised IR
    ↓
[Code Generation] → Target machine code / Assembly
    ↓
[Assembler/Linker/Loader] → Executable
```

**Front End:** Lexical + Syntax + Semantic analysis (machine-independent).
**Back End:** Code generation + Optimisation (machine-dependent).

**Symbol Table:** Stores identifier information (name, type, scope, location); updated during all phases.

**Error Types:**
- Lexical: Invalid token (e.g., `@` not in language).
- Syntax: Malformed structure (e.g., missing `}`).
- Semantic: Type mismatch; undeclared variable.
- Runtime: Division by zero; null pointer.

### 1.7 Formal Translation Models

**Finite Automaton (FA):** Lexical analysis; recognises regular languages.
**Pushdown Automaton (PDA):** Syntax analysis; recognises context-free languages.
**Turing Machine:** Semantics and computability.

**Chomsky Hierarchy (recap):**
- Regular (FA) → Context-Free (PDA) → Context-Sensitive (LBA) → Recursively Enumerable (TM).

**Regular Expressions → NFA (Thompson) → DFA (Subset construction) → Minimised DFA → Scanner code.**
**CFG → LL(1) or LR(1) parsing tables → Parser.**

---

## 2. Elementary Data Types

### 2.1 Properties of Types and Objects

**Data Type:** Defines a set of values and the operations applicable to those values.
- **Type checking:** Ensure operations are applied to compatible types.
- **Strong typing:** All type errors detected (Java, Haskell).
- **Weak typing:** Implicit coercions allowed (C, JavaScript).
- **Static typing:** Types checked at compile time (C, Java).
- **Dynamic typing:** Types checked at runtime (Python, JavaScript).

**Object Properties:**
- **Value:** Data stored in object.
- **Type:** Set of valid values and operations.
- **Location (L-value):** Memory address.
- **Name (identifier):** Symbolic reference.
- **Lifetime:** Period during which object exists.
- **Scope:** Region of program where name is visible.

**Scope Rules:**
- **Static (Lexical) Scoping:** Scope determined by program text at compile time. Most languages.
- **Dynamic Scoping:** Scope determined by call stack at runtime (older Lisps, Emacs Lisp).

**Lifetime of Variables:**
| Storage Class | Lifetime | Allocation |
|---|---|---|
| **Static** | Entire program run | Compile time (data segment) |
| **Stack (Automatic)** | Procedure invocation | Runtime (stack frame) |
| **Heap (Dynamic)** | `malloc`/`new` to `free`/`delete` | Runtime (heap) |

### 2.2 Scalar Data Types

Single, indivisible values.

| Type | Description | Examples |
|---|---|---|
| **Integer** | Whole numbers; signed/unsigned; various widths | `int`, `long`, `short` |
| **Float/Double** | IEEE 754 floating point | `float` (32), `double` (64) |
| **Character** | Single character; ASCII or Unicode | `char` |
| **Boolean** | True or False | `bool`, `boolean` |
| **Enumeration** | Named integer constants | `enum Day {MON, TUE, ...}` |
| **Pointer** | Memory address | `int *p` |
| **Ordinal** | Types with predecessor/successor (int, char, enum) | — |

**Type Coercion (implicit conversion):** Narrowing (may lose data) vs Widening (safe).
- Widening: `int → long → float → double`.

### 2.3 Composite Data Types

Built from simpler types.

| Type | Description | Access |
|---|---|---|
| **Array** | Homogeneous; contiguous memory; fixed size | Index: `a[i]` |
| **Record (Struct)** | Heterogeneous; named fields | Field name: `s.field` |
| **Union** | Same memory for different types | Only one active at a time |
| **String** | Sequence of characters; may be mutable/immutable | Index or operations |
| **Set** | Unordered collection of distinct values | Membership, union, intersection |
| **Pointer** | Reference to another object | Dereference: `*p` |
| **List** | Ordered sequence; dynamic size | Head, tail, indexing |
| **File** | Sequence of components on storage | Read, write, seek |

**Array Storage:**
- **Row-major (C):** Row elements stored contiguously.
  - `A[i][j]` at: `base + (i × n_cols + j) × element_size`
- **Column-major (Fortran):** Column elements stored contiguously.
  - `A[i][j]` at: `base + (j × n_rows + i) × element_size`

**Array Descriptor (Dope Vector):** Base address, element type/size, number of dimensions, index bounds for each dimension, stride for each dimension.

---

## 3. Programming in C

### 3.1 Tokens and Identifiers

**Tokens:** Keywords, identifiers, constants, string literals, operators, punctuators.

**Keywords (32 in C89):** `auto, break, case, char, const, continue, default, do, double, else, enum, extern, float, for, goto, if, int, long, register, return, short, signed, sizeof, static, struct, switch, typedef, union, unsigned, void, volatile, while`

**Identifier Rules:** Start with letter or underscore; followed by letters, digits, underscores; case-sensitive; cannot be keyword.

### 3.2 Data Types in C

| Type | Size (typical) | Range |
|---|---|---|
| `char` | 1 byte | −128 to 127 (signed) |
| `unsigned char` | 1 byte | 0 to 255 |
| `short` | 2 bytes | −32,768 to 32,767 |
| `int` | 4 bytes | −2^31 to 2^31−1 |
| `long` | 4 or 8 bytes | — |
| `long long` | 8 bytes | −2^63 to 2^63−1 |
| `float` | 4 bytes | ≈ ±3.4×10^38 (7 digits) |
| `double` | 8 bytes | ≈ ±1.8×10^308 (15 digits) |
| `long double` | 10/12/16 bytes | — |

**Type Qualifiers:** `const` (value cannot change), `volatile` (may change externally), `restrict` (no aliasing — C99).

**Storage Classes:**
| Class | Scope | Lifetime | Default Value |
|---|---|---|---|
| `auto` | Local block | Block duration | Undefined |
| `register` | Local block | Block duration; stored in register (hint) | Undefined |
| `static` | Local (if in function) or file (if global) | Program duration | Zero |
| `extern` | File/global | Program duration | Zero |

### 3.3 Sequence Control in C

**Expressions and Operators (Precedence, high to low):**
```
() [] -> .                  (postfix)
! ~ ++ -- - * & (type) sizeof (unary prefix)
* / %                       (multiplicative)
+ -                         (additive)
<< >>                       (shift)
< <= > >=                   (relational)
== !=                       (equality)
&                           (bitwise AND)
^                           (bitwise XOR)
|                           (bitwise OR)
&&                          (logical AND)
||                          (logical OR)
?:                          (conditional/ternary)
= += -= *= /= %= &= |= ^= <<= >>= (assignment)
,                           (comma)
```

**Control Structures:**
```c
/* if-else */
if (condition) { ... } else { ... }

/* switch */
switch(expr) { case val: ...; break; default: ...; }

/* for loop */
for(init; condition; update) { ... }

/* while */
while(condition) { ... }

/* do-while */
do { ... } while(condition);

/* goto (avoid) */
goto label; ... label: ...
```

**`break`:** Exit loop or switch.
**`continue`:** Skip to next loop iteration.

### 3.4 Arrays in C

```c
int a[10];                        // 1D array, indices 0-9
int b[3][4];                      // 2D array, 3 rows, 4 columns
int c[] = {1, 2, 3, 4};          // initialised; size = 4

/* 2D element address */
// a[i][j] is at: base_addr + (i*4 + j) * sizeof(int)
```

- Array name = pointer to first element.
- `a[i]` ≡ `*(a + i)`.
- Arrays passed to functions as pointers (not copied).
- Bounds not checked at runtime (undefined behaviour on overflow).

**Variable-Length Arrays (VLA, C99):** Array size determined at runtime: `int a[n];`.

### 3.5 Structures, Unions, and Enumerations

```c
/* Structure */
struct Student {
    int id;
    char name[50];
    float gpa;
};
struct Student s = {101, "Alice", 3.9};
s.gpa = 3.95;

/* Typedef */
typedef struct { int x; int y; } Point;
Point p = {3, 4};

/* Union */
union Data {
    int i;
    float f;
    char c;
};
/* Only one member valid at a time; size = size of largest member */

/* Enum */
enum Color { RED = 0, GREEN = 1, BLUE = 2 };
```

**Structure Padding:** Compiler may insert padding bytes for alignment.
- `sizeof(struct)` ≥ sum of `sizeof(members)`.

### 3.6 Strings in C

- Character array terminated by null character `'\0'`.
- `char str[] = "Hello";` → `{'H','e','l','l','o','\0'}`.
- String length: `strlen(str)` (excludes `'\0'`).

**Common String Functions (`<string.h>`):**
```c
strlen(s)           // length (excluding '\0')
strcpy(dst, src)    // copy src to dst (unsafe; use strncpy)
strncpy(dst, src, n)// copy at most n chars
strcat(dst, src)    // concatenate src to end of dst
strcmp(s1, s2)      // compare; returns 0 if equal, <0 or >0
strchr(s, c)        // first occurrence of char c in s
strstr(s1, s2)      // first occurrence of s2 in s1
sprintf(buf, fmt, ...)  // print to string
```

### 3.7 Pointers in C

```c
int x = 10;
int *p = &x;       // p holds address of x
*p = 20;           // dereference; x is now 20
int **pp = &p;     // pointer to pointer

/* Pointer arithmetic */
int arr[5] = {1,2,3,4,5};
int *q = arr;
q++;               // moves to next int (q += sizeof(int) bytes)
*(q+2)             // arr[3]

/* NULL pointer */
int *ptr = NULL;   // pointer to nothing; dereference is undefined behaviour

/* Function pointer */
int (*fp)(int, int);   // pointer to function taking two ints, returning int
fp = &add;
int result = fp(3, 4);
```

**Pointer vs Array:** Array name is a constant pointer; cannot reassign. Pointer is a variable.

**Dynamic Memory Allocation:**
```c
#include <stdlib.h>
int *p = (int*) malloc(n * sizeof(int));   // allocate
int *q = (int*) calloc(n, sizeof(int));    // allocate and zero
p = (int*) realloc(p, new_size);           // resize
free(p);                                   // deallocate
```

**Common Pointer Errors:** Dangling pointer, memory leak, double free, buffer overflow, uninitialized pointer.

### 3.8 Functions in C

```c
/* Function declaration (prototype) */
int add(int a, int b);

/* Definition */
int add(int a, int b) {
    return a + b;
}

/* Call by value: copy of argument passed */
void swap_fail(int a, int b) { int t=a; a=b; b=t; }

/* Call by reference (via pointer): address passed */
void swap_ok(int *a, int *b) { int t=*a; *a=*b; *b=t; }
swap_ok(&x, &y);

/* Recursion */
int factorial(int n) {
    if (n <= 1) return 1;
    return n * factorial(n-1);
}
```

**Scope and Lifetime:**
- Local variables: `auto` by default; exist only within function.
- `static` local: Persists across calls; initialised once.
- `extern`: Declared in one file; defined in another.

### 3.9 Subprogram Control

**Call Stack:** Activation records (stack frames) pushed on function call; popped on return.
**Activation Record Contents:** Return address, local variables, parameters, saved registers, frame pointer, dynamic link.

**Recursion:** Stack grows with each recursive call; base case terminates recursion.

**Parameter Passing:**
- **Call by Value:** Copy of argument; original unchanged. (C default for scalars)
- **Call by Reference:** Address of argument; modifications affect original. (C with pointers, C++ with `&`)
- **Call by Value-Result:** Copy in; copy out on return.
- **Call by Name:** Textual substitution; lazy evaluation.

### 3.10 File Handling in C

```c
#include <stdio.h>
FILE *fp;

/* Opening */
fp = fopen("file.txt", "r");   // modes: r, w, a, rb, wb, r+, w+, a+
if (fp == NULL) { perror("Error"); exit(1); }

/* Reading and writing */
fgetc(fp);                   // read one char
fputc(c, fp);                // write one char
fgets(buf, n, fp);           // read line (up to n-1 chars + '\0')
fputs(str, fp);              // write string
fscanf(fp, "%d", &x);        // formatted read
fprintf(fp, "%d\n", x);      // formatted write
fread(buf, size, count, fp); // binary read
fwrite(buf, size, count, fp);// binary write

/* Position */
fseek(fp, offset, SEEK_SET); // SEEK_SET(0), SEEK_CUR(1), SEEK_END(2)
ftell(fp);                   // current position
rewind(fp);                  // rewind to beginning

/* Closing */
fclose(fp);

/* Error and EOF */
feof(fp);    // non-zero if end of file
ferror(fp);  // non-zero if error
```

### 3.11 Command Line Arguments

```c
int main(int argc, char *argv[]) {
    // argc: number of arguments (including program name)
    // argv[0]: program name
    // argv[1] to argv[argc-1]: actual arguments
    printf("Program: %s\n", argv[0]);
    for (int i = 1; i < argc; i++)
        printf("Arg %d: %s\n", i, argv[i]);
    return 0;
}
```

### 3.12 Preprocessors in C

Processed before compilation; textual substitution.

```c
/* Macro definitions */
#define PI 3.14159265
#define MAX(a,b) ((a) > (b) ? (a) : (b))  // function-like macro

/* File inclusion */
#include <stdio.h>       // system header
#include "myfile.h"      // user header

/* Conditional compilation */
#ifdef DEBUG
    printf("Debug mode\n");
#endif

#ifndef GUARD_H
#define GUARD_H
/* header content */
#endif

#if PLATFORM == WINDOWS
    /* Windows code */
#elif PLATFORM == LINUX
    /* Linux code */
#else
    /* Other */
#endif

/* Predefined macros */
__FILE__   // current filename
__LINE__   // current line number
__DATE__   // compilation date
__TIME__   // compilation time

/* Pragma */
#pragma once        // include guard (non-standard but widely supported)
#pragma pack(1)     // pack structure without padding
```

**`#undef`:** Remove a macro definition.
**Stringification:** `#param` converts parameter to string literal.
**Token Pasting:** `A##B` concatenates tokens.

---

## 4. Object-Oriented Programming

### 4.1 OOP Concepts

**Class:** A blueprint/template defining data (attributes) and behaviour (methods).
**Object:** An instance of a class; has its own state.
**Instantiation:** Process of creating an object from a class.

### 4.2 Encapsulation

- Bundling data and methods that operate on data within a class.
- Hiding internal implementation details from outside.
- **Access Modifiers:** `public` (accessible everywhere), `private` (class only), `protected` (class and subclasses).
- **Information Hiding:** Expose only what is necessary via a public interface.

### 4.3 Inheritance

- Mechanism by which a class (subclass/derived) acquires properties of another class (superclass/base).
- **IS-A relationship:** Derived IS-A Base.
- **Types:** Single, Multiple, Multilevel, Hierarchical, Hybrid.
- **Method Overriding:** Subclass provides specific implementation of method from superclass.
- **`super`/`parent`:** Reference to superclass.

**Benefits:** Code reuse, extensibility, polymorphism support.

### 4.4 Polymorphism

- Same interface; different implementations.
- **Compile-time (Static) Polymorphism:** Function/operator overloading; resolved at compile time.
- **Runtime (Dynamic) Polymorphism:** Virtual functions; method overriding; resolved at runtime via virtual dispatch table (vtable).

### 4.5 Abstract Class

- Cannot be instantiated directly; contains at least one pure virtual function.
- Serves as interface/contract for subclasses.
- **Interface (Java):** All methods abstract; no state.
- **Abstract Class (C++/Java):** May have some implementations; partially abstract.

---

## 5. Programming in C++

### 5.1 Tokens, Identifiers, Variables and Constants

- Similar to C; additionally: `class`, `private`, `protected`, `public`, `virtual`, `template`, `namespace`, `try`, `catch`, `throw`, `new`, `delete`, `bool`, `inline`, `explicit`, `friend`, `operator`, `this`, `nullptr` (C++11).

```cpp
const int MAX = 100;          // compile-time constant
constexpr int SQ = MAX * MAX; // constant expression (C++11)
auto x = 3.14;                // type inferred (C++11)
```

### 5.2 Data Types and Operators

- All C types plus `bool`, `string` (via `<string>`), `wchar_t`, `nullptr`.
- `true`/`false` for boolean.
- **Reference type:** `int &r = x;` — alias for x; cannot be rebound.
- **Operators:** All C operators; additionally `::` (scope resolution), `new`, `delete`, `->*`, `.*`, `typeid`, `dynamic_cast`, etc.

### 5.3 Functions and Parameter Passing

```cpp
/* Default arguments */
int power(int base, int exp = 2) { ... }

/* Inline function */
inline int square(int x) { return x * x; }

/* Pass by reference */
void swap(int &a, int &b) { int t = a; a = b; b = t; }

/* Pass by const reference (efficiency without modification) */
void print(const string &s) { cout << s; }

/* Function overloading */
int add(int a, int b) { return a + b; }
double add(double a, double b) { return a + b; }
```

### 5.4 Virtual Functions

```cpp
class Shape {
public:
    virtual double area() = 0;    // pure virtual → abstract class
    virtual void draw() { cout << "Shape"; }
    virtual ~Shape() {}           // virtual destructor essential for polymorphism
};

class Circle : public Shape {
    double r;
public:
    Circle(double radius) : r(radius) {}
    double area() override { return 3.14159 * r * r; }
    void draw() override { cout << "Circle"; }
};

/* Runtime polymorphism via pointer/reference */
Shape *s = new Circle(5.0);
s->draw();    // calls Circle::draw() via vtable
delete s;
```

**vtable:** Each class with virtual functions has a virtual table (vtable) — array of function pointers. Each object has a pointer to its class's vtable (`vptr`).

**vptr overhead:** Extra pointer per object (typically 8 bytes on 64-bit).

### 5.5 Classes and Objects

```cpp
class BankAccount {
private:
    double balance;
    string owner;

public:
    /* Constructor */
    BankAccount(string name, double initial)
        : owner(name), balance(initial) {}

    /* Copy constructor */
    BankAccount(const BankAccount &other)
        : owner(other.owner), balance(other.balance) {}

    /* Destructor */
    ~BankAccount() { cout << "Account closed\n"; }

    /* Methods */
    void deposit(double amount) { balance += amount; }
    double getBalance() const { return balance; }

    /* Static member */
    static int count;
    static int getCount() { return count; }

    /* Friend function */
    friend void display(const BankAccount &acc);
};

int BankAccount::count = 0;    // static member definition
```

**`this` pointer:** Implicit pointer in non-static member functions pointing to current object.

**`static` members:** Shared across all instances; accessed via class name.

**`const` member functions:** Cannot modify object; callable on const objects.

### 5.6 Constructors and Destructors

| Constructor Type | Description |
|---|---|
| **Default** | No parameters; `ClassName()` |
| **Parameterised** | Takes arguments; initialises with values |
| **Copy** | `ClassName(const ClassName &other)`; creates copy |
| **Move (C++11)** | `ClassName(ClassName &&other)`; transfers resources |
| **Delegating (C++11)** | One constructor calls another |
| **Explicit** | `explicit ClassName(int x)` — prevents implicit conversion |

**Member Initialiser List:** `Constructor() : member1(val1), member2(val2) {}`
- Required for: `const` members, reference members, base class initialisation, efficiency (avoids default + assign).

**Destructor:** Called automatically when object goes out of scope or `delete` is called; `~ClassName()`.

**Rule of Three/Five:**
- If you define any of: destructor, copy constructor, copy assignment → define all three (Rule of Three).
- C++11: Add move constructor and move assignment (Rule of Five).
- Or: Rule of Zero — use RAII wrappers; no manual memory management.

### 5.7 Overloading

**Function Overloading:** Same name, different parameter list; resolved at compile time.

**Operator Overloading:**
```cpp
class Complex {
    double re, im;
public:
    Complex operator+(const Complex &other) const {
        return Complex(re + other.re, im + other.im);
    }
    Complex operator*(const Complex &other) const {
        return Complex(re*other.re - im*other.im,
                       re*other.im + im*other.re);
    }
    friend ostream& operator<<(ostream &os, const Complex &c) {
        os << c.re << "+" << c.im << "i";
        return os;
    }
    bool operator==(const Complex &other) const {
        return re == other.re && im == other.im;
    }
};
```

**Operators that cannot be overloaded:** `::`, `.*`, `.`, `?:`, `sizeof`, `typeid`.
**Operators that can only be overloaded as member:** `=`, `[]`, `()`, `->`.

### 5.8 Inheritance in C++

```cpp
class Animal {
protected:
    string name;
public:
    Animal(string n) : name(n) {}
    virtual void speak() { cout << "..."; }
};

/* Single inheritance */
class Dog : public Animal {
public:
    Dog(string n) : Animal(n) {}
    void speak() override { cout << "Woof"; }
};

/* Multiple inheritance */
class FlyingFish : public Fish, public Bird { ... };

/* Access specifiers in inheritance */
// public:    public → public; protected → protected
// protected: public → protected; protected → protected
// private:   public → private; protected → private
```

**Constructor/Destructor Order:**
- Construction: Base → Derived.
- Destruction: Derived → Base.

**Virtual Inheritance:** Solves Diamond Problem in multiple inheritance.
```cpp
class B : virtual public A { ... };
class C : virtual public A { ... };
class D : public B, public C { ... }; // Only one A subobject
```

### 5.9 Templates

**Function Template:**
```cpp
template <typename T>
T max(T a, T b) { return a > b ? a : b; }

// Explicit instantiation
max<int>(3, 5);
max<double>(3.1, 5.2);
// Implicit (type deduced): max(3, 5);
```

**Class Template:**
```cpp
template <typename T, int N>
class Array {
    T data[N];
public:
    T& operator[](int i) { return data[i]; }
    int size() const { return N; }
};

Array<int, 10> arr;
```

**Template Specialisation:** Provide specific implementation for a particular type.
```cpp
template<>
class Array<bool, 10> { /* bit-level implementation */ };
```

**STL (Standard Template Library):** Containers (vector, list, map, set), algorithms (sort, find, for_each), iterators.

### 5.10 Exception Handling

```cpp
try {
    if (denom == 0) throw std::runtime_error("Division by zero");
    result = num / denom;
    throw 42;              // throw any type
}
catch (const std::runtime_error &e) {
    cerr << "Runtime error: " << e.what();
}
catch (int code) {
    cerr << "Error code: " << code;
}
catch (...) {             // catch all
    cerr << "Unknown exception";
}
// finally equivalent: RAII / destructors called automatically
```

**Exception hierarchy:**
```
std::exception
    std::logic_error: invalid_argument, out_of_range, domain_error
    std::runtime_error: overflow_error, underflow_error, range_error
    std::bad_alloc
    std::bad_cast
```

**`noexcept`:** C++11 specifier; function guarantees no exceptions thrown.

**Stack Unwinding:** When exception thrown, destructors called for all local objects as stack is unwound.

### 5.11 Streams and Files

```cpp
#include <iostream>
#include <fstream>
#include <sstream>

// Console I/O
cin >> x;
cout << "Value: " << x << endl;
cerr << "Error\n";

// File I/O
ifstream fin("in.txt");
ofstream fout("out.txt");
fstream both("data.txt", ios::in | ios::out);

fin >> x;
fout << x;
fin.getline(buf, 100);
getline(fin, str);        // read entire line into string

// File seek
fin.seekg(100, ios::beg); // seek get pointer
fout.seekp(-10, ios::end);// seek put pointer
fin.tellg();              // current get position
```

**Stream states:**
- `good()`, `eof()`, `fail()`, `bad()`
- `ios::goodbit`, `ios::eofbit`, `ios::failbit`, `ios::badbit`

### 5.12 Multifile Programs

```cpp
// header.h
#ifndef HEADER_H
#define HEADER_H
class MyClass {
public:
    void method();
    static int count;
};
extern int globalVar;      // declaration
#endif

// header.cpp
#include "header.h"
int MyClass::count = 0;    // static member definition
int globalVar = 10;        // definition

// main.cpp
#include "header.h"
int main() { MyClass obj; obj.method(); }
```

**Compilation:** `g++ -c header.cpp -o header.o; g++ -c main.cpp -o main.o; g++ header.o main.o -o program`

**Namespaces:**
```cpp
namespace MyLib {
    int add(int a, int b) { return a + b; }
}
MyLib::add(3, 4);
using namespace MyLib;  // brings all into scope (use carefully)
using MyLib::add;       // brings only add
```

---

## 6. Web Programming

### 6.1 HTML and DHTML

**HTML (HyperText Markup Language):** Markup language for structuring web content.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Page Title</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Heading 1</h1>
    <p>Paragraph with <a href="url">link</a> and <img src="img.jpg" alt="desc"></p>
    <ul><li>Item</li></ul>
    <ol><li>Ordered</li></ol>
    <table>
        <tr><th>Header</th></tr>
        <tr><td>Data</td></tr>
    </table>
    <form action="submit.php" method="post">
        <input type="text" name="username">
        <input type="submit" value="Submit">
    </form>
    <div class="container"><span id="element">text</span></div>
</body>
</html>
```

**DHTML (Dynamic HTML):** Combination of HTML + CSS + JavaScript + DOM to create dynamic, interactive pages.
- **DOM (Document Object Model):** Tree structure representing HTML; JavaScript can modify it.
- Changes can be made without page reload.

### 6.2 XML

**XML (eXtensible Markup Language):** Self-describing, hierarchical data format; user-defined tags.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<students>
    <student id="101">
        <name>Alice</name>
        <grade>A</grade>
    </student>
    <student id="102">
        <name>Bob</name>
        <grade>B</grade>
    </student>
</students>
```

**XML vs HTML:**
- XML: data-centric; user-defined tags; strict well-formedness rules.
- HTML: presentation-centric; predefined tags; more lenient.

**DTD (Document Type Definition):** Defines structure rules for XML document.
**XML Schema (XSD):** More powerful alternative to DTD; uses XML syntax.
**XPath:** Navigate XML document tree.
**XSLT:** Transform XML documents into other formats.
**SAX vs DOM parsing:** SAX = event-driven (streaming); DOM = loads entire tree into memory.

### 6.3 Scripting

**Client-side:** JavaScript (runs in browser).
**Server-side:** PHP, Python, Node.js, Ruby.

**JavaScript Basics:**
```javascript
// Variables (ES6+)
let x = 10;
const PI = 3.14;
var oldStyle = "avoid";

// Functions
function greet(name) { return `Hello, ${name}`; }
const add = (a, b) => a + b;  // arrow function

// DOM manipulation
document.getElementById("id").innerHTML = "New content";
document.querySelector(".class").style.color = "red";

// Event handling
document.getElementById("btn").addEventListener("click", function() {
    alert("Clicked!");
});

// AJAX (XMLHttpRequest / fetch)
fetch("api/data")
    .then(response => response.json())
    .then(data => console.log(data));
```

### 6.4 Java (for Web)

- Object-oriented, platform-independent (Write Once Run Anywhere via JVM).
- Strongly typed; garbage collected; robust.

**Java Program Structure:**
```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

**Key differences from C++:**
- No pointers (references only); no multiple inheritance of classes (use interfaces); no operator overloading; automatic garbage collection; all code in classes.

### 6.5 Servlets

- Java programs running on a web server; process HTTP requests and generate responses.
- **Lifecycle:** `init()` → `service()` [doGet() / doPost()] → `destroy()`.

```java
import javax.servlet.*;
import javax.servlet.http.*;
public class HelloServlet extends HttpServlet {
    protected void doGet(HttpServletRequest req, HttpServletResponse res)
            throws ServletException, IOException {
        res.setContentType("text/html");
        PrintWriter out = res.getWriter();
        out.println("<html><body><h1>Hello from Servlet!</h1></body></html>");
    }
}
```

**Servlet Container (Web Container):** Tomcat, Jetty — manage servlet lifecycle, HTTP parsing, threading.

### 6.6 Applets

- Java programs that run inside a web browser (via JVM plugin).
- **Lifecycle:** `init()` → `start()` → `paint()` → `stop()` → `destroy()`.
- **Status:** Deprecated; modern browsers dropped Java plugin support.
- Superseded by JavaScript, HTML5, WebAssembly.

```java
import java.applet.Applet;
import java.awt.Graphics;
public class HelloApplet extends Applet {
    public void paint(Graphics g) {
        g.drawString("Hello, Applet!", 20, 20);
    }
}
```

---

## 7. Computer Graphics

### 7.1 Video-Display Devices

**CRT (Cathode Ray Tube):**
- Electron beam steered by deflection plates/coils to illuminate phosphor screen.
- **Raster Scan:** Beam sweeps left-to-right, top-to-bottom; entire screen refreshed periodically (60–85 Hz). Stores pixel values in frame buffer.
- **Random Scan (Vector/Calligraphic):** Beam directed only to portions of screen where drawing is needed; draws lines directly. No frame buffer for full screen.

**Flat Panel Displays:**
- LCD (Liquid Crystal Display): Backlight + liquid crystals + polarisers.
- OLED (Organic LED): Self-emitting; better contrast; flexible.
- Plasma: Gas discharge; each pixel a tiny fluorescent lamp.

**Refresh Rate:** Number of times screen redrawn per second (Hz). Minimum ~60 Hz to avoid flicker.

**Interlacing:** Alternate scans draw odd and even lines to increase apparent refresh rate.

**Resolution:** `H_pixels × V_pixels`. Common: 1920×1080 (FHD), 3840×2160 (4K UHD).

**Aspect Ratio:** Ratio of width to height (e.g., 16:9, 4:3).

**Frame Buffer (Bitmap):** Memory area storing colour value of each pixel.
- Memory required: `H × V × bits_per_pixel` bits.
- 1920×1080 × 24 bits = ≈ 6.2 MB per frame.

### 7.2 Raster-Scan vs Random-Scan Systems

| Aspect | Raster Scan | Random Scan |
|---|---|---|
| Drawing | Entire screen scanned row by row | Only defined objects drawn |
| Picture Storage | Frame buffer (full screen pixels) | Display list (drawing commands) |
| Picture Quality | Smooth shading; image textures | Sharp lines; no realistic shading |
| Resolution | Fixed by grid | Arbitrary (smooth curves) |
| Cost | Lower | Higher |
| Use | TVs, monitors, most modern displays | Oscilloscopes, old plotters, CAD |

### 7.3 Input Devices

| Device | Type | Input |
|---|---|---|
| Keyboard | Alphanumeric | Characters, commands |
| Mouse | Relative position | 2D coordinates, clicks |
| Trackball | Relative position | 2D, rotational |
| Light Pen | Absolute position | Point on screen |
| Joystick | Direction + magnitude | 2D/3D direction |
| Data Glove | 3D gesture | Hand position, orientation |
| Digitizer/Tablet | Absolute position | 2D coordinates |
| Touch Screen | Absolute position | Direct interaction |
| Scanner | Image input | Digitise hardcopy |

### 7.4 Points and Lines

**Point:** Defined by coordinates `(x, y)` in 2D or `(x, y, z)` in 3D; rendered as a pixel in raster graphics.

**Line:** Defined by two endpoints `P1(x1, y1)` and `P2(x2, y2)`.
- **Slope:** `m = (y2 - y1) / (x2 - x1)`
- **Slope-intercept:** `y = mx + b` where `b = y1 - m·x1`.

---

## 8. Line Drawing Algorithms

### 8.1 DDA (Digital Differential Analyser)

```
dx = x2 - x1; dy = y2 - y1
steps = max(|dx|, |dy|)
x_inc = dx / steps; y_inc = dy / steps
x = x1; y = y1
for k = 0 to steps:
    plot(round(x), round(y))
    x = x + x_inc; y = y + y_inc
```

- Uses floating-point arithmetic; slow due to round() and division.
- `steps` ensures no gaps and no redundant points.

### 8.2 Bresenham's Line Algorithm

- Integer arithmetic only; faster than DDA.
- Uses a **decision parameter** to choose next pixel.

**For line with slope `0 ≤ m ≤ 1` (|dx| ≥ |dy|):**
```
dx = x2 - x1; dy = y2 - y1
p₀ = 2·dy - dx         (initial decision parameter)

for each step from x1 to x2:
    plot(x, y)
    if p < 0:
        x = x + 1; p = p + 2·dy
    else:
        x = x + 1; y = y + 1; p = p + 2·dy - 2·dx
```

**Decision parameter derivation:**
- Ideal y at step k+1: `y = m(xₖ + 1) + b`
- Distances to candidate pixels: `d_lower = y - yₖ`, `d_upper = yₖ + 1 - y`
- `pₖ = 2dy(xₖ + 1) - 2dx·yₖ - 2dx·b - dx` (integer form)
- `pₖ₊₁ = pₖ + 2dy - 2dx(yₖ₊₁ - yₖ)`

**Advantages over DDA:** Only integer additions and comparisons; no floating point; faster.

---

## 9. Circle and Ellipse Drawing

### 9.1 Mid-Point Circle Algorithm

Uses **8-way symmetry** of circle: compute one octant, reflect for other 7.

**Given:** Circle centred at origin, radius r.
- Point `(x, y)` → also plot at `(x,-y)`, `(-x,y)`, `(-x,-y)`, `(y,x)`, `(y,-x)`, `(-y,x)`, `(-y,-x)`.

**Algorithm:**
```
x = 0; y = r
p = 1 - r          (initial decision parameter)
plot_circle_points(cx, cy, x, y)  // plot 8 symmetric points

while x < y:
    x = x + 1
    if p < 0:
        p = p + 2x + 1
    else:
        y = y - 1
        p = p + 2x - 2y + 1
    plot_circle_points(cx, cy, x, y)
```

**Decision parameter derivation:**
- Circle equation: `f(x, y) = x² + y² - r²`
- Mid-point at `(xₖ + 1, yₖ - 0.5)`.
- `pₖ = f(xₖ + 1, yₖ - 0.5) = (xₖ+1)² + (yₖ-0.5)² - r²`
- If `pₖ < 0`: mid-point inside circle → choose `yₖ`; `pₖ₊₁ = pₖ + 2xₖ₊₁ + 1`
- If `pₖ ≥ 0`: mid-point outside → choose `yₖ - 1`; `pₖ₊₁ = pₖ + 2xₖ₊₁ - 2yₖ₊₁ + 1`
- Initial: `p₀ = 1 - r`

### 9.2 Mid-Point Ellipse Algorithm

**Ellipse equation:** `(x/a)² + (y/b)² = 1` or `b²x² + a²y² = a²b²`

**Two regions based on slope magnitude:**
- **Region 1:** `|slope| < 1` → x is driving direction.
- **Region 2:** `|slope| > 1` → y is driving direction.
- Boundary: when `2b²x = 2a²y`.

**Region 1 (starting at top `(0, b)`):**
```
p1₀ = b² - a²b + a²/4    (≈ b² - a²b + a²/4 using integers)
while 2b²x < 2a²y:
    x++
    if p1 < 0: p1 = p1 + 2b²x + b²
    else: y--; p1 = p1 + 2b²x - 2a²y + b²
    plot (use 4-way symmetry)
```

**Region 2 (starting from end of Region 1 to `(a, 0)`):**
```
p2 = b²(x+0.5)² + a²(y-1)² - a²b²    (initial at boundary)
while y > 0:
    y--
    if p2 > 0: p2 = p2 - 2a²y + a²
    else: x++; p2 = p2 + 2b²x - 2a²y + a²
    plot (use 4-way symmetry)
```

**4-way symmetry for ellipse:** `(x,y)`, `(-x,y)`, `(x,-y)`, `(-x,-y)`.

---

## 10. Polygon Fill Algorithms

### 10.1 Scan-Line Polygon Fill

- Fill interior pixels of polygon by processing one horizontal scan line at a time.

**Algorithm:**
1. **Find all intersections** of scan line y with polygon edges.
2. **Sort** intersections by x-coordinate.
3. **Fill** pixels between pairs of intersections (parity rule: enter on odd intersection, exit on even).
4. Repeat for all scan lines from `y_min` to `y_max`.

**Edge Table (ET):**
- Non-horizontal edges stored sorted by their minimum y.
- Each edge entry: `{y_max, x_min, 1/m}` (reciprocal of slope for x increment).

**Active Edge Table (AET):**
- Edges currently intersected by scan line.
- Updated at each scan line: remove edges where `y = y_max`; add from ET; sort by x; update x values `x_new = x_old + 1/m`.

**Special Cases:**
- Vertex at scan line: Count once if it's a local extremum; count twice (or zero) otherwise.
- Horizontal edges: Usually ignored (handled by vertices).

### 10.2 Boundary-Fill Algorithm

- Start from interior seed point; fill until boundary colour encountered.

**4-connected version:**
```python
def boundary_fill_4(x, y, fill_color, boundary_color):
    if get_pixel(x,y) != boundary_color and get_pixel(x,y) != fill_color:
        set_pixel(x, y, fill_color)
        boundary_fill_4(x+1, y, fill_color, boundary_color)
        boundary_fill_4(x-1, y, fill_color, boundary_color)
        boundary_fill_4(x, y+1, fill_color, boundary_color)
        boundary_fill_4(x, y-1, fill_color, boundary_color)
```

**8-connected:** Also fills diagonal neighbours.
- More robust but may leak through thin diagonal boundaries.

**Iterative version:** Use explicit stack to avoid recursion limit.

### 10.3 Flood-Fill Algorithm

- Like boundary-fill but replaces a specific interior colour (not defined by boundary).

```python
def flood_fill(x, y, old_color, new_color):
    if get_pixel(x, y) == old_color:
        set_pixel(x, y, new_color)
        flood_fill(x+1, y, old_color, new_color)
        flood_fill(x-1, y, old_color, new_color)
        flood_fill(x, y+1, old_color, new_color)
        flood_fill(x, y-1, old_color, new_color)
```

---

## 11. 2D Geometric Transforms and Viewing

### 11.1 Basic 2D Transformations

All 2D transformations represented as matrix operations on column vectors.

**Translation:**
```
x' = x + tx
y' = y + ty
```
Matrix (using homogeneous coordinates):
```
[x']   [1  0  tx] [x]
[y'] = [0  1  ty] [y]
[1 ]   [0  0   1] [1]
```

**Scaling (about origin):**
```
x' = x · sx
y' = y · sy
```
Matrix:
```
[x']   [sx  0  0] [x]
[y'] = [ 0  sy 0] [y]
[1 ]   [ 0   0 1] [1]
```
- `sx = sy`: Uniform scaling. `sx ≠ sy`: Differential scaling.
- Scaling about a fixed point (px, py): Translate to origin → Scale → Translate back.

**Rotation (about origin by angle θ, counter-clockwise):**
```
x' = x·cosθ - y·sinθ
y' = x·sinθ + y·cosθ
```
Matrix:
```
[x']   [cosθ  -sinθ  0] [x]
[y'] = [sinθ   cosθ  0] [y]
[1 ]   [ 0      0    1] [1]
```
- Rotation about arbitrary point (px, py): T(px,py) → R(θ) → T(-px,-py).

**Reflection:**

| Reflection | Matrix |
|---|---|
| About x-axis | `[1,0,0; 0,-1,0; 0,0,1]` |
| About y-axis | `[-1,0,0; 0,1,0; 0,0,1]` |
| About y = x | `[0,1,0; 1,0,0; 0,0,1]` |
| About y = -x | `[0,-1,0; -1,0,0; 0,0,1]` |
| About origin | `[-1,0,0; 0,-1,0; 0,0,1]` |

**Shear:**

X-direction shear:
```
x' = x + shx·y
y' = y
Matrix: [1, shx, 0; 0, 1, 0; 0, 0, 1]
```

Y-direction shear:
```
x' = x
y' = shy·x + y
Matrix: [1, 0, 0; shy, 1, 0; 0, 0, 1]
```

### 11.2 Homogeneous Coordinates

- Represent 2D point `(x, y)` as 3D `(x·h, y·h, h)` for any `h ≠ 0`.
- Standard: use `h = 1` → `(x, y, 1)`.
- **Purpose:** Represent translation as matrix multiplication (otherwise impossible with 2×2 matrix); unify all affine transformations.
- To convert back: `(X, Y, h) → (X/h, Y/h)`.

### 11.3 Composite Transforms

- Apply multiple transformations by multiplying their matrices (right to left order).
- `P' = Mₙ · Mₙ₋₁ · ... · M₁ · P`
- **Example — Rotate about arbitrary point (px, py):**
  `M = T(px, py) · R(θ) · T(-px, -py)`

**Order matters:** Matrix multiplication is not commutative.

**Scale about fixed point:**
`M = T(px, py) · S(sx, sy) · T(-px, -py)`

**Rotation then translation ≠ Translation then rotation** (in general).

### 11.4 Transformations Between Coordinate Systems

**World Coordinate System (WCS) → Viewing/Screen Coordinate System:**
- Define viewing coordinate system by origin `(x0, y0)` and rotation angle θ.
- `T_WC = R(-θ) · T(-x0, -y0)`
  1. Translate WCS origin to align with WCS origin.
  2. Rotate to align viewing axes with world axes.

### 11.5 2D Viewing Pipeline

```
World Coordinates
    ↓ [Viewing Transform]
Viewing Coordinates
    ↓ [Window selection: clip]
Clipped Scene
    ↓ [Viewport Transform]
Normalised Device Coordinates
    ↓ [Device Transform]
Device Coordinates (Screen)
```

**Window:** Rectangular region in world/viewing space to be displayed.
**Viewport:** Rectangular region on screen/device where window is mapped.

### 11.6 Window-to-Viewport Transformation

```
Window: (xwmin, xwmax, ywmin, ywmax)
Viewport: (xvmin, xvmax, yvmin, yvmax)
```

**Mapping equations:**
```
sx = (xvmax - xvmin) / (xwmax - xwmin)
sy = (yvmax - yvmin) / (ywmax - ywmin)

xv = xvmin + (xw - xwmin) · sx
yv = yvmin + (yw - ywmin) · sy
```

**As composite transformation:**
`M = T(xvmin, yvmin) · S(sx, sy) · T(-xwmin, -ywmin)`

### 11.7 Line Clipping Algorithms

**Cohen-Sutherland Algorithm:**
- Assign 4-bit region code (outcode) to each endpoint: `[Top | Bottom | Right | Left]`
  - Bit set if outside that boundary.
  - Inside region: code = `0000`.

**Region Codes:**
```
1001 | 1000 | 1010
-----+------+-----
0001 | 0000 | 0010
-----+------+-----
0101 | 0100 | 0110
```

**Algorithm:**
```
while True:
    if both inside (code1 | code2 == 0000): accept; break
    if trivially outside (code1 & code2 ≠ 0): reject; break
    else:
        Pick endpoint outside (non-zero code)
        Find intersection with boundary corresponding to set bit
        Replace endpoint with intersection
```

**Intersection formulas (window boundary):**
- Left `(x = xwmin)`: `y = y1 + m·(xwmin - x1)`, `x = xwmin`
- Right `(x = xwmax)`: `y = y1 + m·(xwmax - x1)`, `x = xwmax`
- Bottom `(y = ywmin)`: `x = x1 + (ywmin - y1)/m`, `y = ywmin`
- Top `(y = ywmax)`: `x = x1 + (ywmax - y1)/m`, `y = ywmax`

where `m = (y2 - y1) / (x2 - x1)`.

**Liang-Barsky Algorithm:**
- Parametric line: `P(t) = P1 + t·(P2 - P1)`, `0 ≤ t ≤ 1`.
- Line: `x = x1 + t·Δx`, `y = y1 + t·Δy` where `Δx = x2-x1`, `Δy = y2-y1`.
- Clip conditions:
  - Left: `-Δx·t ≤ x1 - xwmin` → `p1 = -Δx`, `q1 = x1 - xwmin`
  - Right: `Δx·t ≤ xwmax - x1` → `p2 = Δx`, `q2 = xwmax - x1`
  - Bottom: `-Δy·t ≤ y1 - ywmin` → `p3 = -Δy`, `q3 = y1 - ywmin`
  - Top: `Δy·t ≤ ywmax - y1` → `p4 = Δy`, `q4 = ywmax - y1`
- For each i:
  - If `pᵢ = 0` and `qᵢ < 0`: line parallel and outside → reject.
  - If `pᵢ < 0`: `t_enter = max(t_enter, qᵢ/pᵢ)` (entering).
  - If `pᵢ > 0`: `t_exit = min(t_exit, qᵢ/pᵢ)` (exiting).
- If `t_enter > t_exit`: reject. Else: `P1' = P1 + t_enter·ΔP`, `P2' = P1 + t_exit·ΔP`.

**Nicholl-Lee-Nicholl (NLN):** Faster for lines that are clearly outside or inside; reduces intersection computations.

**Polygon Clipping:**

**Sutherland-Hodgman Algorithm:**
- Clip polygon against each boundary (left, right, bottom, top) successively.
- For each boundary, process all edges; add vertices to output list using 4 cases:
  - Both inside: add current vertex.
  - Inside to outside: add intersection.
  - Both outside: add nothing.
  - Outside to inside: add intersection and current vertex.

**Weiler-Atherton:** Handles concave polygons and polygons with holes.

---

## 12. 3D Object Representation

### 12.1 Polygon Surfaces (Polygon Mesh)

- Object surface approximated by a set of polygons (usually triangles or quads).
- **Vertex List:** List of 3D coordinates.
- **Edge List:** Pairs of vertex indices.
- **Polygon (Face) List:** Ordered lists of vertex/edge indices forming each polygon.
- **Surface normal:** `N = (P2 - P1) × (P3 - P1)` (cross product of two edge vectors).
  - `N = (a, b, c)`; `|N| = √(a² + b² + c²)`; unit normal `n̂ = N / |N|`.

### 12.2 Quadric Surfaces

Defined by second-degree polynomial equation: `Ax² + By² + Cz² + Dxy + Exz + Fyz + Gx + Hy + Iz + J = 0`

| Surface | Equation |
|---|---|
| Sphere | `x² + y² + z² = r²` |
| Ellipsoid | `(x/a)² + (y/b)² + (z/c)² = 1` |
| Paraboloid | `z = ax² + by²` (elliptic); `z = ax² - by²` (hyperbolic) |
| Cone | `x²/a² + y²/b² = z²/c²` |
| Cylinder | `x² + y² = r²` |
| Hyperboloid | `x²/a² + y²/b² - z²/c² = 1` (one sheet) |

### 12.3 Spline Representation

- **Spline:** Piecewise polynomial curve; smooth joins between segments.
- **Knot:** Joining point between segments.
- **Smoothness Conditions:** C⁰ (positional), C¹ (tangent), C² (curvature) continuity.

**Parametric Form:** `P(t) = (x(t), y(t), z(t))` for `t ∈ [0, 1]`.

**Cubic Hermite Spline:** Defined by two endpoints and two tangent vectors.
```
P(t) = h₁(t)·P1 + h₂(t)·P2 + h₃(t)·T1 + h₄(t)·T2
where Hermite basis:
h₁(t) = 2t³ - 3t² + 1
h₂(t) = -2t³ + 3t²
h₃(t) = t³ - 2t² + t
h₄(t) = t³ - t²
```

### 12.4 Bezier Curves

**Bernstein Polynomials (basis functions):**
```
Bᵢ,ₙ(t) = C(n,i) · tⁱ · (1-t)^(n-i)
where C(n,i) = n! / (i! · (n-i)!)
```

**Bezier Curve of degree n (n+1 control points P₀, P₁, ..., Pₙ):**
```
P(t) = Σᵢ₌₀ⁿ Bᵢ,ₙ(t) · Pᵢ,    t ∈ [0, 1]
```

**Matrix form (cubic, n=3):**
```
P(t) = [t³ t² t 1] · M_B · [P0 P1 P2 P3]ᵀ

where Bezier matrix M_B:
[-1   3  -3  1]
[ 3  -6   3  0]
[-3   3   0  0]
[ 1   0   0  0]
```

**Properties of Bezier Curves:**
- Interpolates first (P₀) and last (Pₙ) control points.
- Lies within the convex hull of control points.
- Tangent at P₀: `P'(0) = n(P₁ - P₀)`; tangent at Pₙ: `P'(1) = n(Pₙ - Pₙ₋₁)`.
- Affine invariance: Transform curve by transforming control points.
- Symmetric: Curve unchanged by reversing control point order.
- Variation diminishing: Curve does not oscillate more than its control polygon.

**de Casteljau Algorithm:** Recursive computation of Bezier curve point at parameter t.
```
P₀⁰=P₀, P₁⁰=P₁, ..., Pₙ⁰=Pₙ
For r = 1 to n:
    For i = 0 to n-r:
        Pᵢʳ = (1-t)·Pᵢʳ⁻¹ + t·Pᵢ₊₁ʳ⁻¹
Result: P₀ⁿ = P(t)
```

**Joining Bezier Curves (C¹ continuity):** Last three points of first curve and first three of second must be collinear: `Pₙ₋₁, Pₙ = Q₀, Q₁` must be collinear with `|PₙPₙ₋₁| = |Q₀Q₁|`.

### 12.5 B-Spline Curves

More flexible than Bezier; local control; can represent wider class of shapes.

**B-Spline Curve:**
```
P(t) = Σᵢ₌₀ⁿ Nᵢ,ₖ(t) · Pᵢ
```
where `Nᵢ,ₖ(t)` = B-spline basis functions of order k; defined recursively (Cox-de Boor):
```
Nᵢ,₁(t) = 1 if tᵢ ≤ t < tᵢ₊₁, else 0
Nᵢ,ₖ(t) = [(t - tᵢ)/(tᵢ₊ₖ₋₁ - tᵢ)] · Nᵢ,ₖ₋₁(t)
         + [(tᵢ₊ₖ - t)/(tᵢ₊ₖ - tᵢ₊₁)] · Nᵢ₊₁,ₖ₋₁(t)
```
where `t₀, t₁, ..., tₘ` is the **knot vector**.

**Properties of B-Splines:**
- Local control: Moving one control point affects at most k spans.
- Convex hull property: Curve lies within convex hull of local control points.
- Partition of unity: `Σ Nᵢ,ₖ(t) = 1` for all t.
- Does NOT necessarily interpolate control points.

**NURBS (Non-Uniform Rational B-Splines):**
```
P(t) = Σ wᵢ · Nᵢ,ₖ(t) · Pᵢ / Σ wᵢ · Nᵢ,ₖ(t)
```
- Weights `wᵢ` allow exact representation of conics (circles, ellipses).
- Standard in CAD (AutoCAD, CATIA, STEP format).

### 12.6 Bezier and B-Spline Surfaces

**Bezier Surface (m×n patch):**
```
P(s, t) = Σᵢ₌₀ᵐ Σⱼ₌₀ⁿ Bᵢ,ₘ(s) · Bⱼ,ₙ(t) · Pᵢⱼ
```
where `Pᵢⱼ` = control point mesh.

**B-Spline Surface:**
```
P(s, t) = Σᵢ Σⱼ Nᵢ,ₖ(s) · Nⱼ,ₗ(t) · Pᵢⱼ
```

**Tensor Product:** Surface is product of two independent 1D splines.

---

## 13. Illumination Models

### 13.1 Basic Illumination Models

**Ambient Light:** Non-directional background illumination.
```
I_ambient = Iₐ · kₐ
```
where `Iₐ` = ambient light intensity, `kₐ` = ambient reflection coefficient (0 to 1).

**Diffuse Reflection (Lambertian):** Light reflected equally in all directions.
```
I_diffuse = Iₗ · kd · cos(θ) = Iₗ · kd · (N̂ · L̂)
```
where `N̂` = surface normal, `L̂` = light direction unit vector, `kd` = diffuse coefficient, `θ` = angle between N and L.

**Specular Reflection (Phong):** Mirror-like highlights.
```
I_specular = Iₗ · ks · cos^n(α) = Iₗ · ks · (R̂ · V̂)^n
```
where `R̂` = reflection direction, `V̂` = viewer direction, `n` = shininess (Phong exponent), `ks` = specular coefficient.

**Reflection vector:**
```
R̂ = 2(N̂ · L̂)·N̂ - L̂
```

**Phong Illumination Model (Complete):**
```
I = Iₐ·kₐ + Iₗ·[kd·(N̂·L̂) + ks·(R̂·V̂)^n]
```

**Blinn-Phong Model:** Replaces R·V with N·H where H = halfway vector.
```
H̃ = (L̂ + V̂) / |L̂ + V̂|    (halfway vector)
I_specular = Iₗ · ks · (N̂ · H̃)^n
```
- Faster computation; physically more accurate for rough surfaces.

**Attenuation with distance:**
```
f_att = 1 / (c₁ + c₂·d + c₃·d²)
```
where d = distance from light source.

**Multiple Light Sources:**
```
I = Iₐ·kₐ + Σⱼ f_att_j · Iₗⱼ · [kd·(N̂·L̂ⱼ) + ks·(R̂ⱼ·V̂)^n]
```

### 13.2 Polygon Rendering Methods

**Flat (Constant) Shading:**
- Compute one colour per polygon (using normal of polygon).
- Fast but shows facets (Mach band effect).

**Gouraud Shading:**
- Compute colour at each vertex; interpolate linearly across polygon.
- **Vertex normal:** Average of normals of adjacent polygon faces.
- Eliminates intensity discontinuities between faces; smooth appearance.
- Cannot capture highlights within polygon that don't hit vertices.

**Phong Shading:**
- Interpolate surface normals across polygon; compute illumination at each pixel.
- Best quality; captures specular highlights accurately.
- Most expensive (illumination computed per pixel).

**Comparison:**
| Method | Quality | Speed | Highlights |
|---|---|---|---|
| Flat | Lowest | Fastest | Faceted |
| Gouraud | Medium | Medium | May miss |
| Phong | Highest | Slowest | Accurate |

**Ray Tracing:** Cast ray from eye through each pixel; compute intersections with objects; recursively trace reflected/refracted rays. Physically accurate; extremely slow.

**Radiosity:** Models diffuse inter-reflection; global illumination for perfectly diffuse scenes.

---

## 14. 3D Geometric Transformations and Viewing

### 14.1 3D Transformations (Homogeneous Coordinates)

3D point represented as `(x, y, z, 1)` in homogeneous form.

**3D Translation:**
```
[x']   [1 0 0 tx] [x]
[y'] = [0 1 0 ty] [y]
[z']   [0 0 1 tz] [z]
[1 ]   [0 0 0  1] [1]
```

**3D Scaling:**
```
[x']   [sx  0   0  0] [x]
[y'] = [ 0  sy  0  0] [y]
[z']   [ 0   0  sz 0] [z]
[1 ]   [ 0   0   0 1] [1]
```

**3D Rotation:**

About z-axis (same as 2D rotation):
```
[cosθ  -sinθ  0  0]
[sinθ   cosθ  0  0]
[  0      0   1  0]
[  0      0   0  1]
```

About x-axis:
```
[1    0      0   0]
[0  cosθ  -sinθ  0]
[0  sinθ   cosθ  0]
[0    0      0   1]
```

About y-axis:
```
[ cosθ  0  sinθ  0]
[   0   1    0   0]
[-sinθ  0  cosθ  0]
[   0   0    0   1]
```

**Rotation about arbitrary axis:**
1. Translate axis to pass through origin.
2. Rotate axis to align with coordinate axis.
3. Apply rotation by θ.
4. Inverse rotations to restore axis orientation.
5. Translate back.

**Euler Angles:** Three rotations about principal axes (Rx, Ry, Rz in some order). Order-dependent.

**Gimbal Lock:** Two rotation axes align when middle angle = ±90°; lose one degree of freedom.

**Quaternions (for rotation):** `q = w + xi + yj + zk` where `w = cos(θ/2)`, `(x,y,z) = sin(θ/2)·axis`.
- Avoids gimbal lock; smooth interpolation (SLERP).
- `SLERP(q₁, q₂, t) = q₁ · (q₁⁻¹ · q₂)^t`

### 14.2 3D Viewing Pipeline

```
World Coordinates
    ↓ [Modelling Transform]
    ↓ [Viewing Transform (Camera/Eye setup)]
View Coordinates (Camera Space)
    ↓ [Projection Transform]
Clip Coordinates
    ↓ [Clipping]
    ↓ [Perspective Division: x/w, y/w, z/w]
Normalised Device Coordinates (NDC)
    ↓ [Viewport Transform]
Window / Screen Coordinates
    ↓ [Scan Conversion / Rasterisation]
Fragment Processing
    ↓ [Display]
```

### 14.3 Viewing Coordinate System

Define by:
- **VRP (View Reference Point):** Origin of view coordinate system in world space.
- **VPN (View Plane Normal):** Normal to the view plane; defines n-axis of view system.
- **VUP (View Up vector):** Approximately upward direction; used to compute v-axis.

**Compute view axes:**
```
n = VPN / |VPN|             (normalise)
u = VUP × n / |VUP × n|    (cross product; right axis)
v = n × u                   (up axis in view system)
```

**View transform matrix:**
```
Mview = [ux  uy  uz  -u·VRP]
        [vx  vy  vz  -v·VRP]
        [nx  ny  nz  -n·VRP]
        [ 0   0   0      1 ]
```
This rotates world coordinate system to align with view system, then translates.

### 14.4 Projection Transforms

**Parallel (Orthographic) Projection:**
- Drop z coordinate; no perspective.
- Object size independent of distance.
- `x' = x`, `y' = y`, `z' = 0` (project onto xy-plane along z-axis).

**Oblique Projection:**
- Parallel projectors not perpendicular to view plane.
- **Cabinet:** projectors at 45°; depth foreshortened by half.
- **Cavalier:** projectors at 45°; no foreshortening.

**Perspective Projection:**
- Objects farther away appear smaller; converging projectors.
- **Centre of Projection (COP):** Eye point.
- **View Plane:** Display surface.

**Simple Perspective (COP at origin, view plane at z = d):**
```
x' = x · d / z
y' = y · d / z
```

**Homogeneous perspective matrix:**
```
[1 0 0  0]
[0 1 0  0]
[0 0 1  0]
[0 0 1/d 0]
```
After applying: `(x, y, z, z/d)` → divide by w=z/d → `(xd/z, yd/z, d)`.

**Vanishing Points:**
- **One-point perspective:** Lines parallel to z-axis converge to one vanishing point.
- **Two-point perspective:** Parallel to x and z axes each have vanishing points.
- **Three-point perspective:** All three axes have vanishing points.

### 14.5 3D Clipping

**View Volume:** Region visible to camera.
- **Orthographic:** Rectangular box (parallelepiped).
- **Perspective:** Frustum (truncated pyramid) defined by:
  - Near clip plane (z = near)
  - Far clip plane (z = far)
  - Left, right, top, bottom planes.

**Cohen-Sutherland for 3D Lines:** Extend to 6-bit outcode (left, right, bottom, top, near, far).

**Cyrus-Beck (Liang-Barsky) for 3D:** Parametric clipping against convex volume; generalises to 3D.

**Polygon Clipping (3D):** Apply Sutherland-Hodgman against each of 6 clip planes.

**Back-Face Culling:** Remove polygons facing away from viewer.
- Polygon is back-facing if `N̂ · V̂ < 0` (normal points away from viewer).
- `N̂ · V̂ = cos(θ)`; if `θ > 90°` → back face.
- Eliminates ≈ 50% of polygons before further rendering.

**Hidden Surface Removal:**
- **Painter's Algorithm:** Sort polygons by depth; render far to near (back to front). Problem: cycles.
- **Z-buffer (Depth Buffer):** Per-pixel depth test; keep pixel with smallest z. O(1) per pixel. Most common hardware method.
  - `if z_new < z_buffer[x][y]: z_buffer[x][y] = z_new; color_buffer[x][y] = new_color`
- **BSP Tree (Binary Space Partitioning):** Hierarchical space subdivision; determines front-to-back order efficiently for static scenes.
- **Ray Casting:** Cast ray per pixel; find first intersection.

---

## Quick Recap Table

| Topic | Key Formulas / Concepts |
|---|---|
| BNF | `<non-terminal> ::= production` ; terminals and non-terminals |
| Binding times | Language design → compile → link → load → runtime |
| Array Address (row-major) | `base + (i × n_cols + j) × elem_size` |
| Carry-Lookahead | `Gᵢ = AᵢBᵢ`; `Pᵢ = Aᵢ⊕Bᵢ`; `Cᵢ₊₁ = Gᵢ + PᵢCᵢ` |
| DDA Algorithm | `steps = max(|dx|,|dy|)`; `x_inc=dx/steps`; `y_inc=dy/steps` |
| Bresenham Line | Integer arithmetic; initial `p = 2dy - dx`; `p<0: p+=2dy`; else `p+=2dy-2dx` |
| Mid-point Circle | `p₀ = 1-r`; `p<0: p+=2x+1`; else `p+=2x-2y+1`; 8-way symmetry |
| Mid-point Ellipse | Two regions; decision based on `2b²x vs 2a²y` |
| Scan-line Fill | ET + AET; fill between intersection pairs per scan line |
| 2D Translation | `x'=x+tx, y'=y+ty`; `[1,0,tx; 0,1,ty; 0,0,1]` |
| 2D Rotation | `x'=xcosθ-ysinθ, y'=xsinθ+ycosθ` |
| 2D Scaling | `x'=x·sx, y'=y·sy`; `[sx,0,0; 0,sy,0; 0,0,1]` |
| 2D Shear (x) | `x'=x+shx·y, y'=y`; `[1,shx,0; 0,1,0; 0,0,1]` |
| Reflection (x-axis) | `[1,0,0; 0,-1,0; 0,0,1]` |
| Window-Viewport | `xv = xvmin + (xw-xwmin)·(xvmax-xvmin)/(xwmax-xwmin)` |
| Cohen-Sutherland | 4-bit outcode; accept if both 0000; reject if AND ≠ 0 |
| Liang-Barsky | `pᵢ<0→t_enter=max(t_enter,q/p)`; `pᵢ>0→t_exit=min(t_exit,q/p)` |
| Bezier curve | `P(t) = Σ Bᵢ,ₙ(t)·Pᵢ`; `Bᵢ,ₙ(t) = C(n,i)tⁱ(1-t)^(n-i)` |
| Bezier tangent | `P'(0) = n(P₁-P₀)`; `P'(1) = n(Pₙ-Pₙ₋₁)` |
| de Casteljau | `Pᵢʳ = (1-t)Pᵢʳ⁻¹ + t·Pᵢ₊₁ʳ⁻¹` |
| B-Spline basis | Cox-de Boor recursion; local support |
| Surface normal | `N = (P2-P1) × (P3-P1)` |
| Phong model | `I = Iₐkₐ + Iₗ[kd(N̂·L̂) + ks(R̂·V̂)^n]` |
| Reflection vector | `R̂ = 2(N̂·L̂)N̂ - L̂` |
| Blinn-Phong | `H̃ = (L̂+V̂)/|L̂+V̂|`; `I_spec = ks(N̂·H̃)^n` |
| Perspective proj | `x' = xd/z`; `y' = yd/z` |
| Back-face culling | Cull if `N̂·V̂ < 0` |
| Z-buffer | `if z_new < z_buf[x][y]`: write pixel |
| Quaternion rotation | `q = cos(θ/2) + sin(θ/2)(xi+yj+zk)` |

---

