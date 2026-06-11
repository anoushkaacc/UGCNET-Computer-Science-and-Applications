# UGC NET – Unit 5: System Software and Operating System
---
## 1. System Software

### 1.1 Machine, Assembly, and High-Level Languages

| Level | Language | Characteristics |
|---|---|---|
| **Machine Language** | Binary code (0s and 1s) | Directly executed by CPU; machine-dependent; no translation needed |
| **Assembly Language** | Mnemonic instructions (MOV, ADD, JMP) | One-to-one correspondence with machine instructions; requires assembler |
| **High-Level Language** | C, Java, Python, Fortran | Machine-independent; requires compiler or interpreter; closer to human language |

**Assembler:** Translates assembly language into machine code.
- **Two-pass assembler:**
  - Pass 1: Build symbol table (label → address).
  - Pass 2: Generate machine code using symbol table.
- **One-pass assembler:** Forward references handled via backpatching.

### 1.2 Compilers and Interpreters

| Aspect | Compiler | Interpreter |
|---|---|---|
| **Translation** | Entire program translated before execution | Translated and executed line by line |
| **Output** | Object code (executable) | No separate object code generated |
| **Speed** | Faster execution (translated once) | Slower execution (translated each run) |
| **Error Detection** | All errors reported after full scan | Errors reported at first occurrence |
| **Memory** | More memory for object code | Less memory; no object code |
| **Examples** | C, C++, Fortran, Pascal | Python (default), Ruby, BASIC |

**Compiler Phases:**
```
Source → Lexical Analysis → Syntax Analysis → Semantic Analysis
       → Intermediate Code Generation → Optimisation → Code Generation → Target Code
```

**Hybrid approach:** Java compiles to bytecode (JVM interprets); Python compiles to .pyc then interprets.

### 1.3 Loading, Linking, and Relocation

**Loader:** Loads executable program into memory for execution.

**Types of Loading:**
- **Absolute Loading:** Program loaded at a fixed, predetermined address. Simple but inflexible.
- **Relocatable Loading:** Program can be loaded at any available address; addresses adjusted at load time.
- **Dynamic Loading:** Routines loaded into memory only when called. Saves memory.
- **Dynamic Linking:** Linking deferred until execution time (shared libraries, DLLs).

**Linker:** Combines multiple object modules into a single executable.

**Linking Steps:**
1. **Symbol Resolution:** Match each symbol reference to exactly one symbol definition.
2. **Relocation:** Merge sections; assign final runtime addresses; update all references.

**Types of Linking:**
| Type | When | Advantage |
|---|---|---|
| **Static Linking** | Compile/link time | Self-contained; no runtime dependency |
| **Dynamic Linking** | Load time or run time | Smaller executables; shared code in memory; updates without relinking |

**Relocation:** Process of modifying object code so it can run at a different memory address.
- **Relocation Register (Base Register):** Hardware support; all logical addresses + relocation register = physical address.
- **Relocation Types:** Absolute relocation (fixed address); relative relocation (offset from current position).

**Object Module Structure:**
- Header, Text segment (code), Data segment, Relocation information, Symbol table, Debug information.

### 1.4 Macros

- A macro is a named sequence of instructions that is substituted (expanded) wherever the macro name appears.
- **Macro vs Subroutine:** Macro = textual substitution (inline expansion); subroutine = one copy + call overhead.

**Macro Processor:**
- **Definition:** `MACRO name params ... MEND`
- **Call (Invocation):** Macro name with arguments.
- **Expansion:** Textual substitution with argument replacement.
- **Macro vs Procedure:** Macros expand at assembly time (no runtime overhead, more code space); procedures called at runtime.

**Nested Macros:** A macro definition containing another macro definition.
**Recursive Macros:** A macro that calls itself; must have a termination condition.

### 1.5 Debuggers

- Tool to test and debug programs; allows control of program execution.

**Features:**
- **Breakpoints:** Stop execution at a specified line/address.
- **Watchpoints:** Stop when a variable's value changes.
- **Single Stepping:** Execute one instruction at a time.
- **Stack Trace:** Display call stack at point of error.
- **Memory Inspection:** View contents of memory and registers.
- **Core Dump Analysis:** Post-mortem debugging of crash dump.

**Types:**
- **Source-level debugger:** Works with original source code (GDB, lldb).
- **Machine-level debugger:** Works with machine code.
- **Post-mortem debugger:** Analyses crash dumps after failure.
- **Remote debugger:** Debugs program running on a different machine.

---

## 2. Basics of Operating Systems

### 2.1 Operating System Structure and Goals

- **OS:** Software that manages hardware resources and provides services to application programs.
- **Goals:** Convenience (user-friendly), Efficiency (optimal use of hardware), Extensibility.

**OS Functions:**
- Process management, Memory management, File system management, I/O management, Security and protection, Networking.

**OS Types:**
| Type | Description | Example |
|---|---|---|
| **Batch OS** | Jobs collected in batches; no user interaction | IBM OS/360 |
| **Multiprogrammed** | Multiple jobs in memory; CPU switches on I/O wait | OS/MFT |
| **Time-Sharing** | CPU switches rapidly; each user gets a time slice | UNIX |
| **Real-Time OS (RTOS)** | Strict timing constraints | VxWorks, FreeRTOS |
| **Distributed OS** | Manages multiple machines as one | Amoeba, Plan 9 |
| **Embedded OS** | Resource-constrained devices | Android, iOS |

### 2.2 OS Structure

| Structure | Description | Example |
|---|---|---|
| **Monolithic** | All OS services in kernel space; fast but hard to maintain | Early UNIX, Linux |
| **Layered** | OS divided into layers; each layer uses layer below | THE OS |
| **Microkernel** | Minimal kernel; services as user-space processes; more reliable | Mach, QNX, Minix |
| **Module-based** | Kernel with loadable modules; object-oriented | Modern Linux |
| **Hybrid** | Combination (e.g., microkernel + monolithic) | Windows NT, macOS |
| **Exokernel** | Minimal abstractions; apps manage resources directly | Research systems |

### 2.3 Operating System Services

- Program execution, I/O operations, File system manipulation, Communication, Error detection.
- **User interface:** CLI (command-line), GUI, Touch.
- **Resource allocation, Accounting, Protection and Security.**

### 2.4 System Calls

- Interface between user programs and OS kernel.
- User program calls library function (e.g., `read()`) → library executes **trap/interrupt** → CPU switches to kernel mode → OS handles request → return to user mode.

**Types of System Calls:**

| Category | Examples |
|---|---|
| **Process Control** | `fork()`, `exec()`, `exit()`, `wait()`, `kill()` |
| **File Management** | `open()`, `read()`, `write()`, `close()`, `stat()` |
| **Device Management** | `ioctl()`, `read()`, `write()` on devices |
| **Information Maintenance** | `getpid()`, `alarm()`, `sleep()`, `time()` |
| **Communication** | `pipe()`, `socket()`, `send()`, `recv()`, `shmget()` |
| **Protection** | `chmod()`, `chown()`, `umask()` |

**User Mode vs Kernel Mode:**
- **User Mode:** Restricted access; cannot directly access hardware or kernel memory.
- **Kernel Mode:** Full access to hardware and memory; OS code runs here.
- **Mode Bit:** Hardware bit; 0 = kernel mode, 1 = user mode.

### 2.5 OS Design and Implementation

- **Policy vs Mechanism:** Policy = what to do; Mechanism = how to do it. Separation improves flexibility.
- **Implementation:** Mostly in C/C++ (kernel); some assembly for low-level hardware interaction.

### 2.6 System Boot

1. Power on → **BIOS/UEFI** runs POST (Power-On Self Test).
2. BIOS loads **bootloader** (GRUB, LILO) from MBR (Master Boot Record) or EFI partition.
3. Bootloader loads the OS **kernel** into memory and transfers control to it.
4. Kernel initialises hardware, sets up memory management, starts first process (`init` / `systemd` with PID 1).
5. `init` starts system services; brings system to desired run level / target.

---

## 3. Process Management

### 3.1 Process Concepts

- **Process:** A program in execution. A program is passive (on disk); a process is active (in memory, has state).

**Process Memory Layout:**
```
High Address
┌──────────────┐
│   Stack      │ ← function calls, local variables (grows downward)
├──────────────┤
│    ↓  ↑      │
│   Heap       │ ← dynamically allocated memory (grows upward)
├──────────────┤
│   Data (BSS) │ ← uninitialised global/static variables
├──────────────┤
│   Data       │ ← initialised global/static variables
├──────────────┤
│   Text       │ ← program code (read-only)
└──────────────┘
Low Address
```

**Process Control Block (PCB):** OS data structure for each process.
- Contains: Process state, PID, Program counter, CPU registers, Memory management info, I/O status, Accounting info, Scheduling info.

**Process States:**
```
New → Ready → Running → Terminated
                ↓  ↑
              Waiting (Blocked)
```
- **New:** Process being created.
- **Ready:** Waiting to be assigned CPU.
- **Running:** Instructions being executed.
- **Waiting:** Waiting for I/O or event.
- **Terminated:** Finished execution.

