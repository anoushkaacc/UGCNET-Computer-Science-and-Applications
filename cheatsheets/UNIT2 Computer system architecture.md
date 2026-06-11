
# UGC NET – Unit 2: Computer System Architecture
---
## 1. Digital Logic Circuits and Components

### 1.1 Logic Gates

**Basic Gates:**

| Gate | Symbol | Boolean Expression | Truth Table (A, B → Y) |
|---|---|---|---|
| AND | A·B | Y = A·B | 00→0, 01→0, 10→0, 11→1 |
| OR | A+B | Y = A+B | 00→0, 01→1, 10→1, 11→1 |
| NOT | A' | Y = A' | 0→1, 1→0 |
| NAND | (A·B)' | Y = (A·B)' | 00→1, 01→1, 10→1, 11→0 |
| NOR | (A+B)' | Y = (A+B)' | 00→1, 01→0, 10→0, 11→0 |
| XOR | A⊕B | Y = A'B + AB' | 00→0, 01→1, 10→1, 11→0 |
| XNOR | (A⊕B)' | Y = AB + A'B' | 00→1, 01→0, 10→0, 11→1 |

- **NAND and NOR** are universal gates — any Boolean function can be implemented using only NAND or only NOR gates.
- **XOR properties:** `A⊕0=A`, `A⊕1=A'`, `A⊕A=0`, `A⊕A'=1`, commutative and associative.

### 1.2 Boolean Algebra

**Postulates and Theorems:**

