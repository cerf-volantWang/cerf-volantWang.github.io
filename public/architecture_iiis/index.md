# Computer Architecture


This lecture is presented by [Mingyu Gao](https://people.iiis.tsinghua.edu.cn/~gaomy/) in Fall 2023.

Thanks to 唐添 for discussing with me.

## Introduction

## System Evaluation Metrics

## RISC-V ISA and Assembly

## RISC-V Encoding and Vector Extension

## Processor: Single-Cycle & Pipelined

10-24-2023

After discussing the structure of RISC-V instructions, it is time to consider how to build a RISC-V processor. 

> ISA is a specification of functionality, and now we are going to build a processor to implement such functionality.


What I am interested is:
1. common design across different ISAs
2. what's different about RISC-V processor, i.e. benefitials?
    - RISC vs. CISC tradeoff
    - MIPS vs. RISC-V

### Review: Digital Logic Design
Key elements:
+ Gates: AND, OR, NOT, ...
+ Basic blocks: multiplexer (MUX), encoder/decoder, arithmetic/logic unit (ALU), ...
+ Simple state: latches, filp-flops, registers
+ Synchronous memories: SRAM

Clocking methodology of sequential circuits — interactions between *State elements* and *combinational logic*
- State elements store the current states (data, address, control signals, ...)
- Combinational logic calculates new states in each clock cycle

### A Single-Cycle Processor

We will focus on a simple one first and later optimize for performance (even starting from correcting mistakes).

A single-cycle processor
+ Execute one instruction to completion before moving to the next one
+ Execute one instruction within one clock cycle, i.e., CPI = 1
+ a subset of the RISC-V instructions
    1. Arithmetic (R,I): `add`, `sub`, `addi`, `ori`
    2. Memory (I,S): `lw`, `sw`
    3. Branch/jump (B,J): `beq`, `j`

Our Approach
Generally speaking, a processor consists of two parts:
+ Datapath: the hardware that processes and stores data
+ Control: the hardware that manages the datapath

Hardware Components
+ State elements: PC register, a 32-entry register file, memory
    + Logically separate memories for instructions and data
    + But physically can be the same one (or view them as caches)
    + Recall the Von-Neuman's architecture!
+ Combinational logic (to update PC/regs/memory): ALU, MUX
+ Control logic: customized combinational circuits

To make things easier, break instruction execution into simple steps:
1. **Fetch** an instruction from memory specified by PC and update the PC
2. **Decode** the instruction and read operands from registers
3. **Execute** an operation using an ALU
4. **Load/Store** a value from/to memory if needed
5. **Store** the result to a register or memory

Questions:
1. in **Fetch** step, is the instruction in memory (why not cache)? And how can we update PC immediately?
2. Why is **Load/Store** after ALU execution, i.e. **Execute** step?
    + Perhaps we are calculating address in **Execute** step
3. How does RISC help with faster fetch and decode?