### 3.2 Process Scheduling

**Queues:**
- **Job Queue:** All processes in the system.
- **Ready Queue:** Processes in memory, ready and waiting for CPU.
- **Device Queues:** Processes waiting for I/O device.

**Schedulers:**
| Scheduler | Role | Frequency |
|---|---|---|
| **Long-term (Job)** | Selects processes to bring into ready queue | Infrequent |
| **Short-term (CPU)** | Selects from ready queue for CPU execution | Very frequent (ms) |
| **Medium-term** | Swaps processes in/out (memory ↔ disk) | Intermediate |

**Context Switch:** Saving state of current process and loading state of next process.
- Pure overhead; no useful work done during context switch.
- Time: hardware-dependent; typically microseconds.

### 3.3 Process Operations

**Process Creation:**
- `fork()`: Creates an exact copy (child) of the calling process (parent). Returns PID of child to parent; returns 0 to child.
- `exec()`: Replaces process's memory space with a new program. Does not create a new process.
- `fork()` + `exec()` = standard Unix way to create and run a new program.

**Process Trees:** Parent creates children; forms a tree rooted at `init/systemd` (PID 1).

**Zombie Process:** Child has terminated but parent has not yet called `wait()`. Entry remains in process table.

**Orphan Process:** Parent terminated before child. Adopted by `init`.

**Process Termination:**
- `exit()`: Process asks OS to delete it. Resources released.
- `wait()`: Parent waits for child termination; retrieves exit status; cleans up zombie.
- `abort()`: Parent can terminate a child (if child exceeds resource limits, task no longer required, parent is exiting and cascading termination is required).

### 3.4 Interprocess Communication (IPC)

**Reasons for IPC:** Information sharing, computation speedup, modularity, convenience.

**IPC Models:**
| Model | Description | Example |
|---|---|---|
| **Shared Memory** | Processes share a region of memory; faster; requires synchronisation | POSIX `shmget`, `mmap` |
| **Message Passing** | Processes communicate via messages; no shared memory needed | `pipe`, `socket`, `send/recv` |

**Message Passing:**
- **Direct Communication:** Sender/receiver explicitly name each other. `send(P, msg)`, `receive(Q, msg)`.
- **Indirect Communication:** Messages sent to/received from **mailboxes (ports)**.
- **Synchronous (Blocking):** Sender blocked until message received; receiver blocked until message available.
- **Asynchronous (Non-blocking):** Sender continues after sending; receiver gets message or null.
- **Buffering:** Zero-capacity (rendezvous), bounded, unbounded buffer.

### 3.5 Communication in Client-Server Systems

| Mechanism | Description |
|---|---|
| **Sockets** | Endpoint of communication; IP address + port. Types: TCP (stream), UDP (datagram), Unix domain socket |
| **Remote Procedure Calls (RPC)** | Call procedure on a remote machine transparently; stubs handle marshalling/unmarshalling |
| **Pipes** | Unidirectional byte stream; `read` end and `write` end |
| **Named Pipes (FIFO)** | Like pipes but have a name in filesystem; can be used by unrelated processes |

**RPC Steps:** Client calls stub → stub marshals parameters → network sends to server → server stub unmarshals → calls actual function → result returned via same path.

**External Data Representation (XDR):** Standardised encoding for RPC parameters across different architectures.

### 3.6 Process Synchronization

**Race Condition:** Two or more processes access shared data concurrently; outcome depends on execution order.

**Critical Section:** Code segment where shared resources are accessed.

**Requirements for a solution to the Critical-Section Problem:**
1. **Mutual Exclusion:** Only one process in its critical section at a time.
2. **Progress:** If no process is in its CS and some wish to enter, only those processes not in their remainder section participate in the decision; decision cannot be postponed indefinitely.
3. **Bounded Waiting:** A bound must exist on the number of times other processes enter their CS after a process has made a request, before that request is granted.

### 3.7 Peterson's Solution

- Software solution for 2 processes (P₀ and P₁); assumes atomic load/store.
- **Shared variables:**
  - `int turn;` — whose turn it is to enter the CS.
  - `boolean flag[2];` — whether each process is ready to enter CS.

```c
/* Process Pᵢ (i = 0 or 1; j = 1 - i) */
flag[i] = TRUE;       // I want to enter
turn = j;             // But give the other process priority
while (flag[j] && turn == j);  // Busy-wait
    /* Critical Section */
flag[i] = FALSE;
    /* Remainder Section */
```

- **Proof of correctness:**
  - **Mutual Exclusion:** If both in CS, both `flag` are true and `turn` = i and turn = j simultaneously → impossible.
  - **Progress and Bounded Waiting:** If Pⱼ does not want to enter (`flag[j] = FALSE`), Pᵢ enters immediately. If both want to enter, `turn` determines who enters; other waits at most one entry.

- **Limitation:** Designed for 2 processes only; does not work on modern architectures without memory barriers (due to instruction reordering).

### 3.8 Semaphores

- **Semaphore S:** Integer variable accessed only through two atomic operations.

**Operations:**
```
wait(S) / P(S) / down(S):
    while S ≤ 0;  // busy-wait or block
    S = S - 1;

signal(S) / V(S) / up(S):
    S = S + 1;    // wake up one waiting process if any
```

**Types:**
- **Binary Semaphore (Mutex):** Value is 0 or 1. Used for mutual exclusion.
- **Counting Semaphore:** Value ranges over an unrestricted domain. Used for resource counting.

**Semaphore Implementation (without busy-waiting):**
```c
typedef struct {
    int value;
    struct process *list;  // waiting queue
} semaphore;

wait(S):
    S.value--;
    if (S.value < 0) {
        add this process to S.list;
        block();         // suspend process
    }

signal(S):
    S.value++;
    if (S.value <= 0) {
        remove a process P from S.list;
        wakeup(P);       // wake up P
    }
```

**Classical Synchronisation Problems:**

**1. Producer-Consumer (Bounded Buffer):**
```
Semaphores: mutex = 1, empty = N (buffer size), full = 0

Producer:                       Consumer:
wait(empty)                     wait(full)
wait(mutex)                     wait(mutex)
// add item                     // remove item
signal(mutex)                   signal(mutex)
signal(full)                    signal(empty)
```

**2. Readers-Writers Problem:**
- Multiple readers can read simultaneously; writer requires exclusive access.
```
Semaphores: rw_mutex = 1, mutex = 1
int read_count = 0;

Reader:                         Writer:
wait(mutex)                     wait(rw_mutex)
read_count++                    // write
if read_count == 1:             signal(rw_mutex)
    wait(rw_mutex)
signal(mutex)
// read
wait(mutex)
read_count--
if read_count == 0:
    signal(rw_mutex)
signal(mutex)
```

**3. Dining Philosophers Problem:**
- N philosophers; N chopsticks. Each needs 2 adjacent chopsticks to eat.
- **Naive solution:** Deadlock possible (all pick left chopstick simultaneously).
- **Solutions:** Allow at most N-1 philosophers at table; pick up both chopsticks atomically; asymmetric solution (odd picks left first, even picks right first).

**Monitors:**
- High-level synchronisation construct; encapsulates shared data and procedures.
- Only one process active inside monitor at a time (mutual exclusion guaranteed by compiler).
- **Condition variables:** `x.wait()` — suspends calling process; `x.signal()` — resumes one suspended process.
- Types: **Hoare monitor** (signal → immediate switch to waiting process); **Mesa monitor** (signal → waiting process goes to ready queue, re-checks condition).

---

## 4. Threads

### 4.1 Thread Concepts

- **Thread:** A unit of execution within a process; lightweight process.
- A process can have multiple threads sharing code, data, and OS resources; each thread has its own PC, registers, and stack.

**Benefits of Multithreading:**
- **Responsiveness:** One thread can continue while another is blocked.
- **Resource Sharing:** Threads share process memory (cheaper than IPC).
- **Economy:** Creating/switching threads is cheaper than processes.
- **Scalability:** Exploit multiprocessor architectures.

**Thread vs Process:**
| Aspect | Thread | Process |
|---|---|---|
| Sharing | Shares memory, files with other threads in process | Own separate address space |
| Creation overhead | Low | High |
| Communication | Direct (shared memory) | IPC required |
| Context switch | Faster | Slower |

### 4.2 Multicore Programming

- **Parallelism:** Multiple tasks executing simultaneously on multiple cores.
- **Concurrency:** Multiple tasks making progress (possibly on one core via time-sharing).

**Challenges:** Dividing tasks, balancing load, data splitting, data dependency, testing and debugging.

**Amdahl's Law:** Maximum speedup S with P processors and fraction f of serial code:
```
S ≤ 1 / (f + (1 - f) / P)
```
As P → ∞: `S ≤ 1/f`. Maximum speedup bounded by the serial fraction.

**Types of Parallelism:**
- **Data Parallelism:** Same operation on different subsets of data across cores.
- **Task Parallelism:** Different tasks/operations distributed across cores.

### 4.3 Multithreading Models

**User Threads:** Managed by user-level thread library; kernel unaware.
**Kernel Threads:** Managed directly by OS kernel.

