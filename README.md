Here's a detailed **README** file for your `tiny_risc` Verilog project. This README explains the purpose, architecture, and usage of the modules clearly for educational or development purposes.

---

# Tiny RISC CPU – Verilog Implementation

## Overview

`tiny_risc` is a simple 32-bit RISC (Reduced Instruction Set Computer) CPU implemented in Verilog. This CPU demonstrates a basic instruction pipeline architecture, supporting essential arithmetic, logic, data movement, and memory access instructions.

It is a great learning tool for understanding how a RISC-based processor works, with modular components for each pipeline stage: Fetch, Decode, Execute, Memory, and Writeback.

---

## Features

* 32-bit architecture
* 5-bit opcode with immediate flag
* 16 general-purpose registers
* 8 instruction support:

  * Arithmetic: `ADD`, `SUB`, `MUL`, `DIV`
  * Logical: `AND`, `OR`, `XOR`
  * Data movement: `MOV`
  * Memory: `LOAD`, `STORE`
* Immediate and register-based operations
* Simple memory model for instruction and data

---

## File Structure

```
tiny_risc.v           # Top-level CPU module
instruction_fetch.v   # Instruction fetch stage
instruction_decode.v  # Instruction decode stage
register_file.v       # General-purpose register file
execute.v             # ALU and execution logic
memory_access.v       # Memory read/write logic
```

---

## Architecture Breakdown

### 1. `tiny_risc` (Top Module)

Controls program counter, integrates all pipeline modules, handles control logic, and generates the final output.

* Inputs: `clk`, `reset`
* Output: `result` (last write data)
* Key internal components:

  * Program counter (PC)
  * Instruction pipeline
  * Control signals for register and memory writes
  * Display debugging via `$display`

### 2. `instruction_fetch`

Fetches instructions from a hardcoded instruction memory using the program counter (`pc`).

* Instruction format (32 bits):

  ```
  [31:27] Opcode (5 bits)
  [26]    Immediate flag
  [25:22] Destination register (rd)
  [21:18] Source register 1 (rs1)
  [17:14] Source register 2 (rs2)
  [13:0]  Immediate value (sign-extended)
  ```

### 3. `instruction_decode`

Decodes the fetched instruction into control signals and operands.

* Outputs: opcode, immediate flag, rd, rs1, rs2, immediate extended to 32 bits

### 4. `register_file`

16 general-purpose 32-bit registers with synchronous write and asynchronous read.

* Registers are reset on system reset.
* Write enable (`reg_write_en`) controls write to destination register (`rd`).

### 5. `execute`

Arithmetic and logic unit (ALU) supporting:

* `ADD`, `SUB`, `MUL`, `DIV`, `AND`, `OR`, `XOR`, `MOV`
* Supports both register and immediate operations
* Division by zero is protected (returns `0xDEADBEEF`)

### 6. `memory_access`

Unified data memory (256 x 32-bit) that supports:

* `LOAD`: Read from memory into register
* `STORE`: Write register data into memory

---

## Sample Instructions (preloaded in `instruction_fetch`)

```verilog
instr_mem[0] = MOV R1, #10
instr_mem[1] = MOV R2, #20
instr_mem[2] = ADD R3, R1, R2
instr_mem[3] = ADD R4, R1, #5
instr_mem[4] = SUB R5, R2, R1
instr_mem[5] = MUL R6, R1, R2
instr_mem[6] = DIV R7, R2, R1
```

---

## Simulation Output

Using `$display`, you get trace outputs like:

```
Time: 0 | R1 = 10, R2 = 20
ALU Operation: R1 = 10, R2 = 20, Result = 30
```

This helps in debugging and validating the instruction flow.

---

## How to Run

1. Load all modules into a Verilog simulator (e.g., ModelSim, Vivado, Icarus Verilog).
2. Create a testbench that instantiates `tiny_risc` and applies clock and reset.
3. Observe the simulation waveforms or output console logs for register and ALU operations.




