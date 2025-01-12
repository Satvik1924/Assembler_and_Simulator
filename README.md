# Assembler and Simulator - README

## Overview
This project consists of an **Assembler** and **Simulator** for a simplified RISC-V-like architecture. The assembler converts assembly language instructions into machine code, while the simulator executes these instructions and manages register and memory operations.

### Key Components
1. **Assembler**:
   - Parses assembly code.
   - Validates instructions and registers.
   - Converts assembly code into binary machine instructions.

2. **Simulator**:
   - Simulates the execution of machine code instructions.
   - Implements RISC-V-like instruction formats (`R`, `I`, `S`, `B`, `U`, `J` types).
   - Maintains memory and register state throughout program execution.

---

## Features
### Assembler
- **Instruction Support**: Handles RISC-V-style instructions such as `add`, `sub`, `lw`, `sw`, `beq`, and `jal`.
- **Error Detection**:
  - Invalid instruction syntax.
  - Incorrect register usage.
  - Out-of-range immediate values.
  - Missing or misnamed labels.
- **Label Management**: Automatically calculates label addresses for branching and jumps.
- **Output**: Generates binary-encoded instructions ready for simulation.

### Simulator
- **Instruction Execution**: Simulates execution of binary machine code, supporting:
  - Arithmetic operations (`add`, `sub`, etc.).
  - Load/store instructions (`lw`, `sw`).
  - Branching (`beq`, `bne`).
  - Immediate and jump instructions (`addi`, `jal`).
- **Memory and Register State**:
  - Supports a register file of 32 registers.
  - Simulates memory access and updates.
- **Output**: Logs program counter (PC), register, and memory states after each instruction.

---

## Prerequisites
- Python 3.x.
- A text editor or IDE for editing assembly programs.

---

## Usage
### 1. Assemble Code
Run the assembler to convert an assembly file into machine code:
```bash
python Assembler.py <input_file> <output_file>
```
- `<input_file>`: Path to the assembly source file.
- `<output_file>`: Path to save the binary output.

### 2. Simulate Code
Run the simulator to execute the binary instructions:
```bash
python Simulator.py <input_file> <output_file>
```
- `<input_file>`: Path to the binary input file (output from assembler).
- `<output_file>`: Path to save the simulation logs.

---

## Instruction Formats
### Supported Instruction Types
| Type   | Description                          | Examples          |
|--------|--------------------------------------|-------------------|
| **R**  | Register-Register Arithmetic         | `add`, `sub`      |
| **I**  | Immediate Instructions               | `addi`, `lw`      |
| **S**  | Store Instructions                   | `sw`              |
| **B**  | Branch Instructions                  | `beq`, `bne`      |
| **U**  | Upper Immediate                      | `lui`, `auipc`    |
| **J**  | Jump Instructions                    | `jal`             |

---

## Outputs
### Assembler Output
- Binary machine code instructions, one per line.

### Simulator Output
- Step-by-step state of:
  - **Program Counter (PC)**.
  - **Registers**.
  - **Memory**.

---

## Error Handling
### Assembler
- Detects and reports:
  - Syntax errors in instructions.
  - Incorrect or out-of-bound register and immediate values.
  - Invalid labels or missing virtual halt (`beq zero, zero, 0`).

### Simulator
- Ensures:
  - Valid instruction execution within memory bounds.
  - Correct handling of register values and memory operations.

---

## Limitations
- **Instruction Limit**: Maximum of 128 instructions.
- **Memory Size**: Predefined memory locations in the simulator.
- **Registers**: Fixed register file of 32 registers.

---

## Example Workflow
### Input Assembly Code (example.asm)
```asm
add t0, t1, t2
lw t3, 0(t0)
beq t0, t1, label
label:
sub t4, t5, t6
beq zero, zero, 0
```

### Assembler Command
```bash
python Assembler.py example.asm output.bin
```

### Simulator Command
```bash
python Simulator.py output.bin simulation.log
```

---

## Future Enhancements
- Expand instruction support.
- Optimize error reporting for more detailed feedback.
- Add interactive simulation debugging tools.