| Model | Description | Advantage | Disadvantage | Example |
|---|---|---|---|---|
| **Many-to-One** | Many user threads → one kernel thread | Efficient; portable | Blocking call blocks all threads; no parallelism | Green threads (early Java) |
| **One-to-One** | Each user thread → one kernel thread | True parallelism; blocking doesn't affect others | Overhead; limited by kernel thread count | Linux pthreads, Windows |
| **Many-to-Many** | Many user threads → many (≤) kernel threads | Best of both; true parallelism possible | Complex to implement | Solaris (older), IRIX |
| **Two-level** | Like M:M but allows 1:1 binding for some | Flexible | Complex | HP-UX, IRIX |

### 4.4 Thread Libraries

- Provide API for creating and managing threads.

| Library | Type | Platform |
|---|---|---|
| **POSIX Pthreads** | User or kernel | Linux, macOS, Unix |
| **Windows Thread API** | Kernel | Windows |
| **Java Threads** | Kernel (via JVM) | Cross-platform |

**Pthreads Example:**
```c
pthread_t tid;
pthread_attr_t attr;
pthread_attr_init(&attr);
pthread_create(&tid, &attr, function, arg);
pthread_join(tid, NULL);
```

### 4.5 Implicit Threading

- Thread creation and management done by compilers and runtime libraries; programmer specifies parallelism.

| Technology | Description |
|---|---|
| **Thread Pools** | Pre-created pool of threads; tasks submitted and assigned; avoids creation overhead |
| **OpenMP** | Compiler directives (`#pragma omp parallel`) for C/C++/Fortran |
| **Grand Central Dispatch (GCD)** | Apple's task-based threading; dispatch queues |
| **Intel TBB (Threading Building Blocks)** | C++ template library for task parallelism |
| **Java Executor Framework** | `ExecutorService`; task submission with thread pool |

### 4.6 Threading Issues

| Issue | Description | Solution |
|---|---|---|
| **`fork()` and `exec()` semantics** | Should fork duplicate all threads or just calling thread? | POSIX: both options exist; exec replaces all threads |
| **Signal Handling** | Where to deliver signals to multithreaded process? | Deliver to thread it applies to; or designated signal-handling thread |
| **Thread Cancellation** | Terminating thread before completion | Asynchronous (immediate) vs Deferred (at cancellation point) |
| **Thread-Local Storage (TLS)** | Each thread has its own private data | `__thread` (C), `ThreadLocal` (Java) |
| **Scheduler Activations** | Communication between user-thread library and kernel | LWP (lightweight process) as virtual processor |

---

## 5. CPU Scheduling

### 5.1 Scheduling Criteria

| Criterion | Optimise | Description |
|---|---|---|
| **CPU Utilisation** | Maximise | Keep CPU as busy as possible (40–90%) |
| **Throughput** | Maximise | Number of processes completing per unit time |
| **Turnaround Time** | Minimise | Total time from submission to completion |
| **Waiting Time** | Minimise | Total time spent in ready queue |
| **Response Time** | Minimise | Time from request to first response |

**Definitions:**
- `Turnaround Time = Completion Time - Arrival Time`
- `Waiting Time = Turnaround Time - Burst Time`
- `Response Time = Time of first CPU grant - Arrival Time`

### 5.2 Scheduling Algorithms

**1. First-Come, First-Served (FCFS):**
- Non-preemptive; processes served in arrival order.
- **Convoy Effect:** Short processes wait for one long process.
- Average waiting time depends heavily on arrival order.

**2. Shortest Job First (SJF):**
- Non-preemptive; select process with smallest burst time.
- **Optimal** for minimising average waiting time.
- **Problem:** Cannot know exact burst time in advance; use prediction.

**3. Shortest Remaining Time First (SRTF):**
- Preemptive version of SJF.
- On new arrival, if its burst time < remaining time of current process → preempt.
- **Optimal preemptive** algorithm for minimising average waiting time.

**4. Round Robin (RR):**
- Preemptive; each process gets a **time quantum (q)**.
- If quantum expires → process preempted and moved to end of ready queue.
- **No starvation.**
- If q is very large → degenerates to FCFS.
- If q is very small → too many context switches.
- **Rule of thumb:** 80% of CPU bursts should be shorter than q.
- Average waiting time: `(n-1) × q / 2` (approximately, for equal burst times).

**5. Priority Scheduling:**
- Each process has a priority; CPU given to highest-priority process.
- **Preemptive or Non-preemptive.**
- **Starvation:** Low-priority processes may never execute.
- **Ageing:** Gradually increase priority of waiting processes to prevent starvation.
- SJF is priority scheduling where priority = predicted next CPU burst.

**6. Multilevel Queue Scheduling:**
- Ready queue partitioned into multiple queues (e.g., foreground, background).
- Each queue has its own scheduling algorithm.
- Fixed priority between queues; or time-sliced between queues.

**7. Multilevel Feedback Queue (MLFQ):**
- Processes can move between queues based on behaviour.
- New processes enter highest-priority queue; if they use full quantum, demoted; I/O-bound processes stay high.
- Most general and widely used CPU scheduling algorithm.

**CPU Burst Prediction (Exponential Averaging):**
```
τₙ₊₁ = α × tₙ + (1 - α) × τₙ
```
where:
- `tₙ` = actual nth CPU burst length.
- `τₙ` = predicted nth burst.
- `α` = weighting factor, `0 ≤ α ≤ 1` (typically `α = 0.5`).

**Expanding the recurrence:**
`τₙ₊₁ = α tₙ + (1-α) α tₙ₋₁ + (1-α)² α tₙ₋₂ + ... + (1-α)ⁿ τ₁`
(Recent history weighted more heavily due to geometric decay.)

**Gantt Chart Example (RR, q=2):**

| Process | Arrival | Burst |
|---|---|---|
| P1 | 0 | 5 |
| P2 | 1 | 3 |
| P3 | 2 | 1 |

```
P1   P2   P3   P1   P2   P1
|0   |2   |4   |5   |7   |8   |10
```
- WT(P1)=(2-0)+(7-4)=5, WT(P2)=(4-1)+(8-6)=5, WT(P3)=(5-2)=3; Avg WT = 13/3 ≈ 4.33

### 5.3 Thread Scheduling

- **Process Contention Scope (PCS):** Scheduling among threads within the same process (user-level library).
- **System Contention Scope (SCS):** Scheduling among all kernel threads in the system.
- Pthreads allows specifying `PTHREAD_SCOPE_PROCESS` or `PTHREAD_SCOPE_SYSTEM`.

### 5.4 Multiple Processor Scheduling

- **Asymmetric Multiprocessing (AMP):** One master processor handles scheduling; others execute user code. Simple but master is bottleneck.
- **Symmetric Multiprocessing (SMP):** Each processor is self-scheduling. All processes in common ready queue or each with private queue. Used by Linux, Windows.

**Processor Affinity:** Process has affinity for processor it ran on last (warm cache).
- **Soft Affinity:** OS tries to keep process on same processor; not guaranteed.
- **Hard Affinity:** Process specifies processor(s) it must run on (Linux `sched_setaffinity`).

**Load Balancing:** Keep all CPUs busy. Used in SMP systems.
- **Push Migration:** Specific task checks and moves processes from overloaded to underloaded CPUs.
- **Pull Migration:** Idle processor pulls a process from a busy processor's queue.

**NUMA (Non-Uniform Memory Access):**
- Memory access times differ depending on which processor accesses which memory.
- NUMA-aware scheduling: assign memory to CPU whose memory is fastest.

### 5.5 Real-Time CPU Scheduling

- **Soft Real-Time:** Critical processes get priority; no guarantee of when scheduled.
- **Hard Real-Time:** Tasks must meet deadlines; missing deadline is a system failure.

**Real-Time Scheduling Algorithms:**

**Rate-Monotonic (RM):**
- Fixed-priority; shorter period = higher priority.
- Preemptive.
- CPU utilisation bound for n tasks: `U = Σ(Cᵢ/Tᵢ) ≤ n(2^(1/n) - 1)`
- As n → ∞: `U ≤ ln 2 ≈ 0.693`
- If utilisation ≤ bound → guaranteed schedulable.

**Earliest Deadline First (EDF):**
- Dynamic priority; process closest to deadline gets highest priority.
- **Optimal** preemptive algorithm for single processor.
- Can achieve 100% CPU utilisation theoretically.
- Utilisation condition: `Σ(Cᵢ/Tᵢ) ≤ 1`

**Least Laxity First (LLF) / Minimum Laxity:**
- Laxity = Deadline - Remaining computation time - Current time.
- Process with smallest laxity scheduled first.

**Notation:** For task τᵢ: `Cᵢ` = execution time, `Tᵢ` = period (= deadline for periodic tasks).

---

## 6. Deadlocks

### 6.1 Deadlock Characterization

**Definition:** A set of processes is deadlocked if every process in the set is waiting for an event that can only be caused by another process in the set.

