# Random Access Machine

A Random Access Machine (RAM) consists of the following components:

- (Main) Memory: $s$ cells of storage, each cell can store 64 bits of data.
- A constant number of register (often 8): where RAM can perform operations on data.
- A set of $l = O(1)$ allowed machine instruction:
  - Write the value currently stored in a given register to a specific location in Main Memory.
  - Read the value from a specific location in Main Memory into a register.
  - Perform basic manipulations of data in registers.
- A program counter: tells the machine what is the next instruction to execute.
