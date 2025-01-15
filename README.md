# RISC-V Assembler and Simulator

A Python-based RISC-V assembler and simulator that supports basic RISC-V instructions and provides detailed execution tracking.

## Overview

This project implements a basic RISC-V toolchain consisting of:
1. An assembler that converts RISC-V assembly code to machine code
2. A simulator that executes the generated machine code and tracks system state

## Features

### Assembler
- Supports multiple RISC-V instruction formats:
  - R-type: `add`, `sub`, `sll`, `slt`, `sltu`, `xor`, `srl`, `or`, `and`
  - I-type: `lw`, `addi`, `sltiu`, `jalr`
  - S-type: `sw`
  - B-type: `beq`, `bne`, `blt`, `bge`, `bltu`, `bgeu`
  - U-type: `lui`, `auipc`
  - J-type: `jal`
- Label support for branch and jump instructions
- Error detection for:
  - Invalid register usage
  - Out-of-range immediate values
  - Missing virtual halt instruction
  - Syntax errors
  - Program size exceeding 128 instructions

### Simulator
- Full instruction execution simulation
- Register file with 32 registers
- Memory simulation with pre-defined memory locations (0x00010000 to 0x0001007c)
- Detailed state tracking:
  - Program Counter (PC)
  - Register values
  - Memory contents
- Support for signed and unsigned operations
- Binary-decimal-hexadecimal conversion utilities

## Prerequisites
- Python 3.x

## Usage

### Assembler
```bash
python assembler.py <input_file> <output_file>
```
The assembler reads RISC-V assembly code from the input file and generates binary machine code in the output file.

### Simulator
```bash
python simulator.py <input_file> <output_file>
```
The simulator reads the binary machine code and produces detailed execution logs including PC, register, and memory states.

## Register Set
The assembler and simulator support the standard RISC-V register set:
- `zero` (x0): Hardwired zero
- `ra` (x1): Return address
- `sp` (x2): Stack pointer
- `gp` (x3): Global pointer
- `tp` (x4): Thread pointer
- `t0-t6` (x5-x7, x28-x31): Temporary registers
- `s0/fp` (x8): Saved register/Frame pointer
- `s1-s11` (x9, x18-x27): Saved registers
- `a0-a7` (x10-x17): Function arguments/results

## Memory Layout
- Data memory starts at address 0x00010000
- Memory is word-aligned (4-byte blocks)
- Available memory range: 0x00010000 to 0x0001007c (32 words)

## Program Constraints
- Maximum 128 instructions per program
- Programs must end with a virtual halt instruction (`beq zero, zero, 0`)
- All immediate values must be within their respective ranges:
  - I-type: -2048 to 2047
  - B-type: -32768 to 32767
  - U-type/J-type: -1048576 to 1048575

## Output Format

### Assembler Output
- One binary instruction per line
- 32-bit instructions in binary format

### Simulator Output
- Program state after each instruction:
  - Program Counter (binary)
  - Register values (binary)
  - Final memory dump (hexadecimal addresses with binary values)

## Error Handling
The assembler performs extensive error checking including:
- Invalid instruction syntax
- Unknown instructions
- Invalid register names
- Out-of-range immediate values
- Missing halt instruction
- Program size violations

## Example Program
```assembly
# Simple program to add two numbers
addi t0, zero, 5    # Load 5 into t0
addi t1, zero, 3    # Load 3 into t1
add t2, t0, t1      # Add t0 and t1, store in t2
sw t2, 0(sp)        # Store result in memory
beq zero, zero, 0   # Halt
```

## Implementation Notes
- The assembler uses a two-pass approach:
  1. First pass: Label resolution
  2. Second pass: Instruction encoding
- The simulator implements a fetch-execute cycle
- All arithmetic operations support signed numbers
- Memory operations are word-aligned

## Limitations
- No floating-point support
- No system calls or interrupts
- Limited memory space
- No support for pseudo-instructions
- Maximum 128 instructions per program