**Four Necessary Conditions (all must hold simultaneously for deadlock):**
1. **Mutual Exclusion:** At least one resource is held in a non-sharable mode.
2. **Hold and Wait:** A process is holding at least one resource and is waiting for additional resources held by other processes.
3. **No Preemption:** Resources cannot be forcibly taken away; released only voluntarily.
4. **Circular Wait:** A set of processes `{P₀, P₁, ..., Pₙ}` where P₀ waits for resource held by P₁, P₁ waits for resource held by P₂, ..., Pₙ waits for resource held by P₀.

**Resource Allocation Graph (RAG):**
- **Vertices:** Processes (circles) and Resources (rectangles with dots for instances).
- **Request Edge:** P → R (process requests resource).
- **Assignment Edge:** R → P (instance of resource assigned to process).
- **Deadlock detection:**
  - If graph has no cycle → no deadlock.
  - If graph has a cycle:
    - If each resource type has exactly one instance → deadlock.
    - If resource types have multiple instances → cycle is necessary but not sufficient.

### 6.2 Methods for Handling Deadlocks

| Approach | Strategy |
|---|---|
| **Prevention** | Ensure at least one necessary condition can never hold |
| **Avoidance** | Dynamically decide if granting a resource leads to unsafe state |
| **Detection and Recovery** | Allow deadlock; detect and recover |
| **Ignorance (Ostrich)** | Pretend deadlock never occurs (used by most OS including Linux, Windows) |

### 6.3 Deadlock Prevention

Negate one of the four necessary conditions:

| Condition | Prevention Strategy |
|---|---|
| **Mutual Exclusion** | Make resources sharable (not always possible) |
| **Hold and Wait** | Process must request all resources at once; or release all before requesting new ones. Disadvantage: low utilisation, starvation |
| **No Preemption** | If process cannot get new resource, release all held resources. Disadvantage: not suitable for non-preemptible resources |
| **Circular Wait** | Impose total ordering on resource types; process must request in increasing order. Effectively prevents circular wait |

### 6.4 Deadlock Avoidance

- Requires advance information about maximum resource needs.
- **Safe State:** A state where there exists a **safe sequence** — an ordering of all processes such that each process can obtain all needed resources, finish, and release them for subsequent processes.
- **Safe State → No Deadlock; Deadlock → Unsafe State; Unsafe State does not guarantee deadlock.**

