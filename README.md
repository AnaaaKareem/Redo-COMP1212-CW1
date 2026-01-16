# From Truth Tables to Circuits (CWK1)

The **From Truth Tables to Circuits** project is a fundamental exercise in digital logic design using **Hack Hardware Description Language (HDL)**. It involves deriving minimum Boolean expressions from truth tables using Karnaugh maps and implementing the resulting circuits using basic logic gates.

The project proceeds from individual combinational logic circuits to a combined multiplexed circuit, and finally to a sequential circuit with feedback.

---

## Input and Interaction

The circuits are simulated using the **Nand2Tetris Hardware Simulator**. Interaction is primarily through automated test scripts which drive inputs and verify outputs.

* **Inputs**:
  * **Data Inputs**: `a`, `b`, `c` (and `d` in sequential logic).
  * **Control Inputs**: `f1`, `f0` (used in `FALL.hdl` to select the active function).
  * **Clock/Reset**: `clk`, `load` (used in `FSEQ.hdl` for sequential behavior).

**Interaction Flow:**

1. Load the Chip (`.hdl`) into the Hardware Simulator.
2. Load the corresponding Test Script (`.tst`).
3. Run the simulation.
4. The script applies inputs and validates the output pins.

---

## Output Format

The simulation generates output files and compares them against expected results:

* **Output Pins**:
  * `e`, `f`, `g`: Result bits of the logic functions.
* **Verification Files**:
  * `.out`: The actual output values recorded during simulation.
  * `.cmp`: The expected output values (Compare file).
  * **Success**: The simulator displays "Comparison ended successfully" if functionality is correct.

---

## How to Run

### Requirements

Allowed execution environment: **Nand2Tetris Software Suite** (specifically the `HardwareSimulator`).

### Execution

1. Launch the **HardwareSimulator** script/bat from the Nand2Tetris tools.
2. **Load Chip**: Click the folder icon to load an HDL file (e.g., `hdlFiles/FALL.hdl`).
3. **Load Script**: Click the script icon to select the matching test (e.g., `testFiles/FALL.tst`).
4. **Run**:
    * Press the **Run** button (Double Blue Arrows or Play icon) to execute the script.
    * Watch the "Output" and "Compare" views populate.
5. **Verify**:
    * Ensure the status bar reads "Comparison ended successfully".

---

## Program Features

* **Combinational Logic (F0 - F3)**:
  * Four distinct logic circuits (`FZero`, `FOne`, `FTwo`, `FThree`) acting on inputs `a`, `b`, `c`.
  * Implemented using minimum gate counts derived from K-Map analysis.
* **Combined Circuit (FALL)**:
  * Integrates all four sub-circuits.
  * Uses a multiplexer logic controlled by `f1` and `f0` to routing inputs to the correct function.
* **Sequential Logic (FSEQ)**:
  * Feedback loop where outputs determine the next state inputs.
  * Uses a **DFF (Data Flip-Flop)** or Register to maintain state across clock cycles.
* **Allowed Components**:
  * `Nand`, `Not`, `And`, `Or`, `Xor`, `Mux`, `DFF`.

---

## Author and License

It is not licensed and is free to use and modify for educational purposes.

---

## Logic Design Process

The following traces the theoretical process used to create the circuits in this project.

### 1. Truth Table Analysis

We begin with the specification truth tables (e.g., for `FZero`).

| a | b | c | E | F | G |
|---|---|---|---|---|---|
| 0 | 0 | 0 | 1 | 0 | 1 |
| 0 | 0 | 1 | 1 | 1 | 0 |
| ... | ... | ... | ... | ... | ... |

*(Actual values depend on the specifications for F0, F1, F2, F3)*

### 2. Karnaugh Map (K-Map) Minimization

For each output (E, F, G), we map the minterms to a K-Map to find the optimal grouping.

**Example K-Map for Output F:**

```
      bc
    00  01  11  10
 a +---+---+---+---+
 0 | 0 | 1 | 1 | 0 |
   +---+---+---+---+
 1 | 0 | 0 | 0 | 0 |
   +---+---+---+---+
```

*Groupings are identified to eliminate variables.*

### 3. Boolean Expression Deriviation

From the groups, we derive the Simplified Boolean Expression.

* **Expression**: $F(a, b, c) = \overline{a} \cdot c + ...$

### 4. HDL Implementation

The expression is translated into Hack HDL syntax.

```hdl
// Example partial implementation
Not(in=a, out=nota);
And(a=nota, b=c, out=term1);
Or(a=term1, b=..., out=f);
```
