

# 🧠 Tiny RISC – 5-Stage Pipelined Processor (Verilog)

This repository contains a **Tiny RISC processor** implemented in **Verilog HDL**, featuring a **classic 5-stage pipeline architecture**.
The project is designed for **learning, RTL design practice.

---

## 📌 Overview

The processor follows a **RISC-style design** with a fixed instruction format and a clean separation of pipeline stages:

1. **IF** – Instruction Fetch
2. **ID** – Instruction Decode & Register Fetch
3. **EX** – Execute / ALU
4. **MEM** – Data Memory Access
5. **WB** – Write Back

Each stage is separated using **pipeline registers**, enabling concurrent instruction execution.

---

## 🏗️ Architecture

* **Pipeline Depth:** 5 stages
* **Word Size:** 32-bit
* **Register File:** 16 registers × 32-bit
* **Instruction Format:** Fixed 32-bit
* **Design Style:** Modular, synthesizable RTL

---

## 🧩 Instruction Format (32-bit)

```
| 31:27 | 26 | 25:22 | 21:18 | 17:14 | 13:0 |
| opcode|imm |   rd  |  rs1  |  rs2  | imm |
```

* `opcode` : Instruction operation
* `imm`    : Immediate flag
* `rd`     : Destination register
* `rs1`    : Source register 1
* `rs2`    : Source register 2
* `imm`    : 14-bit immediate (sign-extended)

---

## 🧮 Supported Instructions

| Opcode | Instruction | Description           |
| ------ | ----------- | --------------------- |
| 00000  | ADD         | Add                   |
| 00001  | SUB         | Subtract              |
| 00010  | AND         | Bitwise AND           |
| 00011  | OR          | Bitwise OR            |
| 00100  | XOR         | Bitwise XOR           |
| 00101  | MOV         | Move / Load Immediate |
| 00110  | MUL         | Multiply              |
| 00111  | DIV         | Divide                |
| 01000  | LOAD        | Load from memory      |
| 01001  | STORE       | Store to memory       |

Immediate and register-based operations are supported using the `imm` flag.

---

## 🧠 Control & Datapath

* Central **Control Unit** generates:

  * `regwrite`
  * `memwrite`
  * `memtoreg`
  * `alusrc`
  * `aluop`
* Control signals are **properly pipelined** to avoid stage mismatch.
* Immediate values are **sign-extended** in EX stage.

---

## 🧪 Verification

* Custom **testbench** provided
* Instruction memory preloaded with test programs
* Register values verified at end of simulation
<img width="318" height="340" alt="Screenshot 2026-01-18 185253" src="https://github.com/user-attachments/assets/2a1786b9-16c7-4615-a4ac-61c9bca7c86e" />


---

## 📂 Module Breakdown

| Module            | Description               |
| ----------------- | ------------------------- |
| `instruction_mem` | Instruction memory        |
| `if_id`           | IF/ID pipeline register   |
| `decode`          | Instruction decode        |
| `id_ex`           | ID/EX pipeline register   |
| `control_unit`    | Control signal generation |
| `register_file`   | Register file             |
| `op`              | Operand selection (MUX)   |
| `alu`             | Arithmetic Logic Unit     |
| `ex_mem`          | EX/MEM pipeline register  |
| `mem_stage`       | Data memory stage         |
| `mem_wb`          | MEM/WB pipeline register  |
| `write_back`      | Write-back logic          |
| `risc`            | Top-level module          |

---


## 🔮 Planned Improvements

* Data forwarding unit
* Load-use hazard detection
* Branch & jump instructions
* Pipeline stall and flush logic

---

## 🎯 Learning Outcomes

* Strong understanding of **pipelined datapaths**
* Control signal timing across pipeline stages
* RTL coding best practices
* Modular Verilog design
* CPU microarchitecture fundamentals

---

## 🧑‍💻 Author

Designed and implemented by **kiran kumar**
Domain: **VLSI / RTL Design / Computer Architecture**