**Banker's Algorithm (E.W. Dijkstra):**
- For multiple instances of each resource type.
- **Data Structures (n = # processes, m = # resource types):**
  - `Available[m]`: Number of available instances of each resource type.
  - `Max[n][m]`: Maximum demand of each process.
  - `Allocation[n][m]`: Currently allocated to each process.
  - `Need[n][m]`: Remaining need. `Need[i][j] = Max[i][j] - Allocation[i][j]`

**Safety Algorithm:**
```
1. Work = Available; Finish[i] = false for all i.
2. Find i such that: Finish[i] == false AND Need[i] ≤ Work
   If none found, go to step 4.
3. Work = Work + Allocation[i]; Finish[i] = true; go to step 2.
4. If Finish[i] == true for all i → system is in safe state.
```

**Resource Request Algorithm:**
```
When process Pᵢ requests Request[i]:
1. If Request[i] ≤ Need[i], continue; else ERROR (exceeded maximum claim).
2. If Request[i] ≤ Available, continue; else wait (resources not available).
3. Pretend to allocate:
   Available = Available - Request[i]
   Allocation[i] = Allocation[i] + Request[i]
   Need[i] = Need[i] - Request[i]
4. Run safety algorithm. If safe → allocate. If unsafe → rollback (process must wait).
```

**Banker's Algorithm for Single Resource (Resource Allocation Graph with claim edges):**
- Add **claim edge** Pᵢ → Rⱼ (dashed) representing future request.
- When resource requested, convert to request edge; check for cycle.
- If no cycle in resulting graph → safe to grant.

### 6.5 Deadlock Detection

**Single instance of each resource:**
- Use **Wait-for Graph** (derived from RAG by removing resource nodes).
- Edge Pᵢ → Pⱼ: Pᵢ is waiting for resource held by Pⱼ.
- Deadlock iff wait-for graph contains a cycle.
- Cycle detection: O(n²) algorithm.

**Multiple instances of each resource:**
```
Data: Available[m], Allocation[n][m], Request[n][m]
1. Work = Available; Finish[i] = (Allocation[i] == 0) for all i.
2. Find i such that Finish[i] == false AND Request[i] ≤ Work.
   If none → go to step 4.
3. Work = Work + Allocation[i]; Finish[i] = true; go to step 2.
4. If Finish[i] == false for some i → process Pᵢ is deadlocked.
```

**Detection Frequency:** After every request (costly) or periodically (may allow deadlock to persist).

### 6.6 Recovery from Deadlock

**Process Termination:**
- Abort all deadlocked processes (simple but expensive).
- Abort one process at a time until deadlock cycle is broken (costly; must re-run detection).
- **Victim selection criteria:** Priority, runtime so far, resources held, resources needed, number of victims needed.

**Resource Preemption:**
- Selectively preempt resources from deadlocked processes and give to others.
- **Issues:** Selecting a victim, rollback (return preempted process to safe state), starvation (same process always victim).

---

## 7. Memory Management

### 7.1 Memory Hierarchy and Binding

**Address Binding:**
- **Compile time:** If memory location known at compile time → absolute code generated.
- **Load time:** If not known at compile time → relocatable code; linker binds at load time.
- **Execution time:** Binding delayed until runtime; requires hardware support (MMU).

**Logical (Virtual) Address:** Generated by CPU; what the program sees.
**Physical Address:** Actual address in memory hardware.

**Memory Management Unit (MMU):** Hardware device that maps logical to physical addresses.

### 7.2 Contiguous Memory Allocation

Each process occupies a single contiguous section of memory.

**Fixed-size Partitions:** Memory divided into fixed partitions.
- **Internal Fragmentation:** Allocated memory larger than requested; wasted space inside partition.

**Variable-size Partitions:**
- **External Fragmentation:** Free memory exists but is not contiguous; cannot satisfy a large request.
- **Compaction:** Shuffle memory contents to place all free memory together; costly.

**Allocation Strategies:**
| Strategy | Description | Fragmentation |
|---|---|---|
| **First Fit** | Allocate first hole that is big enough | Moderate; fastest |
| **Best Fit** | Allocate smallest hole that is big enough | Least external fragmentation; slow |
| **Worst Fit** | Allocate largest hole | Most external fragmentation; slow |

**First Fit and Best Fit are better than Worst Fit** in terms of time and storage utilisation.

### 7.3 Swapping

- Process temporarily moved from memory to backing store (disk) and back.
- Allows more processes than physical memory; increases degree of multiprogramming.
- **Modified/Enhanced Swapping:** Modern OS swaps pages/segments rather than entire processes.
- **Swap Space:** Dedicated disk area for swapping; faster than file system.
- **Swap-in / Swap-out** times dominated by transfer time; proportional to memory size swapped.

### 7.4 Paging

- Divide physical memory into fixed-size blocks called **frames**.
- Divide logical memory (process) into same-size blocks called **pages**.
- Page size = Frame size = power of 2 (typically 4 KB to 4 MB).
- **No external fragmentation; internal fragmentation** ≤ page size - 1 per process.

**Address Translation:**
- Logical address: `(page number p, page offset d)`.
- `p = logical address / page size`, `d = logical address mod page size`.
- `physical address = (frame number × page size) + d`
- Frame number = `page_table[p]`.

**Page Table:** Array indexed by page number; contains frame number.
- Each page table entry also contains: valid/invalid bit, dirty bit, reference bit, protection bits.

**Hardware Support:**
- **TLB (Translation Lookaside Buffer):** Fast associative cache of recently used page table entries.
- `TLB Hit`: Frame number from TLB → fast (single memory access).
- `TLB Miss`: Access page table in memory → load into TLB → two memory accesses.

**Effective Access Time (EAT):**
```
EAT = α × (TLB access time + memory access time)
    + (1 - α) × (TLB access time + 2 × memory access time)
```
where α = TLB hit ratio.

Simplified (assuming TLB access ≈ 0 or combined with memory access):
```
EAT = α × tm + (1 - α) × 2tm
    = (2 - α) × tm
```
where `tm` = memory access time, `α` = hit ratio.

**Hierarchical Page Tables:**
- For 32-bit address space with 4 KB pages: page table has `2^20` entries → too large.
- **Two-level paging:** Split page number into two parts.
  - Logical address: `(p₁, p₂, d)` where p₁ = outer page, p₂ = inner page, d = offset.
  - `outer_page_table[p₁]` → inner page table → `inner_page_table[p₂]` → frame.
- **64-bit:** Three or four levels may be needed.

**Inverted Page Table:**
- One entry per physical frame (not per logical page).
- Entry: `(PID, page number)`.
- Reduces page table size; but search time is O(n) — mitigated by hash table.
- Used in IBM RISC/6000, HP-UX.

**Shared Pages:** Multiple processes share same frames for shared libraries (read-only code).

**Page Table Size Calculation:**
- Address space = 2³² bytes, page size = 4 KB = 2¹² bytes.
- Number of pages = 2³²/2¹² = 2²⁰ entries.
- Each entry = 4 bytes → page table size = 4 MB per process.

### 7.5 Segmentation

- Logical view of memory; program divided into variable-size **segments** (code, data, stack, heap).
- **Logical Address:** `(segment number s, offset d)`.
- **Segment Table:** Array of `(base, limit)` pairs.
  - `base`: Starting physical address of segment.
  - `limit`: Length of segment.
- **Validation:** If `d ≥ limit` → trap (segmentation fault).
- **Physical address:** `base[s] + d` (if `d < limit[s]`).
- **External fragmentation** can occur; no internal fragmentation.

**Segmentation with Paging:** Used in x86 (Intel); segments paged to eliminate external fragmentation.

### 7.6 Demand Paging

- Pages loaded into memory only when needed (on demand).
- **Lazy swapper (pager):** Never swaps a page into memory unless it is needed.

**Page Fault Handling:**
1. Process accesses page → MMU checks page table.
2. Valid bit = 0 → **page fault** trap.
3. OS checks if reference is valid (if not → abort).
4. Find free frame (or page replacement).
5. Schedule disk I/O to read page into frame.
6. Update page table; set valid bit = 1.
7. Restart the faulting instruction.

**Effective Access Time with Page Faults:**
```
EAT = (1 - p) × memory access time + p × page fault time
```
where p = page fault rate (0 ≤ p ≤ 1).

Page fault time includes: service interrupt, read page from disk, restart process (~8ms for disk I/O).

For EAT < 10% degradation from memory access time tm = 200 ns:
```
EAT < 1.1 × tm = 220 ns
220 > (1-p) × 200 + p × 8,000,000
p < 0.0000025 (1 fault in ~400,000 accesses)
```

### 7.7 Page Replacement Algorithms

When a page fault occurs and no free frames exist, a victim page must be chosen.

**1. FIFO (First-In, First-Out):**
- Replace the oldest page in memory.
- **Belady's Anomaly:** Increasing number of frames may increase number of page faults.

**2. Optimal (OPT / MIN):**
- Replace page that will not be used for the longest time in the future.
- **Optimal** — lowest page fault rate.
- Not implementable in practice (requires future knowledge); used as benchmark.

**3. LRU (Least Recently Used):**
- Replace page not used for the longest time in the past.
- Good approximation of OPT; no Belady's Anomaly.
- **Implementation:** Counter per page (update on every access); or doubly-linked list.
- Expensive hardware support needed; software approximations used.

**4. LRU Approximation — Clock Algorithm (Second-Chance):**
- Each page has a **reference bit** (set to 1 on access, cleared by OS).
- Clock pointer advances; if reference bit = 1 → clear and skip; if reference bit = 0 → replace.
- **Enhanced Second-Chance:** Use `(reference bit, dirty bit)` pair:
  - `(0, 0)`: Best replacement candidate.
  - `(0, 1)`: Not recently used but dirty (must write to disk).
  - `(1, 0)`: Recently used; clean.
  - `(1, 1)`: Recently used; dirty; worst to replace.

**5. LFU (Least Frequently Used):** Replace page with smallest count.
**6. MFU (Most Frequently Used):** Replace page with largest count.

**Page Fault Rate Comparison:**
- Optimal < LRU ≤ Clock < FIFO (approximately).

### 7.8 Allocation of Frames

**Minimum number of frames:** Must allocate enough frames per process to execute one instruction without fault. Determined by instruction set architecture.

**Allocation Policies:**
- **Equal Allocation:** `m frames / n processes` frames per process.
- **Proportional Allocation:** `aᵢ = (sᵢ / Σsⱼ) × m` where sᵢ = size (virtual memory) of process i, m = total frames.
- **Priority Allocation:** Allocate proportionally to priority.

**Frame Allocation Scopes:**
- **Local Replacement:** Process replaces only its own frames.
- **Global Replacement:** Process can replace frames of other processes; generally better throughput.

**Working Set Model:**
- `Δ` = working set window (number of recent page references).
- `WS(tᵢ, Δ)` = set of pages referenced in the last Δ references.
- `|WS|` = working set size (number of pages in working set).
- `D = Σ|WSᵢ|` = total demand for frames.
- If `D > m` (total frames) → thrashing likely; suspend some processes.

### 7.9 Thrashing

- Process spends more time paging than executing.
- Occurs when: total page demand >> total available frames.
- **Cause:** Global replacement + no working set consideration.

**Thrashing Curve:**
- CPU utilisation increases with degree of multiprogramming up to a point.
- Beyond that point, adding more processes → thrashing → CPU utilisation drops sharply.

**Solutions:**
- Working set model (allocate at least |WS| frames per process).
- Page-fault frequency (PFF) algorithm: If fault rate too high → give more frames; too low → take frames away.
- **PFF Threshold:** Set upper and lower bounds on fault rate.

### 7.10 Memory-Mapped Files

- File I/O treated as memory access; file mapped to virtual address space.
- `mmap()` system call.
- **Advantages:** Simplified programming, faster access (no read/write system calls), sharing between processes.
- Multiple processes can map same file (shared memory via file).

---

## 8. Storage Management

### 8.1 Mass Storage Structure

**HDD (Hard Disk Drive):**
- **Structure:** Platters, tracks, sectors, cylinders, read-write heads.
- **Sector:** Smallest unit of disk I/O (typically 512 B or 4 KB).
- **Access Time:** `Seek Time + Rotational Latency + Transfer Time`
  - Seek Time: Time to move head to correct track.
  - Rotational Latency: Time for sector to rotate under head (avg = half rotation time).
  - Transfer Rate: Function of RPM and bytes per track.
- **Average rotational latency** = `1/(2 × RPM) × 60 seconds`

**SSD (Solid State Drive):**
- Flash memory; no moving parts.
- Faster random access; lower latency; limited write cycles.
- No seek or rotational delay; access time ≈ 0.1 ms.

### 8.2 Disk Scheduling Algorithms

Goal: Minimise seek time (head movement).

**1. FCFS:** Serve in arrival order; simple; not optimal.
**2. SSTF (Shortest Seek Time First):** Serve request closest to current head position; may cause starvation.
**3. SCAN (Elevator Algorithm):** Head moves in one direction; serves requests; reaches end, reverses.
**4. C-SCAN (Circular SCAN):** Like SCAN but on return journey, head moves to beginning without serving; more uniform wait times.
**5. LOOK:** Like SCAN but reverses at last request (not at disk end).
**6. C-LOOK:** Like C-SCAN but returns to first request rather than disk beginning.

**Example (SSTF):** Head at 53; requests: 98, 183, 37, 122, 14, 124, 65, 67.
- Order: 65, 67, 37, 14, 98, 122, 124, 183. Total head movement = 236 cylinders.

### 8.3 RAID (Redundant Array of Independent/Inexpensive Disks)

| Level | Description | Redundancy | Performance | Use |
|---|---|---|---|---|
| **RAID 0** | Striping; no redundancy | None | High read/write | Scratch disks, performance |
| **RAID 1** | Mirroring; duplicate data | Full copy | High read; same write | Critical data |
| **RAID 2** | Bit-level striping + Hamming ECC | Hamming code | Rarely used | Historical |
| **RAID 3** | Byte-level striping + dedicated parity disk | 1 parity disk | Good | Rarely used |
| **RAID 4** | Block-level striping + dedicated parity | 1 parity disk | Parity bottleneck | Uncommon |
| **RAID 5** | Block-level striping + distributed parity | 1 disk failure | Good; parity balanced | Most common |
| **RAID 6** | Like RAID 5 + double distributed parity | 2 disk failures | Slightly slower write | Enterprise |
| **RAID 10 (1+0)** | Mirrored stripes | Good | Very high | High performance critical |

**RAID 5 Minimum disks:** 3. **RAID 6 Minimum disks:** 4.
**Parity calculation in RAID 5:** `P = D₀ XOR D₁ XOR D₂ XOR ...`

---

## 9. File and I/O Systems

### 9.1 File System Concepts

- **File:** Named collection of related information recorded on secondary storage.
- **File Attributes:** Name, identifier, type, location, size, protection, time/date, owner.
- **File Operations:** Create, read, write, seek, delete, truncate, open, close.
- **Open-file Table:** Kernel structure tracking all currently open files.

**Access Methods:**
- **Sequential Access:** Read/write bytes in order (tape model): `read_next()`, `write_next()`, `rewind()`.
- **Direct (Random) Access:** Read/write at any position: `read(n)`, `write(n)`.
- **Index Sequential (ISAM):** Index over direct access; commonly used in databases.

### 9.2 Directory Structure

| Structure | Description | Advantage | Disadvantage |
|---|---|---|---|
| **Single-level** | All files in one directory | Simple | Name conflicts; no organisation |
| **Two-level** | Separate directory per user | User isolation | No subdirectories |
| **Tree-structured** | Hierarchical directories | Efficient search; organised | Cannot share files easily |
| **Acyclic Graph** | Allow shared directories/files | Sharing | Dangling pointers |
| **General Graph** | Allow cycles | — | Must handle cycles in traversal |

**Directory Implementation:**
- **Linear List:** Simple; O(n) search.
- **Hash Table:** O(1) average search; fixed table size or chaining.

### 9.3 File System Mounting

- A file system must be mounted before access.
- **Mount Point:** Directory where the file system is attached.
- `mount /dev/sdb1 /mnt/data` — mounts device sdb1 at /mnt/data.
- Unmount before removal to flush buffers: `umount /mnt/data`.
- **`/etc/fstab`:** Configuration file for automatic mounting at boot.

### 9.4 File Sharing and Protection

- **Access Control List (ACL):** List of users and permissions for each file.
- **Unix Protection:** Owner, Group, Others; permissions: Read (r=4), Write (w=2), Execute (x=1).
  - `chmod 755 file` → owner=rwx, group=r-x, others=r-x.
  - Numeric: each digit is sum of r+w+x for owner, group, others.

### 9.5 File System Implementation

**On-Disk Structures:**
- **Boot Control Block:** Boot information (MBR sector 0 or EFI partition).
- **Volume Control Block (Superblock):** Block count, block size, free block count, free inode count.
- **Inode:** File metadata (type, size, permissions, timestamps, block pointers).
- **Data Blocks:** Actual file contents.

**In-Memory Structures:**
- **Mount Table:** Mounted file systems info.
- **Directory Cache:** Recently accessed directories.
- **System-wide Open-File Table:** Per-file: inode, file size, current position.
- **Per-process Open-File Table:** Current file position, access rights.

### 9.6 Disk Allocation Methods

**1. Contiguous Allocation:**
- Each file occupies contiguous blocks on disk.
- Directory entry: `(start block, length)`.
- **Pros:** Simple; fast sequential and direct access; minimal seek time.
- **Cons:** External fragmentation; file cannot grow easily; must know file size in advance.

**2. Linked Allocation:**
- Each block contains a pointer to the next block; last block has null pointer.
- Directory entry: `(start block, end block)`.
- **Pros:** No external fragmentation; file can grow easily.
- **Cons:** Sequential access only (no direct access); pointer overhead per block; reliability (lost pointer loses rest of file).
- **FAT (File Allocation Table):** Linked list maintained in a separate table in memory; allows direct access.

**3. Indexed Allocation:**
- One **index block** per file; index block contains list of block pointers.
- Directory entry: `(index block)`.
- **Pros:** Supports direct access; no external fragmentation.
- **Cons:** Pointer overhead; small files waste index block.

**Large File Index Block Schemes:**
- **Linked Index Blocks:** Last entry of index block points to another index block.
- **Multilevel Index:** Index block points to second-level index blocks.
- **Combined (Unix inode):**
  - Direct pointers (12 in inode): Point directly to data blocks.
  - Single indirect: Pointer to a block of direct pointers.
  - Double indirect: Pointer to block of single-indirect blocks.
  - Triple indirect: Pointer to block of double-indirect blocks.

**File Size Calculation (Unix inode with 4 KB blocks, 4-byte pointers):**
- Pointers per block: 4096 / 4 = 1024.
- Direct: 12 blocks.
- Single indirect: 1024 blocks.
- Double indirect: 1024² = 1,048,576 blocks.
- Triple indirect: 1024³ blocks.
- Maximum file size ≈ (12 + 1024 + 1024² + 1024³) × 4 KB ≈ 4 TB.

### 9.7 Free Space Management

| Method | Description | Performance |
|---|---|---|
| **Bit Vector (Bitmap)** | One bit per block; 1 = free, 0 = allocated | Easy to find contiguous blocks; simple |
| **Linked List** | Link all free blocks together | No wasted space; traversal needed; slow |
| **Grouping** | First free block stores addresses of n free blocks; last = next group | Faster than linked list |
| **Counting** | Store (first free block, count of consecutive free blocks) | Efficient for contiguous allocation |
| **Space Maps (ZFS)** | Divide device into metaslabs; bitmap + space map log | Scales to very large storage |

### 9.8 I/O Hardware

**I/O Components:** Port, Bus (daisy chain or shared direct access), Device controller, Interrupt mechanism, DMA.

**I/O Techniques:**
| Technique | Description | CPU Involvement |
|---|---|---|
| **Programmed I/O (Polling)** | CPU continuously checks device status | High (busy-wait) |
| **Interrupt-Driven I/O** | Device interrupts CPU when ready | Moderate (interrupt handling) |
| **DMA (Direct Memory Access)** | DMA controller handles transfer; interrupts CPU only on completion | Low; CPU free during transfer |

**Interrupt Mechanism:**
1. Device signals interrupt request (IRQ).
2. CPU finishes current instruction; checks interrupt line.
3. CPU saves state; jumps to Interrupt Service Routine (ISR) via interrupt vector.
4. ISR handles interrupt; restores CPU state; returns.

**Interrupt Priority Levels:** Higher-priority interrupts can preempt lower-priority ISRs.

### 9.9 Application I/O Interface

**I/O Device Categories:**

| Category | Characteristics | Examples |
|---|---|---|
| **Block Device** | Fixed-size blocks; random access | Disk, SSD |
| **Character Device** | Byte stream; sequential | Keyboard, serial port |
| **Network Device** | Socket interface | NIC |
| **Clock/Timer** | Time measurement, alarms | System clock |

**Blocking vs Non-blocking vs Asynchronous I/O:**
- **Blocking I/O:** System call blocks until I/O complete; simple programming.
- **Non-blocking I/O:** Returns immediately with available data (may be 0 bytes).
- **Asynchronous I/O:** I/O continues; process notified on completion via signal or callback.

### 9.10 Kernel I/O Subsystem

**I/O Scheduling:** Order I/O requests for efficiency (like CPU scheduling for disk).
**Buffering:** Store data in buffer while transferring between devices with different speeds.
- Single buffer, double buffer, circular buffer.
**Caching:** Keep copy of frequently used data in faster memory (page cache, buffer cache).
**Spooling:** Buffer output for devices that can serve only one request at a time (e.g., printer spool).
**Device Reservation:** Exclusive access to a device (e.g., tape drive).

---

## 10. Security

### 10.1 Protection and Access Control

**Goals of Protection:** Prevent malicious misuse; ensure each resource used only in authorised ways.

**Access Matrix:**
- `Access[i][j]` = set of operations process i can perform on object j.
- Rows = processes/domains; columns = objects.
- **Operations:** Read, Write, Execute, Append, Delete.
- **Sparse matrix** in practice; implemented as:
  - **Access Control Lists (ACL):** Each object has a list of (domain, operations) pairs (column of access matrix).
  - **Capability Lists:** Each domain has a list of (object, operations) pairs (row of access matrix).

**Revocation of Access Rights:**
| Method | ACL | Capability |
|---|---|---|
| **Immediate** | Easy (modify ACL) | Difficult |
| **Selective** | Easy | Difficult |
| **Partial** | Possible | Difficult |
| **Temporary** | Possible | Difficult |

### 10.2 Program Threats

| Threat | Description |
|---|---|
| **Trojan Horse** | Hidden malicious code in legitimate program |
| **Trap Door (Backdoor)** | Secret entry point in software left by developer |
| **Logic Bomb** | Code that activates under specific conditions |
| **Stack/Buffer Overflow** | Write beyond buffer to overwrite return address; gain control |
| **Virus** | Self-replicating; attaches to host program |
| **Worm** | Self-replicating; spreads without host |
| **Rootkit** | Hides malicious processes/files; modifies OS |
| **Ransomware** | Encrypts user data; demands payment |

### 10.3 System and Network Threats

| Threat | Description |
|---|---|
| **Port Scanning** | Probe open ports to find vulnerable services |
| **Denial of Service (DoS)** | Overwhelm resources; deny legitimate access |
| **Distributed DoS (DDoS)** | DoS from multiple sources (botnet) |
| **Man-in-the-Middle** | Attacker intercepts communication |
| **Replay Attack** | Re-send captured authentication messages |
| **IP Spoofing** | Forge source IP address |
| **Sniffing** | Capture network packets |
| **SQL Injection** | Inject SQL into input fields |
| **XSS (Cross-Site Scripting)** | Inject scripts into web pages |

### 10.4 Cryptography as a Security Tool

See Unit 9 notes for full coverage. Summary:
- **Symmetric:** AES (block cipher); fast; key distribution problem.
- **Asymmetric:** RSA; public/private key pair; slow; `C = M^e mod n`, `M = C^d mod n`.
- **Hash:** SHA-256; one-way; integrity verification.
- **Digital Signature:** Sign with private key; verify with public key.
- **SSL/TLS:** Secure communication protocol; uses hybrid (asymmetric for key exchange, symmetric for data).

### 10.5 User Authentication

| Method | Type | Examples |
|---|---|---|
| **Password** | Something you know | Unix `/etc/shadow`; salted hash |
| **Token** | Something you have | Smart card, RSA SecurID, OTP |
| **Biometric** | Something you are | Fingerprint, iris, facial recognition |
| **Multi-factor (MFA)** | Combination | Password + OTP |

**Password Storage:** Store `H(salt || password)` where H is a hash function and salt is a random value.
- Salt prevents precomputed dictionary attacks (rainbow tables).

### 10.6 Implementing Security Defenses

| Defense | Description |
|---|---|
| **Firewall** | Filter network traffic based on rules |
| **Intrusion Detection System (IDS)** | Detect attacks; signature-based or anomaly-based |
| **Intrusion Prevention System (IPS)** | Detect and block attacks |
| **Principle of Least Privilege** | Grant only minimum necessary permissions |
| **Defence in Depth** | Multiple layers of security |
| **Code Signing** | Verify software integrity with digital signature |
| **Address Space Layout Randomisation (ASLR)** | Randomise memory layout; defeat buffer overflow exploits |
| **Data Execution Prevention (DEP/NX)** | Mark data segments non-executable; prevent shellcode execution |
| **Sandboxing** | Isolate process in restricted environment |
| **Audit Logging** | Record security-relevant events for analysis |

---

## 11. Virtual Machines

### 11.1 Types of Virtual Machines

**Type 1 Hypervisor (Bare Metal):**
- Runs directly on physical hardware.
- Guest OS runs on top of hypervisor.
- Examples: VMware ESXi, Microsoft Hyper-V, Xen, KVM.
- Better performance; used in enterprise/cloud.

**Type 2 Hypervisor (Hosted):**
- Runs as an application on a host OS.
- Guest OS runs inside the hypervisor application.
- Examples: VMware Workstation, VirtualBox, QEMU.
- Easier to install; lower performance.

**Paravirtualisation:**
- Guest OS modified to be aware of hypervisor; uses hypercalls instead of privileged instructions.
- Better performance than full virtualisation.
- Example: Xen with modified guest kernels.

**Hardware-Assisted Virtualisation:**
- CPU provides special instructions for virtualisation (Intel VT-x, AMD-V).
- Eliminates need to trap-and-emulate privileged instructions.
- Enables full virtualisation without paravirtualisation.

**Container-based Virtualisation:**
- OS-level virtualisation; containers share host OS kernel.
- Much lighter than VMs; faster startup; lower overhead.
- Isolation via **namespaces** (PID, network, mount, user) and **cgroups** (resource limits).
- Examples: Docker, LXC, Kubernetes.

**Comparison: VM vs Container:**
| Aspect | Virtual Machine | Container |
|---|---|---|
| OS | Full OS per VM | Shared host OS kernel |
| Size | GBs | MBs |
| Startup | Minutes | Seconds |
| Isolation | Strong | Weaker |
| Portability | Less | More |

### 11.2 Virtualisation Benefits

- **Isolation:** Fault and security isolation between VMs.
- **Resource consolidation:** Run multiple OS on one physical machine.
- **Snapshots:** Save/restore VM state.
- **Live migration:** Move running VM between physical hosts with minimal downtime.
- **Testing:** Run multiple OS versions simultaneously.
- **Cloud computing:** Foundation of IaaS.

---

## 12. Linux Operating System

### 12.1 Design Principles

- **Monolithic kernel** with loadable kernel modules.
- **POSIX-compliant**; everything is a file (devices, sockets, pipes).
- **Multiuser, multitasking, multiprocessor** support.
- Open source (GPL license); highly portable.
- Policy-mechanism separation; many configurable parameters.

### 12.2 Kernel Modules

- Extend kernel functionality without recompiling or rebooting.
- Loaded/unloaded dynamically: `insmod`, `rmmod`, `modprobe`, `lsmod`.
- Common modules: device drivers, file system drivers, network protocols.
- `modprobe` handles dependencies; `insmod` does not.

### 12.3 Linux Process Management

- **Task (Process/Thread):** Represented by `struct task_struct` in kernel.
- `fork()` uses **Copy-On-Write (COW):** Child initially shares parent's pages; copy made only on write.
- `clone()` system call: More fine-grained than `fork()`; used to create threads (specifies which resources to share).
- **Process states:** Running, Interruptible (waiting, can be woken by signal), Uninterruptible (waiting, cannot be interrupted), Stopped, Zombie.
- **Namespaces:** Isolate PID, network, mount, UTS, IPC, user namespaces.
- **cgroups (Control Groups):** Limit, account, and isolate resource usage of process groups.

### 12.4 Linux Scheduling

- **CFS (Completely Fair Scheduler):** Default since Linux 2.6.23.
  - Uses a **Red-Black Tree** (self-balancing BST) ordered by **virtual runtime (vruntime)**.
  - `vruntime += Δtime × (NICE_0_LOAD / task_weight)` — tasks with lower weight get vruntime incremented faster.
  - Always schedules the leftmost node (smallest vruntime) — the task that has run least.
  - **Target latency:** Period within which every runnable task runs at least once (default 6 ms).
  - **Minimum granularity:** Minimum time a task runs to avoid excessive context switches (default 0.75 ms).
- **Real-time scheduling:** `SCHED_FIFO` and `SCHED_RR` for real-time tasks; priorities 1–99.
- **Scheduling classes (priority order):** Stop > Deadline > Real-time > CFS > Idle.

### 12.5 Linux Memory Management

- **Virtual memory** with demand paging.
- **Buddy System:** Physical memory managed in power-of-2 blocks. Allocation/deallocation via combining or splitting buddies.
  - Buddy of a block of size 2^k starting at address x: `buddy = x XOR 2^k`.
- **Slab Allocator:** Kernel object caching; manages `slabs` (contiguous memory containing multiple cache objects). Avoids fragmentation for fixed-size kernel objects.
  - Hierarchy: Cache → Slab → Objects.
- **OOM Killer:** When memory exhausted, kernel kills a process to free memory (scored by `oom_score`).
- **Page Frame Reclamation Algorithm (PFRA):** Based on LRU with active/inactive page lists.
- **Huge Pages (THP):** Support for 2 MB or 1 GB pages; reduces TLB pressure.
- **NUMA support:** Memory allocated near the requesting CPU's node.

### 12.6 Linux File Systems

- **Virtual File System (VFS):** Abstraction layer; uniform interface to multiple file systems.
- **VFS Objects:** Superblock, Inode, Dentry (directory entry cache), File.
- **ext4:** Default Linux file system. Features: journaling, extents, large file/directory support.
  - **Journaling:** Write journal entry before actual write → fast recovery after crash.
  - Journal modes: Writeback (metadata only), Ordered (data before metadata), Journal (both).
- **Proc File System (`/proc`):** Virtual FS; exposes kernel data structures as files. No disk usage.
- **sysfs (`/sys`):** Exposes kernel devices and drivers.
- **tmpfs:** In-memory file system; used for `/tmp`, `/run`.
- **Other supported FS:** XFS, Btrfs, ZFS, NTFS, FAT32, NFS, CIFS.

### 12.7 Linux I/O

- **Block I/O Layer:** Merges and sorts disk requests (I/O elevator). Schedulers: CFQ, Deadline, NOOP, BFQ.
- **Character device interface:** Direct byte-stream I/O.
- **Network I/O:** Socket-based; `sk_buff` structure for network packets.
- **Device drivers:** Kernel modules; divided into block, character, network drivers.

### 12.8 Linux IPC and Networking

**IPC mechanisms:** Pipes, Named Pipes (FIFOs), Message Queues, Semaphores, Shared Memory, Signals, Sockets, D-Bus.

**Network Stack:** BSD socket interface → TCP/IP stack → Network device driver.
- **Netfilter:** Kernel framework for packet filtering; basis of `iptables`/`nftables` firewalls.
- **Network Namespaces:** Isolated network stacks per container.

---

## 13. Windows Operating System

### 13.1 Design Principles

- **Layered architecture** with **microkernel-like** design (actually a hybrid kernel).
- **Portability:** Written mostly in C; architecture-specific code isolated.
- **Security and reliability:** Integrated from design.
- **Object-based:** All resources as objects managed by Object Manager.
- **Compatibility:** POSIX, OS/2 subsystems; Win32 API standard interface.

### 13.2 System Components

| Component | Description |
|---|---|
| **HAL (Hardware Abstraction Layer)** | Isolates OS from hardware differences; portability |
| **Kernel** | Low-level scheduling, interrupt handling, synchronisation, exception dispatching |
| **Executive** | Collection of managers running in kernel mode |
| **Object Manager** | Manages all Windows objects (files, processes, threads, events) |
| **Process Manager** | Creates/terminates processes and threads |
| **Virtual Memory Manager (VMM)** | Paging, virtual address space management |
| **I/O Manager** | I/O requests, device drivers, IRPs (I/O Request Packets) |
| **Security Reference Monitor (SRM)** | Enforces access control; validates access tokens |
| **Cache Manager** | File system cache |
| **Configuration Manager** | Registry management |
| **Local Procedure Call (LPC)** | Inter-process communication within same machine |

**Windows Object:** Has name, handle count, security descriptor, quota charges, reference count. Created by `CreateObject`, accessed via `Handle`.

**Registry:** Centralised hierarchical database for system and application configuration.
- **Hives:** HKEY_LOCAL_MACHINE, HKEY_CURRENT_USER, HKEY_CLASSES_ROOT, HKEY_USERS.

### 13.3 Windows Scheduling

- Priority-based preemptive scheduling; 32 priority levels (0–31).
- **Levels 16–31:** Real-time; not adjusted by OS.
- **Levels 1–15:** Dynamic; OS can boost/reduce based on behaviour.
- **Level 0:** Zero-page thread (zeroes free pages).
- **Priority boost:** After waiting for I/O, foreground window gets boost.

### 13.4 Windows Memory Management

- **Virtual address space per process:** 2 GB user + 2 GB kernel (32-bit); much larger for 64-bit.
- **Page sizes:** 4 KB (default), 2 MB, 1 GB large pages.
- **Working set:** Set of pages in physical memory for a process.
- **VAD (Virtual Address Descriptor):** Tree of reserved virtual memory regions.

### 13.5 Terminal Services and Fast User Switching

- **Terminal Services (Remote Desktop):** Multiple simultaneous user sessions over network; each session isolated.
- **Fast User Switching:** Switch between logged-in users without logging out; sessions preserved.

### 13.6 Windows File System (NTFS)

- **NTFS (New Technology File System):** Default Windows FS.
- **MFT (Master File Table):** Every file/directory has an MFT record; contains all file attributes.
- **Features:** Journaling (log-based), ACLs for fine-grained security, encryption (EFS), compression, hard links, symbolic links, sparse files, disk quotas, file streams.
- **Cluster:** NTFS allocation unit (512 B to 64 KB; default 4 KB).
- **USN Journal (Update Sequence Number):** Tracks changes to files; used by search indexers, backup software.

### 13.7 Windows Networking

- **Architecture:** NDIS (Network Driver Interface Specification) → TDI / WFP → Protocol drivers (TCP/IP) → AFD (Ancillary Function Driver) → Winsock API.
- **Protocols:** TCP/IP, SMB (Server Message Block) for file sharing, RPC.
- **Active Directory:** LDAP-based directory service for user/group/computer management; authentication via Kerberos.
- **Windows Firewall:** Integrated; configurable via GPO (Group Policy Object).

---

## 14. Distributed Systems

### 14.1 Types of Network-Based Operating Systems

| Type | Description |
|---|---|
| **Network OS (NOS)** | Loose coupling; each machine has its own OS; access remote resources explicitly (FTP, NFS) |
| **Distributed OS** | Tight coupling; single coherent OS manages all machines; transparent resource access |
| **Middleware-based** | Layer between OS and applications enabling distributed computing (CORBA, Java RMI, .NET Remoting) |

### 14.2 Network Structure

- **LAN (Local Area Network):** High speed; low latency; single organisation.
- **WAN (Wide Area Network):** Low speed relatively; high latency; geographically dispersed.
- **Communication links:** Dedicated, packet-switched, circuit-switched.
- **Topology:** Bus, Ring, Star, Mesh, Hybrid.

### 14.3 Communication Structure and Protocols

**Naming and Transparency:**
- **Location Transparency:** User need not know where resource is physically located.
- **Migration Transparency:** Resources can move without changing names.
- **Replication Transparency:** Multiple copies of resource managed transparently.

**Communication Primitives:**
- **Message Passing:** `send()` and `receive()`.
- **RPC (Remote Procedure Call):** Transparent procedure call across network.
- **RMI (Remote Method Invocation):** Object-oriented RPC (Java).
- **Sockets:** Low-level; explicit network programming.

**Protocols:** TCP/IP, UDP, HTTP/REST, gRPC, SOAP, AMQP, MQTT.

### 14.4 Robustness

- **Failure Types:** Crash failure, Omission failure (lost message), Timing failure, Byzantine failure (arbitrary incorrect behaviour).
- **Fault Tolerance Techniques:**
  - **Replication:** Keep multiple copies of data/services.
  - **Checkpointing:** Periodically save state; restart from checkpoint on failure.
  - **Message Logging:** Log messages; replay after failure (for deterministic processes).
- **Byzantine Fault Tolerance:** System continues correctly despite arbitrary (including malicious) failures. Requires 3f+1 nodes to tolerate f Byzantine failures.
- **Consensus Algorithms:** Paxos, Raft — ensure all nodes agree on a value despite failures.

### 14.5 Design Issues

| Issue | Description |
|---|---|
| **Transparency** | Hide distribution details (access, location, migration, replication, failure) |
| **Naming** | Naming resources uniquely across distributed system (DNS, UUID) |
| **Scalability** | System remains effective as scale grows; avoid bottlenecks |
| **Consistency** | Keep replicas consistent; CAP theorem constraints |
| **Availability** | System remains operational despite failures |
| **Security** | Authenticate, authorise, encrypt across network |
| **Deadlock** | Distributed deadlock detection across multiple machines |
| **Synchronisation** | Clock synchronisation; logical clocks (Lamport clocks) |

**Lamport Logical Clock:**
- Each event `e` assigned a timestamp `C(e)`.
- **Rules:** 
  - Each process increments its counter before each event: `Ci = Ci + 1`.
  - When process sends message: attach timestamp.
  - When process receives message with timestamp `t`: `Ci = max(Ci, t) + 1`.
- Provides **happened-before** ordering: `a → b ⟹ C(a) < C(b)` (not converse).

**Vector Clocks:**
- Each process maintains a vector of timestamps (one per process).
- **Update:** Increment own component on event.
- **Send:** Include vector; receiver takes componentwise maximum + increments own.
- `V(a) < V(b) ⟺ ∀i: V(a)[i] ≤ V(b)[i] ∧ ∃j: V(a)[j] < V(b)[j]`
- Can detect concurrent events (neither happened-before the other).

**CAP Theorem:** A distributed system can simultaneously guarantee at most 2 of:
- **Consistency (C):** Every read gets most recent write.
- **Availability (A):** Every request gets a response.
- **Partition Tolerance (P):** System continues despite network partition.

### 14.6 Distributed File Systems (DFS)

- Files accessible from any node in the distributed system; location transparent.

| System | Description |
|---|---|
| **NFS (Network File System)** | Sun/Unix; stateless server; RPC-based; vnode interface |
| **AFS (Andrew File System)** | Scalable; client-side caching with callbacks; whole-file caching |
| **Coda** | Supports disconnected operation; conflict resolution |
| **GFS (Google File System)** | Large files; fault-tolerant; single master; 64 MB chunks |
| **HDFS** | Based on GFS; for MapReduce; NameNode + DataNodes |
| **Lustre** | High-performance computing; parallel access |

**NFS Architecture:**
- **VFS layer** provides abstraction; NFS implemented as VFS module.
- **Stateless:** Server does not maintain client state; each request self-contained → easy recovery.
- **Mount protocol:** Client mounts remote directory at local mount point.
- **Client-side caching:** Cached data validated via **attribute cache** (checks file modification time).

**DFS Design Goals:**
- Transparency (access, location, migration, replication, concurrency, failure).
- Scalability, performance, fault tolerance, heterogeneity.

---

## Quick Recap Table

| Topic | Key Concepts / Formulas |
|---|---|
| Compilers vs Interpreters | Compiler: whole program; Interpreter: line by line |
| Loading | Absolute, Relocatable, Dynamic loading |
| Two-pass Assembler | Pass 1: Symbol table; Pass 2: Code generation |
| Process States | New → Ready → Running → Waiting → Terminated |
| fork() | Returns child PID to parent; 0 to child |
| Peterson's Solution | flag[] + turn variable; 2-process mutual exclusion |
| Semaphore | wait(): S--; block if S<0; signal(): S++; wake if S≤0 |
| Amdahl's Law | `S ≤ 1/(f + (1-f)/P)` |
| CPU Burst Prediction | `τₙ₊₁ = α·tₙ + (1-α)·τₙ` |
| Banker's Safety | Find safe sequence: Work ≥ Need[i]; Work += Alloc[i] |
| TLB EAT | `EAT = (2 - α) × tm` where α = hit ratio |
| Page Fault EAT | `EAT = (1-p)·tm + p·page_fault_time` |
| Proportional Allocation | `aᵢ = (sᵢ/Σsⱼ) × m` |
| RM Utilisation Bound | `U ≤ n(2^(1/n) - 1)`; approaches `ln2 ≈ 0.693` |
| EDF | Optimal preemptive; `Σ(Cᵢ/Tᵢ) ≤ 1` |
| Unix inode max file size | ~4 TB (12 direct + 1-indirect + 2-indirect + 3-indirect) |
| RAID 5 Parity | `P = D₀ XOR D₁ XOR D₂ ...`; distributed across disks |
| Linux CFS | Red-black tree on vruntime; always schedule leftmost node |
| Linux Buddy System | Block size = 2^k; buddy = addr XOR 2^k |
| Lamport Clock | `Ci = max(Ci, t) + 1` on receive |
| CAP Theorem | At most 2 of: Consistency, Availability, Partition Tolerance |
| Byzantine Tolerance | Requires `3f+1` nodes to tolerate `f` failures |
| Deadlock Conditions | ME + Hold&Wait + No Preemption + Circular Wait |
| Banker's Need | `Need[i][j] = Max[i][j] - Allocation[i][j]` |
| Wait-for Graph | Cycle → Deadlock (single resource instances) |

---