| Law | AND form | OR form |
|---|---|---|
| Identity | A·1 = A | A+0 = A |
| Null (Domination) | A·0 = 0 | A+1 = 1 |
| Idempotent | A·A = A | A+A = A |
| Complement | A·A' = 0 | A+A' = 1 |
| Involution | (A')' = A | — |
| Commutative | A·B = B·A | A+B = B+A |
| Associative | (A·B)·C = A·(B·C) | (A+B)+C = A+(B+C) |
| Distributive | A·(B+C) = AB+AC | A+(B·C) = (A+B)(A+C) |
| Absorption | A·(A+B) = A | A+(A·B) = A |
| De Morgan's | (A·B)' = A'+B' | (A+B)' = A'·B' |
| Consensus | AB+A'C+BC = AB+A'C | (A+B)(A'+C)(B+C) = (A+B)(A'+C) |

### 1.3 Map Simplifications (Karnaugh Map)

- **K-map** is a graphical method to minimise Boolean expressions.
- Adjacent cells differ by exactly one variable (Gray code ordering).
- Group cells of 1s (SOP) or 0s (POS) in powers of 2: 1, 2, 4, 8, 16.
- Wrapping around edges is allowed.

**Rules:**
- Groups must be of size 2^k (1, 2, 4, 8, ...).
- Each group should be as large as possible.
- Fewer groups → fewer product terms.
- **Prime Implicant (PI):** Largest possible group of 1s.
- **Essential PI:** Covers at least one minterm not covered by any other PI.

**Don't Care conditions (X):** Can be treated as 0 or 1 to form larger groups.

**2-variable K-map:**
```
     B' B
A'  | 0 | 1 |
A   | 2 | 3 |
```

**3-variable K-map:**
```
     BC
A  | 00 | 01 | 11 | 10 |
A' |    |    |    |    |
A  |    |    |    |    |
```

**4-variable K-map:**
```
      CD
AB  | 00 | 01 | 11 | 10 |
00  |  0 |  1 |  3 |  2 |
01  |  4 |  5 |  7 |  6 |
11  | 12 | 13 | 15 | 14 |
10  |  8 |  9 | 11 | 10 |
```

**Quine-McCluskey Method:** Tabular minimisation; used when number of variables is large (>4); finds all prime implicants systematically.

### 1.4 Combinational Circuits

- Output depends only on current inputs (no memory).

**Half Adder:**
- Inputs: A, B. Outputs: Sum S, Carry C.
- `S = A ⊕ B` ; `C = A · B`

**Full Adder:**
- Inputs: A, B, Cin. Outputs: Sum S, Carry Cout.
- `S = A ⊕ B ⊕ Cin`
- `Cout = AB + Cin(A ⊕ B) = AB + BCin + ACin`

**Ripple Carry Adder:** Chain of n full adders; simple but slow (carry ripples through all stages).
- **Delay:** `tRCA = n × tFA`

**Carry Lookahead Adder (CLA):**
- Generate: `Gᵢ = AᵢBᵢ` (carry generated at stage i regardless of Cin)
- Propagate: `Pᵢ = Aᵢ ⊕ Bᵢ` (carry propagated through stage i)
- `Cᵢ₊₁ = Gᵢ + PᵢCᵢ`
- `C₁ = G₀ + P₀C₀`
- `C₂ = G₁ + P₁G₀ + P₁P₀C₀`
- `C₃ = G₂ + P₂G₁ + P₂P₁G₀ + P₂P₁P₀C₀`
- All carries computed in parallel → O(1) delay (hardware-limited).

**Half Subtractor:** `D = A ⊕ B` ; `Borrow = A'B`
**Full Subtractor:** `D = A ⊕ B ⊕ Bin` ; `Bout = A'B + A'Bin + BBin`

**Comparator:** Compares two n-bit numbers. For 1-bit: `A>B = AB'`, `A<B = A'B`, `A=B = XNOR(A,B)`.

**Parity Generator/Checker:** 
- Even parity bit = XOR of all data bits.
- Odd parity bit = (XOR of all data bits)'.

### 1.5 Flip-Flops (Sequential Basic Elements)

- **Flip-flop:** Bistable device; stores one bit; changes state on clock edge.

**SR Flip-Flop:**
| S | R | Q(next) |
|---|---|---|
| 0 | 0 | Q (no change) |
| 0 | 1 | 0 (reset) |
| 1 | 0 | 1 (set) |
| 1 | 1 | X (invalid/forbidden) |

**D Flip-Flop (Data/Delay):**
- `Q(next) = D`
- Eliminates invalid state of SR; most commonly used.
- Stores input D on clock edge.

**JK Flip-Flop:**
| J | K | Q(next) |
|---|---|---|
| 0 | 0 | Q (no change) |
| 0 | 1 | 0 (reset) |
| 1 | 0 | 1 (set) |
| 1 | 1 | Q' (toggle) |

- `Q(next) = JQ' + K'Q`
- No invalid state; most versatile.

**T Flip-Flop (Toggle):**
| T | Q(next) |
|---|---|
| 0 | Q (no change) |
| 1 | Q' (toggle) |

- `Q(next) = T ⊕ Q = TQ' + T'Q`
- Built from JK with J=K=T.

**Flip-Flop Conversions:** Using excitation tables.

**JK from D:** `J = D`, `K = D'`
**D from JK:** `D = JQ' + K'Q`
**T from JK:** `T = J = K`
**D from T:** `D = T ⊕ Q`

**Excitation Tables:**

| Q→Q(next) | D needed | J needed | K needed | T needed |
|---|---|---|---|---|
| 0→0 | 0 | 0 | X | 0 |
| 0→1 | 1 | 1 | X | 1 |
| 1→0 | 0 | X | 1 | 1 |
| 1→1 | 1 | X | 0 | 0 |

**Triggering:**
- **Level Triggered (Latch):** Transparent when clock is at a level (high or low).
- **Edge Triggered:** Changes state only on rising or falling clock edge.
- **Master-Slave:** Two latches; first (master) captures on one level, second (slave) transfers on other edge.

**Setup Time (tsu):** D must be stable before clock edge.
**Hold Time (th):** D must remain stable after clock edge.
**Propagation Delay (tp):** Time from clock edge to stable output.
**Maximum Clock Frequency:** `f_max = 1 / (tsu + tp)`

### 1.6 Sequential Circuits

- Output depends on current inputs AND stored state.
- **Mealy Machine:** Output depends on current state AND current input.
- **Moore Machine:** Output depends only on current state.

**Design Steps:**
1. Derive state diagram from problem description.
2. Encode states as binary (state assignment).
3. Derive state table (next state and output for each state/input combination).
4. Derive flip-flop excitation expressions using excitation tables.
5. Implement with logic gates.

**State Reduction:** Merge equivalent states (same output, same next state transitions for all inputs) using implication table or partitioning method.

### 1.7 Integrated Circuits

| Scale | Abbreviation | Gate Count | Example |
|---|---|---|---|
| Small Scale | SSI | < 10 gates | Basic gates, flip-flops |
| Medium Scale | MSI | 10–100 gates | Adders, MUX, decoders |
| Large Scale | LSI | 100–1000 gates | Small memories, ALU |
| Very Large Scale | VLSI | 1000–1M gates | Microprocessors |
| Ultra Large Scale | ULSI | > 1M gates | Modern CPUs, GPUs |

**Families:** TTL (Transistor-Transistor Logic) — 5V, fast; CMOS — low power, high density; ECL — fastest, high power.

### 1.8 Decoders

- n inputs → 2ⁿ outputs; exactly one output active for each input combination.
- **2-to-4 decoder:** 2 inputs (A, B), 4 outputs (D₀–D₃).
  - `D₀ = A'B'`, `D₁ = A'B`, `D₂ = AB'`, `D₃ = AB`
- **3-to-8 decoder:** 3 inputs → 8 outputs (minterm generator).
- With enable input: active only when Enable = 1.
- **Implementing Boolean functions:** Connect decoder outputs corresponding to minterms to OR gate.

**Encoder:** Reverse of decoder; 2ⁿ inputs → n outputs. Produces binary code for which input is active.
- **Priority Encoder:** If multiple inputs active, outputs code for highest-priority (usually highest-numbered) input.

### 1.9 Multiplexers (MUX)

- Data selector; 2ⁿ data inputs, n select inputs, 1 output.
- `Y = selected input based on select lines`

**4-to-1 MUX (2 select lines S₁, S₀):**
`Y = S₁'S₀'I₀ + S₁'S₀I₁ + S₁S₀'I₂ + S₁S₀I₃`

**MUX as Universal Logic:** 2ⁿ-to-1 MUX can implement any n-variable Boolean function (connect select to variables; data inputs = 0 or 1 based on truth table).

**With one extra variable:** (2^(n-1))-to-1 MUX can implement n-variable function by connecting function of last variable to data inputs.

**Demultiplexer (DEMUX):** Reverse of MUX; 1 input → 2ⁿ outputs; routes input to one of 2ⁿ output lines (same circuit as decoder with enable).

### 1.10 Registers and Counters

**Registers:**
- n flip-flops storing n bits.
- **Parallel Load Register:** All bits loaded simultaneously.
- **Shift Register:** Bits shifted left or right by one position per clock.
  - SISO (Serial In, Serial Out), SIPO, PISO, PIPO.
- **Universal Shift Register:** Can shift left, shift right, parallel load, or hold. Controlled by 2-bit mode input.
- **Applications:** Serial-to-parallel conversion, delay, ring counter, sequence detection.

**Counters:**
- **Ripple (Asynchronous) Counter:** Each FF clocked by output of previous; simple but slow (ripple delay).
  - n-bit ripple counter: counts 0 to 2ⁿ−1; frequency of last FF output = f_clk / 2ⁿ.
- **Synchronous Counter:** All FFs clocked simultaneously; faster; more complex logic.
- **Up/Down Counter:** Can count in both directions.
- **Modulo-n Counter (MOD-n):** Counts from 0 to n-1; resets to 0 after reaching n-1.
  - Need `⌈log₂n⌉` flip-flops.
  - For MOD-6: 3 FFs (2³=8 states); reset at count 6 (or 5+1).
- **Ring Counter:** Single 1 circulating through n FFs; n states (not 2ⁿ); self-decoding.
- **Johnson (Twisted Ring) Counter:** Complement of serial output fed back; 2n states for n FFs.
- **BCD Counter (MOD-10):** Counts 0000–1001; resets at 1010.

### 1.11 Memory Unit

**Basic Memory Terms:**
- **Address:** Unique binary code for each memory location.
- **Word:** Unit of data transferred in one memory access.
- **Memory capacity:** `2^k × n` where k = address lines, n = word size (bits).

**Types:**
| Type | Access | Volatility | Use |
|---|---|---|---|
| **RAM (SRAM)** | Random | Volatile | Cache |
| **RAM (DRAM)** | Random | Volatile | Main memory |
| **ROM** | Random (read only) | Non-volatile | Firmware, BIOS |
| **PROM** | Programmed once | Non-volatile | — |
| **EPROM** | Erasable (UV light) | Non-volatile | — |
| **EEPROM** | Electrically erasable | Non-volatile | — |
| **Flash** | Block erase | Non-volatile | USB, SSD |

**SRAM:** Uses 6 transistors per cell; fast; expensive; used in cache.
**DRAM:** Uses 1 transistor + 1 capacitor per cell; needs periodic refresh; slower; cheap; used in main memory.
**DRAM Refresh:** Must refresh every few ms to prevent data loss (capacitor discharge).

---

## 2. Data Representation

### 2.1 Number Systems and Conversion

| System | Base | Digits |
|---|---|---|
| Binary | 2 | 0, 1 |
| Octal | 8 | 0–7 |
| Decimal | 10 | 0–9 |
| Hexadecimal | 16 | 0–9, A–F |

**Positional Notation:** `N = Σ dᵢ × rⁱ` where dᵢ = digit, r = radix, i = position.

**Conversion Methods:**

**Any base → Decimal:** Multiply each digit by its positional weight and sum.
- `(1011.01)₂ = 1×2³ + 0×2² + 1×2¹ + 1×2⁰ + 0×2⁻¹ + 1×2⁻² = 8+0+2+1+0+0.25 = 11.25`

**Decimal → Binary (integer part):** Repeated division by 2; remainders read bottom to top.
**Decimal → Binary (fractional part):** Repeated multiplication by 2; integer parts read top to bottom.

**Binary ↔ Octal:** Group binary digits in groups of 3 (right to left for integer, left to right for fraction).
- `(110 101 011)₂ = (653)₈`

**Binary ↔ Hexadecimal:** Group binary digits in groups of 4.
- `(1010 1111)₂ = (AF)₁₆`

**Conversion Table:**

| Decimal | Binary | Octal | Hex |
|---|---|---|---|
| 0 | 0000 | 0 | 0 |
| 8 | 1000 | 10 | 8 |
| 10 | 1010 | 12 | A |
| 15 | 1111 | 17 | F |
| 16 | 10000 | 20 | 10 |

### 2.2 Complements

**r's Complement:** `N_r = rⁿ − N` (for n-digit number N in base r).
**(r-1)'s Complement:** `N_(r-1) = (rⁿ − 1) − N`

**For Binary:**
- **1's Complement:** Flip every bit. `(1011)₂ → (0100)₂`
- **2's Complement:** 1's complement + 1. `(1011)₂ → (0100+1)₂ = (0101)₂`
  - Alternative: Copy bits from right up to and including first 1; flip all remaining bits.
- **Special case:** `-0` does not exist in 2's complement; `10...0` represents the most negative number.

**For Decimal:**
- **9's Complement** of 546 (3-digit): 999 − 546 = 453.
- **10's Complement** of 546: 1000 − 546 = 454 = 453 + 1.

### 2.3 Fixed-Point Representation

**Sign-Magnitude:** MSB = sign bit (0=positive, 1=negative); remaining bits = magnitude.
- Drawback: Two representations for zero (+0 and -0); subtraction requires sign comparison.
- Range: `−(2^(n-1) − 1)` to `+(2^(n-1) − 1)` for n-bit.

**1's Complement:**
- Range: `−(2^(n-1) − 1)` to `+(2^(n-1) − 1)`; two zeros.
- Subtraction: Add 1's complement; if carry out of MSB → add carry back to result (end-around carry).

**2's Complement (most common):**
- Range: `−2^(n-1)` to `+(2^(n-1) − 1)` for n-bit number.
  - 8-bit: -128 to +127; 16-bit: -32768 to +32767; 32-bit: -2,147,483,648 to +2,147,483,647
- One unique representation of zero.
- Subtraction: Add 2's complement of subtrahend; ignore final carry out.
- **Overflow:** Occurs when result exceeds representable range.
  - Detection: Overflow iff carry into MSB ≠ carry out of MSB.
  - Or: Overflow iff two operands have same sign but result has different sign.

**n-bit 2's complement arithmetic:**
- `A − B = A + (2^n − B) = A + B̄ + 1` (where B̄ is 1's complement of B)

### 2.4 Floating-Point Representation

**General Form:** `N = ±M × r^E`
where M = mantissa (significand), E = exponent, r = radix.

**IEEE 754 Standard:**

| Format | Total bits | Sign | Exponent | Mantissa | Bias |
|---|---|---|---|---|---|
| Single Precision | 32 | 1 | 8 | 23 | 127 |
| Double Precision | 64 | 1 | 11 | 52 | 1023 |
| Extended | 80 | 1 | 15 | 64 | 16383 |

**Encoding:**
```
[Sign (1 bit)] [Biased Exponent (8 bits)] [Mantissa (23 bits)]
```

**Biased Exponent:** `E_stored = E_actual + Bias`
- Single: Bias = 127; stored exponent range 1–254 (0 and 255 reserved).
- Double: Bias = 1023.

**Normalised Form:** `1.mantissa × 2^exponent` (hidden/implicit leading 1 bit for IEEE 754).

**Value:** `(-1)^S × (1.M) × 2^(E_stored - Bias)`

**Special Values (IEEE 754 Single):**

| E_stored | Mantissa | Value |
|---|---|---|
| 0 | 0 | ±0 |
| 0 | ≠ 0 | Denormalised (subnormal): `(-1)^S × 0.M × 2^(-126)` |
| 255 | 0 | ±∞ |
| 255 | ≠ 0 | NaN (Not a Number) |
| 1–254 | any | Normal: `(-1)^S × 1.M × 2^(E-127)` |

**Range:**
- Single: approximately ±1.2 × 10⁻³⁸ to ±3.4 × 10³⁸
- Double: approximately ±2.2 × 10⁻³⁰⁸ to ±1.8 × 10³⁰⁸

**Precision:**
- Single: ~7 significant decimal digits
- Double: ~15-16 significant decimal digits

**Example:** Convert -6.25 to IEEE 754 Single:
1. Sign = 1 (negative)
2. `6.25 = 110.01₂ = 1.1001 × 2²`
3. Biased exponent = 2 + 127 = 129 = `10000001₂`
4. Mantissa = `10010000000000000000000`
5. Result: `1 10000001 10010000000000000000000`

**Floating-Point Arithmetic Issues:**
- **Round-off error:** Result not exactly representable.
- **Truncation:** Drop extra bits.
- **Rounding:** Round to nearest (default), round toward zero, round up, round down.
- **Overflow/Underflow:** Result outside representable range.
- **Catastrophic cancellation:** Loss of significant digits when subtracting nearly equal numbers.

### 2.5 Error Detection Codes

**Parity Bit:**
- **Even parity:** Bit appended so total number of 1s is even.
- **Odd parity:** Total number of 1s is odd.
- Detects single-bit errors (any odd number of errors); cannot detect 2-bit errors.

**Hamming Code:**
- **Error-correcting code** for single-bit correction (SECDED = Single Error Correction, Double Error Detection).
- **Parity bit positions:** Powers of 2: p₁=2⁰, p₂=2¹, p₃=2², p₄=2³, ...
- For m data bits: need r parity bits where `2^r ≥ m + r + 1`.

| Data bits m | Parity bits r | Total bits n |
|---|---|---|
| 1 | 2 | 3 |
| 2–4 | 3 | 5–7 |
| 5–11 | 4 | 9–15 |
| 12–26 | 5 | 17–31 |

- **Parity bit pᵢ** checks all positions whose binary representation has bit i set.
- **Error detection:** Compute syndrome (XOR of relevant parity bits); if non-zero, syndrome = position of error.

**Example — Hamming(7,4):**
- 4 data bits (d₁d₂d₃d₄), 3 parity bits (p₁p₂p₃) at positions 1, 2, 4.
- p₁ covers positions 1, 3, 5, 7 (bit 0 set).
- p₂ covers positions 2, 3, 6, 7 (bit 1 set).
- p₃ covers positions 4, 5, 6, 7 (bit 2 set).
- Syndrome = concatenation of parity check results = error position.

**Checksum:** Sum of data words; transmitted with data; receiver checks sum.

**CRC (Cyclic Redundancy Check):** Polynomial division; generator polynomial used to compute remainder; powerful burst error detection. (See Unit 9 notes for full detail.)

**BCD (Binary Coded Decimal):** Each decimal digit represented by 4-bit binary.
- 8421 BCD: standard; 0→0000, 9→1001 (1010–1111 invalid).
- **Excess-3 Code:** BCD + 3; self-complementing (9's complement by bitwise NOT).
- **Gray Code:** Successive values differ by exactly 1 bit; used in shaft encoders.

### 2.6 Computer Arithmetic

#### Addition and Subtraction

**Binary Addition:** `0+0=0`, `0+1=1`, `1+0=1`, `1+1=0` (carry 1).

**2's Complement Subtraction:** `A − B = A + (−B) = A + B̄ + 1`
- If carry out of MSB: ignore carry (result is correct).
- **Overflow detection:** `V = Cₙ ⊕ Cₙ₋₁` (carry into MSB XOR carry out of MSB).

#### Multiplication Algorithms

**Unsigned Binary Multiplication (Shift-and-Add):**
```
Product = 0
For each bit of multiplier (LSB to MSB):
    If bit = 1: Product = Product + (Multiplicand shifted left by bit position)
    If bit = 0: no addition (just shift)
```
- n × n bit multiplication → up to 2n-bit product.

**Booth's Algorithm (Signed Multiplication):**
- Handles both positive and negative numbers in 2's complement.
- Examine current bit and previous bit of multiplier:

| Q[0] | Q[-1] | Operation |
|---|---|---|
| 0 | 0 | Shift only (no change) |
| 0 | 1 | Add multiplicand; then shift |
| 1 | 0 | Subtract multiplicand; then shift |
| 1 | 1 | Shift only (no change) |

- After each step: arithmetic right shift (A, Q, Q₋₁).
- Advantage: Works correctly for negative numbers; fewer additions if there are long runs of 1s.

**Modified Booth's Algorithm (Radix-4 Booth):**
- Examines 3 bits at a time; halves the number of partial products.
- Multiplier recoding: each 3-bit group maps to {−2M, −M, 0, M, 2M}.

**Array Multiplier:** Combinational; generates all partial products simultaneously and sums them.
- n×n array multiplier: n(n-2) full adders + n half adders; delay = O(n).

**Wallace Tree Multiplier:** Reduces partial products using CSA (Carry-Save Adder) tree; faster — O(log n) delay.

#### Division Algorithms

**Restoring Division:**
```
Remainder R = Dividend
For each step (n steps for n-bit divisor):
    Left shift R by 1
    R = R − Divisor
    If R < 0: Quotient bit = 0; Restore: R = R + Divisor
    If R ≥ 0: Quotient bit = 1
```

**Non-Restoring Division:**
- Avoids restoration step; uses condition of previous remainder.
```
If R < 0: Q_bit = 0; R = 2R + Divisor (instead of restore + subtract)
If R ≥ 0: Q_bit = 1; R = 2R − Divisor
```
- Final correction: if remainder negative, add divisor.

**Division by 2:** Right shift (unsigned) or arithmetic right shift (signed).

**Floating-Point Operations:**
- **Addition/Subtraction:** Align exponents (shift smaller mantissa right) → operate on mantissas → normalise result → round.
- **Multiplication:** Add exponents (subtract bias once), multiply mantissas, normalise.
  - `E_result = E₁ + E₂ − Bias`
  - `M_result = M₁ × M₂`
- **Division:** Subtract exponents (add bias), divide mantissas, normalise.
  - `E_result = E₁ − E₂ + Bias`
  - `M_result = M₁ / M₂`

---

## 3. Register Transfer and Microoperations

### 3.1 Register Transfer Language (RTL)

- Symbolic notation to describe microoperations.
- **Register:** Denoted by capital letters: `MAR`, `MBR`, `PC`, `AC`, `IR`.
- **Transfer:** `R2 ← R1` (contents of R1 copied to R2).
- **Conditional Transfer:** `P: R2 ← R1` (transfer only if control signal P = 1).
- **Simultaneous:** Separated by commas: `R2 ← R1, R1 ← R2` (occurs simultaneously if hardware supports).
- **Bit fields:** `R2[7:0]` = lower 8 bits of R2.

### 3.2 Bus and Memory Transfers

**Common Bus:**
- A set of wires shared by multiple registers.
- Only one register can place data on bus at a time (controlled by multiplexers or tri-state buffers).
- **Three-state buffer:** Output = input (if enable=1), high-impedance Z (if enable=0).
- `BUS ← R1` then `R2 ← BUS` (two-step transfer via bus).

**Memory Transfers:**
- `MAR` = Memory Address Register (holds address).
- `MBR/MDR` = Memory Buffer/Data Register (holds data).
- **Read:** `MAR ← address ; MBR ← M[MAR]` (memory read, takes several clock cycles).
- **Write:** `MAR ← address ; MBR ← data ; M[MAR] ← MBR`.
- Read operation denoted: `Read: MBR ← M[MAR]`
- Write operation: `Write: M[MAR] ← MBR`

### 3.3 Arithmetic Microoperations

| Microoperation | RTL Notation | Description |
|---|---|---|
| Add | `R3 ← R1 + R2` | Binary addition |
| Add with carry | `R3 ← R1 + R2 + Cin` | — |
| Subtract (2's comp) | `R3 ← R1 + R2' + 1` | — |
| Increment | `R1 ← R1 + 1` | — |
| Decrement | `R1 ← R1 - 1` | — |
| Negate | `R1 ← R1' + 1` | 2's complement |
| Transfer | `R2 ← R1` | No change |

### 3.4 Logic Microoperations

| Operation | RTL | Description |
|---|---|---|
| AND | `R1 ← R1 ∧ R2` | Bitwise AND; used to clear bits (masking) |
| OR | `R1 ← R1 ∨ R2` | Bitwise OR; used to set bits |
| XOR | `R1 ← R1 ⊕ R2` | Bitwise XOR; used to complement bits |
| Complement | `R1 ← R1'` | Bitwise NOT |

**Applications:**
- **Selective complement:** XOR with mask (1s at positions to complement).
- **Selective set:** OR with mask.
- **Selective clear:** AND with complement of mask.
- **Mask (clear to 0):** AND with mask (0s at positions to clear).
- **Insert:** AND to clear, then OR to set bits.

### 3.5 Shift Microoperations

| Operation | RTL | Description |
|---|---|---|
| Logical Shift Left | `R ← shl R` | Shift left; fill 0 from right; MSB to carry |
| Logical Shift Right | `R ← shr R` | Shift right; fill 0 from left; LSB to carry |
| Arithmetic Shift Left | `R ← ashl R` | Same as logical; sign-extension not needed |
| Arithmetic Shift Right | `R ← ashr R` | Shift right; replicate sign bit (MSB) |
| Rotate Left | `R ← rol R` | Shift left; MSB wraps to LSB |
| Rotate Right | `R ← ror R` | Shift right; LSB wraps to MSB |
| Rotate Left through Carry | — | MSB → Carry; old Carry → LSB |
| Rotate Right through Carry | — | LSB → Carry; old Carry → MSB |

**ALU (Arithmetic Logic Unit):**
- Performs all arithmetic and logic microoperations.
- Inputs: Data (A, B), Function select (S), Carry in (Cin).
- Outputs: Result (F), Status flags (Carry, Zero, Sign, Overflow).

---

## 4. Basic Computer Organization and Design

### 4.1 Stored Program Concept

- Both program instructions and data stored in the same memory.
- **Von Neumann Architecture:** Single memory for data and instructions; sequential execution.
- **Harvard Architecture:** Separate instruction and data memory; allows simultaneous fetch.
- **Instruction:** Specifies operation (opcode) and operands (addresses).

### 4.2 Instruction Codes

**Instruction Format (Basic Computer — 16-bit):**
```
[Mode (1 bit)] [Opcode (3 bits)] [Address (12 bits)]
```
- Mode bit 0: Direct addressing (address = effective address).
- Mode bit 1: Indirect addressing (address field contains address of effective address).
- **Effective Address (EA):**
  - Direct: `EA = address field`
  - Indirect: `EA = M[address field]`

### 4.3 Computer Registers (Basic Computer)

| Register | Symbol | Bits | Function |
|---|---|---|---|
| Data Register | DR | 16 | Temporary data storage |
| Accumulator | AC | 16 | ALU output, main working register |
| Instruction Register | IR | 16 | Current instruction |
| Temporary Register | TR | 16 | Temporary storage |
| Memory Address Register | MAR | 12 | Address sent to memory |
| Memory Buffer Register | MBR/MBR | 16 | Data to/from memory |
| Program Counter | PC | 12 | Address of next instruction |
| Input Register | INPR | 8 | Data from input device |
| Output Register | OUTR | 8 | Data to output device |

**Flip-flops:** IEN (interrupt enable), FGI (input flag), FGO (output flag), R (interrupt request), S (start/stop), E (carry), HALT.

### 4.4 Computer Instructions (Basic Computer)

**Memory-Reference Instructions (opcode 000–110, mode bit matters):**

| Mnemonic | Opcode | Operation |
|---|---|---|
| AND | 000 | `AC ← AC ∧ M[EA]` |
| ADD | 001 | `AC ← AC + M[EA]; E ← carry` |
| LDA | 010 | `AC ← M[EA]` (Load) |
| STA | 011 | `M[EA] ← AC` (Store) |
| BUN | 100 | `PC ← EA` (Branch Unconditional) |
| BSA | 101 | `M[EA] ← PC; PC ← EA+1` (Branch and Save Return) |
| ISZ | 110 | `M[EA] ← M[EA]+1; if M[EA]=0: PC ← PC+1` (Increment and Skip if Zero) |

**Register-Reference Instructions (opcode = 111, mode = 0):** Operate on AC or PC.

| Mnemonic | Hex | Operation |
|---|---|---|
| CLA | 7800 | `AC ← 0` |
| CLE | 7400 | `E ← 0` |
| CMA | 7200 | `AC ← AC'` |
| CME | 7100 | `E ← E'` |
| CIR | 7080 | Circular shift right `AC` and `E` |
| CIL | 7040 | Circular shift left `AC` and `E` |
| INC | 7020 | `AC ← AC + 1` |
| SPA | 7010 | Skip if `AC > 0` (positive) |
| SNA | 7008 | Skip if `AC < 0` (negative, MSB=1) |
| SZA | 7004 | Skip if `AC = 0` |
| SZE | 7002 | Skip if `E = 0` |
| HLT | 7001 | `S ← 0` (Halt) |

**Input-Output Instructions (opcode = 111, mode = 1):**

| Mnemonic | Operation |
|---|---|
| INP | `AC(0-7) ← INPR; FGI ← 0` |
| OUT | `OUTR ← AC(0-7); FGO ← 0` |
| SKI | Skip if FGI = 1 |
| SKO | Skip if FGO = 1 |
| ION | `IEN ← 1` (enable interrupts) |
| IOF | `IEN ← 0` (disable interrupts) |

### 4.5 Timing and Control

**Timing Signal:** Generated by a counter (SC) incremented every clock cycle. Produces timing pulses T₀, T₁, T₂, ... T₁₅.

**Control Unit Types:**
- **Hardwired Control:** Logic gates and flip-flops directly implement control signals; fast but inflexible.
- **Microprogrammed Control:** Control signals generated from microprogram stored in control memory; flexible but slower.

**Instruction Cycle Timing:**

| Time | Fetch Cycle Operation |
|---|---|
| T₀ | `MAR ← PC` |
| T₁ | `MBR ← M[MAR]; PC ← PC + 1` |
| T₂ | `IR ← MBR` |

After T₂, decode IR and execute.

**SC Reset:** `SC ← 0` when instruction completes (HLT or after execute phase).

### 4.6 Instruction Cycle

```
FETCH: 
    MAR ← PC
    MBR ← M[MAR]; PC ← PC + 1
    IR ← MBR

DECODE:
    Decode IR[14:12] (opcode), IR[15] (mode bit)
    If IR[14:12] = 111: register-reference or I/O instruction
    Else: memory-reference instruction; determine EA

INDIRECT (if mode=1):
    MAR ← IR[11:0]
    MBR ← M[MAR]
    EA ← MBR

EXECUTE:
    Perform operation based on opcode

INTERRUPT CHECK:
    If IEN = 1 and (FGI = 1 or FGO = 1):
        R ← 1
        BUN to interrupt service routine
```

### 4.7 Memory-Reference Instruction Execution

**Example — ADD (direct):**
```
T₀: MAR ← PC
T₁: MBR ← M[MAR]; PC ← PC + 1
T₂: IR ← MBR; SC ← 0 (after decode + execute)
T₄ (EA exists): MAR ← EA
T₅: MBR ← M[MAR]
T₆: AC ← AC + MBR; E ← carry; SC ← 0
```

**BSA (Branch and Save Address):**
```
T₄: MAR ← IR[11:0]; MBR ← PC
T₅: M[MAR] ← MBR; AR ← IR[11:0] + 1
T₆: PC ← AR; SC ← 0
```
(Used to implement subroutines in the basic computer.)

### 4.8 Interrupt Handling

- When `R = 1` (interrupt request): at end of current instruction.
```
T₀: MAR ← 0; MBR ← PC    (save PC at address 0)
T₁: M[MAR] ← MBR; PC ← 1 (PC set to address 1 = ISR start)
T₂: IEN ← 0; R ← 0; SC ← 0 (disable further interrupts)
```
- **ISR:** Saves AC and other registers, services I/O, restores registers, enables interrupts, executes indirect BUN to M[0] (returns to interrupted program).

---

## 5. Programming the Basic Computer

### 5.1 Machine Language

- Program expressed as binary (or hex) sequences of instruction codes.
- **Absolute machine language:** Addresses are absolute memory locations.
- **Disadvantages:** Not human-readable; tedious; error-prone.

### 5.2 Assembly Language

- Symbolic representation; one-to-one with machine instructions.
- **Fields of an assembly language statement:**
  ```
  [Label,]  Mnemonic  [Operand]  [/Comment]
  ```
- **Pseudo-instructions (assembler directives):**
  - `ORG n`: Set program counter to n (origin).
  - `END`: End of program.
  - `DEC n`: Decimal constant.
  - `HEX n`: Hexadecimal constant.
  - `BSS n`: Reserve n words of memory (block storage start).

### 5.3 Assembler

- Translates assembly language to machine language.
- **Two-pass assembler:**
  - **Pass 1:** Scan source; build **symbol table** (label → address); assign addresses.
  - **Pass 2:** Translate instructions using symbol table; generate object code.
- **Symbol Table:** Dictionary mapping labels to their memory addresses.
- **Forward Reference:** Label used before it is defined (resolved in pass 2 using symbol table built in pass 1).

### 5.4 Program Loops

- **Counting Loop:** Counter in memory; use ISZ to decrement and skip when zero.
```asm
     LDA     CTR      / Load counter
LOOP ...              / Loop body
     ISZ     CTR      / Increment counter; skip if zero
     BUN     LOOP     / Branch back if not done
     ...              / Continue after loop
CTR  DEC -N           / Initialize to -N (count N iterations)
```

### 5.5 Subroutines

- **BSA** instruction used to call subroutine; saves return address.
- **Return:** Indirect BUN to address stored by BSA.
```asm
CALL: BSA     SUB      / Call subroutine (saves PC at SUB, jumps to SUB+1)
      ...

SUB,  HEX 0           / Return address stored here
      ...              / Subroutine body
      BUN     SUB  I   / Indirect jump through SUB (returns to caller)
```

**Parameter Passing:** Via accumulator, memory locations, or on stack.

### 5.6 Input-Output Programming

- **Polling (Program-Controlled I/O):**
```asm
INPUT:  SKI          / Skip if input flag FGI set
        BUN  INPUT   / Loop until input ready
        INP          / Read character
        OUT          / Echo
```
- **Interrupt-Driven I/O:** More efficient; CPU executes other code while waiting.

---

## 6. Microprogrammed Control

### 6.1 Control Memory

- Stores microinstructions that implement machine instructions.
- **Microprogram:** Sequence of microinstructions implementing one machine instruction.
- **Microinstruction:** Specifies set of control signals for one clock cycle.
- **Microprogrammed Control Unit:** Reads microinstruction from control memory and generates control signals.

**Microinstruction Format:**
```
[Microoperation fields] [Address Selection fields] [Condition field]
```

**Horizontal Microinstruction:**
- One bit per control signal; wide word; maximum parallelism.
- Long microinstruction word (many bits); expensive control memory.
- Fast (direct control signal generation).

**Vertical Microinstruction:**
- Encoded control signals; shorter word; decoder needed.
- Smaller control memory; slower due to decoding.

### 6.2 Address Sequencing

- Determines address of next microinstruction to execute.

**Methods:**
1. **Incrementing:** Next address = current address + 1 (sequential execution).
2. **Unconditional Branch:** Jump to specified address in microinstruction.
3. **Conditional Branch:** Jump based on status flag (carry, zero, sign, etc.).
4. **Mapping:** Convert machine instruction opcode to starting address of its microprogram.
   - Typical mapping: Insert 0s into opcode bits to form control memory address.
5. **Subroutine Call:** Push return address; jump to subroutine microprogram.

**CAR (Control Address Register):** Holds address of current microinstruction.
**CBR (Control Buffer Register):** Holds current microinstruction being executed.
**SBR (Subroutine Branch Register):** Saves return address for microprogrammed subroutines.

### 6.3 Design of Microprogrammed Control Unit

**Components:**
- **Control Memory (ROM):** Stores microprogram (typically 128 × 20 bits or similar).
- **CAR:** Addressed control memory.
- **Sequencer:** Determines next CAR value (increment, branch, map, return).
- **Decoder:** Converts encoded microoperation field to control signals.

**Microinstruction Fields (Wilkes-style design):**
```
| F1 (3 bits) | F2 (3 bits) | F3 (3 bits) | CD (2 bits) | BR (2 bits) | AD (n bits) |
```
- F1, F2, F3: Microoperation groups.
- CD: Condition (which flag to test).
- BR: Branch type (00=continue, 01=unconditional jump, 10=conditional jump, 11=map/call).
- AD: Next address.

---

## 7. Central Processing Unit

### 7.1 General Register Organization

- CPU has a set of registers connected via an internal bus.
- **ALU** operates on data from registers.
- **Register file:** Array of general-purpose registers (e.g., 8 or 16 registers).
- **Register selection:** Source registers and destination register specified by multiplexers.

**Operations:**
- **Three-address:** `R3 ← R1 OP R2` (specifies all three registers).
- **Two-address:** `R2 ← R2 OP R1` (destination doubles as source).
- **One-address (accumulator):** `AC ← AC OP M[addr]`.
- **Zero-address (stack):** Operands implicitly from top of stack.

### 7.2 Stack Organization

- **LIFO (Last In, First Out)** structure.
- **SP (Stack Pointer):** Points to top of stack.
- **Operations:** PUSH (SP ← SP+1; M[SP] ← data) and POP (data ← M[SP]; SP ← SP-1). (Convention may differ.)
- **Stack-based CPU:** Operands for arithmetic taken from stack; result pushed onto stack.
- **RPN (Reverse Polish Notation):** `A B + C *` means `(A+B)*C`; natural for stack machines.

**Limitations:** Hard to express complex expressions with more than two active operands.

### 7.3 Instruction Formats

**Number of addresses per instruction:**

| Format | Example | Notes |
|---|---|---|
| 3-address | `ADD R1, R2, R3` (R1=R2+R3) | Flexible; long instruction |
| 2-address | `ADD R1, R2` (R1=R1+R2) | Source doubles as destination |
| 1-address | `ADD M[addr]` (AC=AC+M) | Accumulator implicit |
| 0-address | `ADD` (TOS=TOS+NOS) | Stack machine |

**Instruction Length:** Fixed or variable.
- **Fixed:** Simpler decoding; wastes bits for short instructions.
- **Variable:** Efficient; complex decoding.

**Expanding Opcode:** Use short opcodes for common instructions, longer for rare ones.
- Example (16-bit instruction, 4-bit opcode): 15 three-address instructions (opcode 0000–1110) + 14 two-address + 31 one-address + 16 zero-address instructions.

**Expanding Opcode Example:**
```
4-bit field, 6-bit address:
1111 | xxxx | xxxx (allows up to 16 zero-address instructions from 1111 prefix)
1110 | xxxxxx (allows 1 two-address or used differently)
```

### 7.4 Addressing Modes

| Mode | Effective Address (EA) | Notation | Use |
|---|---|---|---|
| **Implied/Implicit** | Operand in specified register | — | Register operations |
| **Immediate** | Operand = constant in instruction | `#N` | Constant loading |
| **Direct (Absolute)** | EA = address field | `M[A]` | Simple variable access |
| **Indirect** | EA = M[address field] | `M[M[A]]` | Pointer dereference |
| **Register Direct** | Operand in register | `Rn` | Fast; no memory access |
| **Register Indirect** | EA = content of register | `M[Rn]` | Pointer via register |
| **Displacement/Based** | EA = base register + offset | `M[R + A]` | Stack frames, arrays |
| **Indexed** | EA = index register + address | `M[Rᵢ + A]` | Array element access |
| **Base + Index** | EA = base + index | `M[Rᵦ + Rᵢ]` | 2D arrays |
| **Relative (PC-relative)** | EA = PC + offset | `M[PC + A]` | Branch instructions |
| **Auto-increment** | EA = Rn; Rn ← Rn + 1 | `M[Rn]+` | Array traversal |
| **Auto-decrement** | Rn ← Rn − 1; EA = Rn | `−M[Rn]` | Stack push |

**Note:** Immediate addressing — no memory access for operand (fastest); indirect — extra memory access (slowest for EA computation).

### 7.5 RISC vs CISC

| Feature | RISC | CISC |
|---|---|---|
| Instruction set | Small, simple, uniform | Large, complex, variable |
| Instruction length | Fixed (typically 32 bits) | Variable |
| Addressing modes | Few (2–4) | Many (5–20+) |
| Registers | Many (32+) | Few |
| Memory access | Load/Store only | Operands directly from memory |
| Execution | 1 instruction/cycle (pipelined) | Multiple cycles per instruction |
| Control unit | Hardwired | Microprogrammed |
| Clock speed | Higher | Lower |
| Code density | Lower (more instructions) | Higher (fewer instructions) |
| Examples | MIPS, SPARC, ARM, RISC-V | x86, x86-64, VAX, 68000 |

**RISC Design Principles:**
1. Simple, fixed-length instructions.
2. Load/Store architecture (only load and store access memory).
3. Large register file (eliminates memory accesses).
4. Hardwired control (no microcode).
5. Single-cycle execution of most instructions.
6. Pipeline optimised.

---

## 8. Pipeline and Vector Processing

### 8.1 Parallel Processing

- **Types:**
  - **Pipeline:** Overlap execution of instructions.
  - **Vector/Array:** Same operation on multiple data simultaneously (SIMD).
  - **Multiprocessor/Multicore:** Multiple CPUs.

**Flynn's Classification (based on instruction and data streams):**

| Class | Instruction streams | Data streams | Example |
|---|---|---|---|
| **SISD** | Single | Single | Classical uniprocessor |
| **SIMD** | Single | Multiple | Vector processors, GPU, SSE/AVX |
| **MISD** | Multiple | Single | Rare; fault-tolerant systems |
| **MIMD** | Multiple | Multiple | Multiprocessors, multicomputers |

### 8.2 Pipelining

- Divide instruction execution into stages; each stage processes one instruction per cycle.
- Multiple instructions overlap in different stages simultaneously.

**Pipeline Stages (classic 5-stage RISC):**
1. **IF** — Instruction Fetch: Fetch instruction from memory.
2. **ID** — Instruction Decode / Register Fetch: Decode and read registers.
3. **EX** — Execute: ALU operation or address calculation.
4. **MEM** — Memory Access: Read or write data memory.
5. **WB** — Write Back: Write result to register file.

**Speedup:**
- Ideal speedup for n-stage pipeline with k instructions: `S = (k × n) / (n + k − 1)`
- As k → ∞ (many instructions): `S → n` (n = number of stages).

**Pipeline Performance:**
- `Clock cycle = max stage delay + pipeline register overhead`
- **Throughput:** Instructions completed per unit time.
  - Ideal: 1 instruction per clock cycle (after pipeline fills).
- **Latency:** Time to complete one instruction = n × clock cycle (n = stages).
- **Efficiency:** `E = S/n`
- For k tasks in n-stage pipeline: `Time = (n + k − 1) × tclk`

**Example:** 5-stage pipeline, 100 instructions, each stage 1 ns:
- Without pipeline: 100 × 5 = 500 ns.
- With pipeline: (5 + 100 − 1) × 1 = 104 ns.
- Speedup ≈ 500/104 ≈ 4.81.

### 8.3 Pipeline Hazards

**Structural Hazard:** Two instructions need the same hardware resource simultaneously.
- Solution: Stall pipeline (insert bubble) or add duplicate hardware.

**Data Hazard:** Instruction depends on result of a previous instruction not yet complete.

| Type | Example | Description |
|---|---|---|
| RAW (Read After Write) | `ADD R1,R2,R3; SUB R4,R1,R5` | True dependence; most common |
| WAR (Write After Read) | — | Anti-dependence; less common in in-order |
| WAW (Write After Write) | — | Output dependence |

**Solutions for Data Hazards:**
- **Stall (pipeline bubble):** Insert NOP cycles. Performance loss.
- **Forwarding (Data Bypass):** Route result directly from EX/MEM stage to ID/EX input without waiting for WB. Eliminates most RAW hazards.
- **Out-of-order execution + register renaming:** Eliminates WAR, WAW hazards.

**Load-Use Hazard:** Data from a load instruction needed in immediately following instruction.
- Must stall 1 cycle even with forwarding (data not available until end of MEM stage).
- Compiler can reorder instructions (load scheduling) to avoid stall.

**Control Hazard (Branch Hazard):** Branch instruction changes PC; instructions fetched after branch may be wrong.

**Solutions for Control Hazards:**
- **Stall:** Wait for branch resolution (flush fetched instructions).
- **Branch Prediction:** Guess branch outcome; fetch speculatively.
  - **Static:** Always predict not-taken; or predict backward branches taken.
  - **Dynamic:** Use history (BTB — Branch Target Buffer, 1-bit or 2-bit saturating counter).
  - **2-bit predictor states:** Strongly taken, Weakly taken, Weakly not-taken, Strongly not-taken.
  - **Penalty:** If prediction wrong, flush pipeline and restart from correct address.
- **Delayed Branch:** Execute instruction(s) after branch regardless of outcome (delay slot); compiler fills delay slot with useful instruction.
- **Branch Target Buffer (BTB):** Cache of {PC → predicted target} pairs.

**Branch Prediction Accuracy:** Modern predictors achieve >95% accuracy.

### 8.4 Arithmetic Pipeline

- Pipeline for floating-point operations.
- **Floating-Point Adder Pipeline (4 stages):**
  1. Compare exponents; compute difference.
  2. Shift smaller mantissa right by exponent difference.
  3. Add/subtract mantissas.
  4. Normalise result.

**Pipeline Diagram (Space-Time Diagram):**
```
Stage:   1  2  3  4
Task 1: [1][2][3][4]
Task 2:    [1][2][3][4]
Task 3:       [1][2][3][4]
```
- Throughput = 1 result per clock cycle (after pipeline fills).

### 8.5 Instruction Pipeline

- **Super-scalar:** Issue multiple instructions per cycle using multiple execution units.
- **VLIW (Very Long Instruction Word):** Compiler explicitly packs multiple operations into one wide instruction.
- **Out-of-order execution:** Instructions executed in order that data is available; reordered result committed in original order (ROB — Reorder Buffer).

### 8.6 Vector Processing

- Operates on vectors (arrays of numbers) rather than scalars.
- **Vector registers:** Hold n elements (e.g., 64 doubles).
- **Vector instructions:** Apply operation to all elements simultaneously or in pipeline.
- `VADD V3, V1, V2` → `V3[i] = V1[i] + V2[i]` for all i.

**Advantages:** Eliminates instruction fetch overhead for loops; exploits memory bandwidth.
**Applications:** Scientific computing, graphics, signal processing.

**Array Processors:**
- **SIMD Array:** Many simple processors operating on different data under a single control unit.
- **Systolic Array:** Rhythmic computation; data flows through array of processing elements. Used in matrix multiplication, convolution, neural networks.

---

## 9. Input-Output Organization

### 9.1 Peripheral Devices

- Keyboard, Mouse, Display, Printer (character/line/page), Disk drives, Magnetic tape, Terminals, Modems, Network adapters.
- Characterised by: Data rate, Transfer unit (character vs block), Directionality, Error rate.

### 9.2 I/O Interface

- **I/O Port:** Set of registers (data, status, control) associated with a device.
- **I/O Interface:** Circuit connecting device to system bus.
- **Status Register:** Contains device flags (ready, error, busy).
- **Control Register:** Commands sent to device.
- **Data Register:** Data in/out.

**I/O Addressing:**
- **Memory-Mapped I/O:** I/O registers occupy part of memory address space; same instructions as memory.
- **Isolated I/O (Port-Mapped):** Separate I/O address space; special IN/OUT instructions.

### 9.3 Asynchronous Data Transfer

**Strobe Control (one-way handshaking):**
- Master asserts strobe signal to indicate data valid.
- Slave must capture data before next strobe.
- No acknowledgement from slave.

**Handshaking (two-way, interlocked):**
- Master: puts data on bus, asserts **Data Valid** signal.
- Slave: receives data, asserts **Data Accepted** (acknowledge).
- Master: removes data, deasserts Data Valid.
- Slave: deasserts acknowledge.
- Ensures reliable transfer; self-timed.

### 9.4 Modes of Transfer

| Mode | Description | CPU involvement |
|---|---|---|
| **Programmed I/O (Polling)** | CPU continuously polls device status register | High (busy-wait) |
| **Interrupt-Driven I/O** | Device interrupts CPU when ready; CPU services ISR | Moderate |
| **DMA** | DMA controller handles block transfer; interrupts CPU only at end | Low |

### 9.5 Priority Interrupt

**Interrupt Nesting:** Higher-priority interrupt can interrupt lower-priority ISR.

**Priority Schemes:**
- **Daisy Chain (Serial):** Interrupt acknowledge signal passes through devices in series; first device in chain has highest priority; simple but slow.
- **Parallel (Vectored Interrupt):** Each device has dedicated interrupt line with priority encoder; faster.
- **Software Priority Poll:** ISR checks each device in priority order.

**Interrupt Vector Table (IVT):** Table of ISR addresses; device provides vector number; CPU indexes into IVT.
- x86: 256 interrupt vectors (0–255); first 32 reserved for exceptions.

**Saving and Restoring State:**
- On interrupt: CPU saves PC, flags (and sometimes registers) onto stack.
- On return (IRET/RTI): Restore saved state.

**Interrupt Priority Levels (Intel 8259A PIC):**
- 8-level priority; can be cascaded for more levels.
- **ICW (Initialization Command Words)** configure the PIC.

### 9.6 DMA (Direct Memory Access)

- DMA controller (DMAC) handles data transfer between I/O device and memory directly.
- CPU initialises DMAC with: source address, destination address, byte count, mode.
- DMAC requests bus from CPU (holds bus during transfer = **cycle stealing**).
- On completion, DMAC interrupts CPU.

**DMA Transfer Modes:**
- **Burst Mode:** DMAC holds bus for entire transfer; CPU waits.
- **Cycle Steal Mode:** DMAC steals one bus cycle per transfer; CPU slows down but continues.
- **Transparent (Interleaved) Mode:** DMA transfers when CPU not using bus; no slowdown.

**DMA Address and Count Registers:**
- `Source Address Register`, `Destination Address Register`, `Count Register`.
- After each transfer: `Address ← Address + 1; Count ← Count − 1`.
- When `Count = 0`: Interrupt CPU.

### 9.7 Serial Communication

**Asynchronous Serial:**
- Data framed with start bit (0), data bits (5–8), parity bit (optional), stop bit(s) (1 or 2).
- No shared clock; receiver synchronises on start bit.
- **Baud rate:** Symbols per second. `Bit rate = Baud rate × bits per symbol`.
- Example: 8-N-1 format (8 data, no parity, 1 stop) = 10 bits per character.

**Synchronous Serial:**
- Continuous bit stream with shared clock; no start/stop bits.
- Framing by special sync characters or bit patterns.
- Higher efficiency (less overhead); used in SPI, I²C, HDLC, USB.

**Standards:**
- **RS-232:** Serial communication; voltage levels ±3 to ±15V; max ~115 kbps for short distances.
- **UART (Universal Asynchronous Receiver/Transmitter):** Hardware implementing async serial.
- **SPI:** Synchronous; full-duplex; 4-wire (MOSI, MISO, SCLK, SS); master-slave.
- **I²C:** Synchronous; half-duplex; 2-wire (SDA, SCL); multi-master; 7-bit addresses.
- **USB:** Serial; differential signalling; host-controlled; various speeds (1.5 Mbps to 20 Gbps).

---

## 10. Memory Hierarchy

### 10.1 Memory Hierarchy Overview

```
Registers   → Fastest, smallest, most expensive (bits)
Cache L1    → Very fast (~1 ns); 32–64 KB per core
Cache L2    → Fast (~5 ns); 256 KB – 1 MB per core
Cache L3    → Moderate (~20 ns); 4–32 MB shared
Main Memory (DRAM) → ~100 ns; GBs
Auxiliary (SSD/HDD) → ms; TBs
```

**Principle of Locality:**
- **Temporal Locality:** Recently accessed items likely accessed again soon.
- **Spatial Locality:** Items near recently accessed items likely accessed soon.
- Both exploited by cache.

### 10.2 Main Memory

- **DRAM (Dynamic RAM):** Main memory; must be refreshed periodically.
- **SDRAM (Synchronous DRAM):** Synchronised with system clock; burst transfers.
- **DDR SDRAM (Double Data Rate):** Transfers on both rising and falling clock edges.
  - DDR4: ~25 GB/s bandwidth per channel.
- **Memory Interleaving:** Distribute consecutive addresses across multiple memory banks; allows overlapped access.
  - `Bank number = address mod m` (m = number of banks).
  - m-way interleaving can provide up to m× bandwidth increase.

**Memory Expansion:**
- **Increase word size:** Connect multiple chips in parallel (e.g., 4 × 1M×4-bit chips = 1M × 16-bit memory).
- **Increase address space:** Connect multiple chips with chip select (e.g., 4 × 1M×8-bit chips = 4M × 8-bit memory).

### 10.3 Auxiliary Memory

- **Magnetic Disk (HDD):** Platters, tracks, sectors, cylinders; access = seek + rotational + transfer.
- **Magnetic Tape:** Sequential access; used for backup.
- **SSD (Flash):** No moving parts; faster random access; limited write endurance.
- **Optical Disk:** CD (700 MB), DVD (4.7–17 GB), Blu-ray (25–128 GB).

### 10.4 Associative Memory (Content-Addressable Memory, CAM)

- Search by content rather than address.
- All locations searched simultaneously in parallel (hardware comparison).
- Used in: TLB, cache tag comparison, routing tables, database search.

**Structure:**
- Each word has a comparand register.
- Argument register holds search key.
- Match register: bit i = 1 if word i matches argument.
- **Mask register:** Specifies which bits to compare (don't-care bits).

**Operations:**
- `Match = (Word XOR Argument) AND (NOT Mask)` applied to each word.
- Word i matches if all unmasked bits equal corresponding argument bits.
- **Multiple matches:** Resolved by priority (first-match or most-recently-used).

**Advantage:** O(1) lookup regardless of size. **Disadvantage:** Expensive (each cell has a comparator).

### 10.5 Cache Memory

**Operation:**
1. CPU generates memory address.
2. Check cache; if **hit** → return data (fast).
3. If **miss** → fetch from main memory → load into cache → return data.

**Cache Hit Ratio (h):** Fraction of accesses found in cache.

**Effective Access Time:**
`EAT = h × Tc + (1 − h) × Tm`
where Tc = cache access time, Tm = main memory access time.

If main memory accessed only on miss (and cache checked first):
`EAT = Tc + (1 − h) × Tm` (sequential access model)

**Cache Organisation — Mapping Functions:**

**1. Direct Mapping:**
- `Cache line = (Block address) mod (Number of cache lines)`
- `Cache line = Block address mod C` (C = number of cache lines)
- Address divided into: **Tag | Line | Word**
- Simple; no replacement needed; but conflicts (two blocks map to same line).
- **Conflict miss:** Two frequently used blocks map to same cache line; thrash.

**2. Fully Associative:**
- Block can go into any cache line.
- Tag search: CAM searches all lines simultaneously.
- Most flexible; lowest miss rate; complex and expensive hardware.
- **Replacement algorithms needed:** LRU, FIFO, Random, LFU.

**3. Set-Associative (k-way):**
- Cache divided into sets; each set has k lines.
- Block maps to a specific set (direct); within the set, it can go into any of the k lines (associative).
- `Set number = Block address mod (Number of sets)`
- Address: **Tag | Set | Word**
- Compromise between direct and fully associative.

**Address Division for k-way Set-Associative Cache:**
- Cache size = C bytes, block size = B bytes.
- Number of sets `S = C / (k × B)`.
- Bits for word offset = `log₂(B)`.
- Bits for set index = `log₂(S)`.
- Bits for tag = remaining address bits.

**Example:** 32-bit address, 4 KB cache, 64-byte blocks, 4-way set-associative:
- B = 64 → word offset bits = 6.
- S = 4096 / (4 × 64) = 16 sets → set index bits = 4.
- Tag bits = 32 − 6 − 4 = 22.

**Cache Write Policies:**
- **Write-Through:** Write to both cache and main memory on every write. Simple; slower writes; always consistent.
- **Write-Back (Copy-Back):** Write only to cache; write to memory only when line is replaced (dirty bit set). Faster; risk of inconsistency.

**Write Miss Policies:**
- **Write-Allocate:** On write miss, load block into cache then write.
- **No-Write-Allocate (Write Around):** On write miss, write directly to memory; do not cache.

**Replacement Algorithms:**
- **LRU (Least Recently Used):** Replace least recently used line. Best performance; complex to implement perfectly.
- **FIFO (First In, First Out):** Replace oldest loaded line. Belady's Anomaly possible.
- **LFU (Least Frequently Used):** Replace line used least often. Can retain old infrequently used data.
- **Random:** Replace randomly chosen line. Simple; surprisingly effective.
- **Pseudo-LRU:** Approximation of LRU using bits.

**Types of Cache Misses (3Cs):**
- **Compulsory (Cold) Miss:** First access to a block; unavoidable.
- **Capacity Miss:** Cache too small to hold all working set.
- **Conflict Miss:** Two blocks compete for same cache location (direct or set-associative).

**Cache Performance:**
- `AMAT (Average Memory Access Time) = Hit_time + Miss_rate × Miss_penalty`
- Reducing miss rate: larger cache, higher associativity, larger blocks (exploit spatial locality).
- Reducing miss penalty: multilevel cache, critical word first, victim cache.

### 10.6 Virtual Memory

- Process addresses (virtual) translated to physical addresses by hardware (MMU + TLB).
- Pages not in physical memory stored on disk (**page fault** → load from disk).

**Page Table Entry (PTE) bits:**
- Present/Valid bit, Dirty bit, Reference bit, Protection bits (R/W/X), Physical Frame Number.

**TLB (Translation Lookaside Buffer):**
- Fast associative cache of recently used PTEs.
- **TLB Hit:** Physical address in one cycle.
- **TLB Miss:** Page table walk in memory (multiple accesses).
- **TLB Flush:** Required on context switch (or use ASIDs — Address Space Identifiers to avoid full flush).

**Page Replacement:** LRU, Clock, Optimal — see OS notes (Unit 5).

### 10.7 Memory Management Hardware

- **Base and Limit Registers:** Simplest; protect one contiguous region.
  - `Physical = Logical + Base`; check `Logical < Limit`.
- **Segmentation Hardware:** Segment table with (base, limit) per segment.
  - `Physical = Segment_base + Offset`; check `Offset < Limit`.
- **Paging Hardware:** Page table maps page number to frame number.
  - `Physical = (Frame × Page_size) + Offset`.
- **Segment + Paging:** Each segment is paged; used in x86.
- **TLB Hardware:** Fully associative cache for page table entries; parallel lookup.
- **Multi-level Page Tables:** Reduce page table size for sparse address spaces.
- **Inverted Page Table:** One entry per physical frame; reduces table size; slower lookup.

---

## 11. Multiprocessors

### 11.1 Characteristics of Multiprocessors

- Multiple CPUs sharing memory or communicating via network.
- **Tightly Coupled (Shared Memory):** All processors share a common main memory; communication via shared variables; MIMD.
- **Loosely Coupled (Distributed):** Processors have their own private memory; communicate via message passing.

**Advantages:** Performance, reliability (fault tolerance), scalability, economy.

**Performance:** Speedup `S = T₁ / Tₙ` where T₁ = single processor time, Tₙ = n-processor time.
- **Amdahl's Law:** `S(n) = 1 / (f + (1-f)/n)` where f = fraction of serial code.
- As n → ∞: `S_max = 1/f`.

**Gustafson's Law:** `Scaled speedup = n − α(n − 1)` where α = serial fraction.
- Different from Amdahl's: problem size grows with n; more realistic for real applications.

### 11.2 Interconnection Structures

**Bus-Based:**
- Single shared bus; all processors and memory connected.
- Simple; cheap; limited scalability (bus becomes bottleneck).
- **Cache coherence** critical.

**Crossbar Switch:**
- Each processor-memory pair has a dedicated switch.
- Full bandwidth; non-blocking (simultaneous transfers); very expensive.
- `n × n` crossbar for n processors and n memories: `n²` switch elements.

**Multistage Interconnection Networks (MINs):**
- Multiple stages of 2×2 switches between processors and memories.
- **Omega Network (Shuffle-Exchange):** `log₂N` stages, `N/2 × log₂N` switches.
- **Butterfly Network:** Similar structure.
- **Banyan Network:** Non-blocking under certain routing conditions.
- **Cost:** O(N log N); performance between crossbar and bus.
- **Blocking:** Multiple paths may conflict → some requests delayed.

**Types of Networks:**
| Network | Topology | Diameter | Bisection Width |
|---|---|---|---|
| **Bus** | Linear shared | 1 | 1 |
| **Ring** | Circular | N/2 | 2 |
| **Mesh (2D)** | Grid | 2(√N − 1) | √N |
| **Hypercube** | n-dimensional cube | n = log₂N | N/2 |
| **Fat Tree** | Tree with wider upper links | 2log₂N | N/2 |
| **Torus** | Mesh with wraparound | √N | 2√N |

**Diameter:** Maximum distance between any two nodes (latency).
**Bisection Width:** Minimum edges to cut to split into two equal halves (bandwidth).

### 11.3 Interprocessor Arbitration

- **Bus Arbitration:** Resolves conflicts when multiple processors request bus simultaneously.

**Methods:**
- **Daisy Chain:** Grant signal propagated; highest priority closest to arbiter; simple but unfair.
- **Centralised Parallel (Fixed Priority):** Each processor has separate request line; arbiter uses priority encoder.
- **Distributed (LRU / Round Robin):** Each processor participates in arbitration; fairer.
- **Polling:** Arbiter polls processors in sequence; each cycle a different processor checked.

**Protocols:**
- **Distributed Self-Selection:** Processors broadcast requests; determine priority by comparing IDs.
- **Collision Detection:** Used in bus protocols like CSMA/CD.

### 11.4 Interprocessor Communication and Synchronization

**Shared Memory Communication:**
- Read/write shared variables; fast but requires synchronisation.
- **Load/Store atomicity** assumed for basic types.

**Synchronisation Primitives:**
- **Test-and-Set (TAS):** Atomic; reads memory and sets to 1; returns old value.
  ```
  TAS(lock): temp ← M[lock]; M[lock] ← 1; return temp
  ```
  - Spin-lock: `while TAS(lock) ≠ 0: spin`; release: `M[lock] ← 0`.

- **Compare-and-Swap (CAS):**
  ```
  CAS(memory, expected, new): 
    if M[memory] == expected: M[memory] ← new; return true
    else: return false
  ```
  - Foundation for lock-free data structures.

- **Fetch-and-Add:** Atomically adds a value and returns old value.
- **LL/SC (Load-Linked / Store-Conditional):** Used in RISC (MIPS, ARM); avoids ABA problem.

**Barrier Synchronisation:** All processors must reach barrier before any proceeds.

### 11.5 Cache Coherence

**Problem:** Multiple processors have private caches; one processor modifies data → others see stale copy.

**Cache Coherence Conditions (for a memory system to be coherent):**
1. A read by processor P after P writes value v to address X (with no intervening writes) returns v.
2. A read by P after Q writes v to X returns v (with sufficient time between).
3. Writes to same address are serialised — all processors see the same order of writes.

**Snoopy Bus Protocol:**
- Each cache controller monitors (snoops) bus transactions.
- When cache sees a write to a block it holds, it either **invalidates** or **updates** its copy.

**MSI Protocol (three states):**
- **M (Modified):** Block dirty; only this cache has it; must write back on replacement.
- **S (Shared):** Block clean; potentially multiple caches have it.
- **I (Invalid):** Block not valid in this cache.

**MESI Protocol (four states):**
- **M (Modified):** Dirty; exclusive; only this cache.
- **E (Exclusive):** Clean; only this cache (no others). Can write without broadcast.
- **S (Shared):** Clean; possibly multiple caches.
- **I (Invalid):** Not valid.

**MOESI Protocol:** Adds **O (Owned)** — dirty but shared (another cache may read it directly).

**Directory-Based Coherence:**
- Scales beyond bus-based; each memory block has a directory entry recording which caches hold it.
- **Full-map directory:** One bit per processor per memory block: `O(M × P)` storage (M=blocks, P=processors).
- **Limited directory:** Only track small number of sharers; use broadcast if more.
- **Chained directory:** Directory entries form linked list of sharers.

### 11.6 Multicore Processors

- Multiple processor cores on a single die.
- Share LLC (Last-Level Cache), memory controller, interconnect.

**Cache Hierarchy:**
- L1 (private per core), L2 (private per core or shared per cluster), L3 (shared across all cores).
- Coherence maintained at L1 and L2 by MESI-type protocol.

**NUMA (Non-Uniform Memory Access) in Multicore:**
- Memory banks closer to some cores than others; access latency differs.
- OS and runtime must be NUMA-aware for performance.

**Simultaneous Multithreading (SMT / Hyper-Threading):**
- Multiple hardware threads share functional units of one core.
- Hides latency; improves utilisation of execution units.
- Intel Hyper-Threading: 2 threads per core; appears as 2 logical CPUs.

**Memory Consistency Models:**
- **Sequential Consistency:** Memory accesses appear to all processors in a single sequential order.
- **Total Store Order (TSO):** Writes may be locally buffered (store buffer); reads may bypass writes (x86 model).
- **Relaxed Consistency:** Various relaxations for performance; memory barriers (fences) enforce ordering.

---

## Quick Recap Table

| Topic | Key Formulas / Concepts |
|---|---|
| Full Adder | `S = A⊕B⊕Cin`; `Cout = AB + BCin + ACin` |
| CLA | `Cᵢ₊₁ = Gᵢ + PᵢCᵢ`; `Gᵢ = AᵢBᵢ`; `Pᵢ = Aᵢ⊕Bᵢ` |
| 2's Complement | Flip all bits + 1; Range: `-2^(n-1)` to `+2^(n-1) - 1` |
| Overflow (2's complement) | `V = Cₙ ⊕ Cₙ₋₁` (carry in XOR carry out of MSB) |
| IEEE 754 Single | 1+8+23 bits; Bias=127; Value: `(-1)^S × 1.M × 2^(E-127)` |
| Hamming Code | `2^r ≥ m + r + 1`; error position = syndrome value |
| JK FF | `Q(next) = JQ' + K'Q`; J=K=1 → toggle |
| D FF | `Q(next) = D` |
| T FF | `Q(next) = T⊕Q` |
| Ring Counter | n FFs → n states; `1/f_clk` per state |
| Johnson Counter | n FFs → 2n states |
| Booth's Algorithm | Examine `Q[0]Q[-1]`; 00/11=shift; 01=add; 10=subtract |
| Pipeline Speedup | `S = (k×n)/(n+k-1)`; approaches n as k→∞ |
| Pipeline Time | `(n + k - 1) × tclk` for k tasks, n stages |
| Amdahl's Law | `S(n) = 1/(f + (1-f)/n)`; limit `S_max = 1/f` |
| Cache EAT | `h×Tc + (1-h)×Tm`; or `Tc + (1-h)×Tm` |
| AMAT | `Hit_time + Miss_rate × Miss_penalty` |
| Set-Associative Sets | `S = Cache_size / (k × Block_size)` |
| Direct Mapped | `Line = Block_addr mod C`; address: Tag|Line|Word |
| Cache Misses (3Cs) | Compulsory, Capacity, Conflict |
| Virtual Memory EAT | `h×Tc + (1-h)×(Tc + TDisk)` ≈ same as demand paging |
| DMA Count | `Count ← 0` triggers interrupt; cycle steal mode |
| Crossbar cost | `n²` switches for n×n |
| Omega Network | `log₂N` stages; `(N/2)log₂N` switches |
| Hypercube Diameter | `log₂N` for N nodes |
| Bus Arbitration | Daisy chain, Parallel, Polling, Distributed |
| MESI States | Modified, Exclusive, Shared, Invalid |
| TAS Spinlock | `while TAS(lock) ≠ 0: spin`; ensures mutual exclusion |
| Nyquist Sampling | `f_sample ≥ 2 × f_max` |
| Memory Interleaving | `Bank = address mod m`; m-way → m× potential bandwidth |

---
