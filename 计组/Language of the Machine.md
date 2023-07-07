# 2.1 Introduction
## Language of the machine
- Instructions->Statement
- Instruction set-> Syntax
## Instruction characteristics wide variety
## Stored-program concept
- Instructions are represented as numbers
- Programs can be stored in memory to be read or written just like numbers
# 2.2 Operations of the computer hardware
## Content
- one operation per instruction
- exactly three variables
## Design Principle
- simplicity
# 2.3 Operands of the computer hardware
## General
- use register
- 32* 64-bit-register file
- from x0 to x31
- 64-bit: doubleword
- 32-bit: word
## RISC-V Register
- name/usage
## Memory Operands
### Main memory used for composite data
### Apply arithmetic operations
- Load values from memory to registers
- Store result form register to memory
### Memory is byte addressed
- Each address identifies an 8-bit byte
### RISC-V is little endian
- Least-significant byte at least address of a word：right least addr
### RISC-V doesn't require words to be aligned in memory
## Memory Alignment
- memory not register
- each read a word
## Endianness
### Big end: Left Least Addr
- Byte1:01 Byte0:02 = 02then01->8bit each->513 in decimal
### Little end: Right Least Addr
- Byte1:01 Byte0:02 ->258 in decimal
### Bi-endian
- MIPS， ARM, Alpha....
## Memory Operand Example
- Only load and store insturction can access memory
- Digit inside instruction is based byte, eg in ld or sd
- Immediate in struction's machine code is bit-bases
## Register and Memory
- Register are faster to access
- Reigister doesn't need load or store, thus feweer instructions to be executed
- Register stores variables that are frequently used, are more common in compiler than memory
## Constant or immediate Operands
- to avoid loading the constant
- constant and instruction are stored in the same space
## Brief summary
- ![[Pasted image 20230328104213.png]]
- ?
# 2.4 Signed and unsigned numbers
- omitted
# 2.5 Representing instructions in the computer
## General
### Machine code
- instructions encoded in binary
### Mapping registers into numbers
- x0 to x31-> 0 to 31
### RISC-V instructions
- Encoded as 32-bit instruction words
- All instructions in RISC-V have the same length
## R-Format Instructions
### Instruction fields
- opcode: operation code
- funct3: 3-bit function code(additional opcode)
- funct7: 7-bit function code(additional opcode)
- rd: destination register number, store the index of register
- rs1: the first source register number, store the index of register
- rs2: the second source register number, store the index of register
### structure
- ![[Pasted image 20230328200050.png]]
### Example
- add x9, x20, x21: x9 = x20 + x21
## I-Format Instructions
### Immediate arithmetic and load instructions
- rs1: addi's source or load's base address register number
- immediate: addi's constant operand or load's offset added to base address(byte)
- immediate is 2's-complement,sign extended
- these two operations only have one variable, so this structure is applicable to both operations
### structure
![[Pasted image 20230328203000.png]]
### Example
- ld x9, 64(x22)
- x22 is placed in rs1
- x9 is placed in rs2
## S-Format Instructions
### Instruction fields
- rs1: base address register number
- immediate: offset added to base address
- rs2: source: source operand register number, the number to be stored
### structure
- ![[Pasted image 20230328203656.png]]
### Example
- sd x9, 64(x22)
- 22(x22) is placed rs1
- 64 is placed immediate
- 9(x9) is placed rs2
## RISC-V instruction encoding
- ![[Pasted image 20230328203857.png]]
# 2.6 Logical operations
## Shift Operations
- immed: how many positions to shift
## And Operations
## OR Operations
## Xor Operations
# 2.7 Instructions for making decision
## Branch instructions
- beq register1, register2, L1 : if equal, jump to L1
- bne register1, register2 L1 : if not equal, jump to L1
- note that L1 is always executed, statement between L1 and this judge may be omitted
- absolutely jump
- ![[Pasted image 20230411201131.png]]
## Loops
- ![[Pasted image 20230411201838.png]]
- A is an array of 100 words, each enjoy an address
- the next address is 1 byte more than the previous, thus 8 bits
- get the address in the first two steps
## While
- ![[Pasted image 20230411202122.png]]
## Compare Operation
- slt x5,x19,x20; if x19 < x20, then x5 = 1: set on less than
## Conditional Operations
- blt rs1,rs2,L1; if rs1 < rs2, branch to L1
- bge rs1,rs2,L1: if rs1 >= rs2, branch to L1
- unsigned: btlu,bgeu
## Hold out Case/Switch
- PC : store instruction's address
- First operate on PC register's address, increasement is 8 byte, get target PC register's address; then load PC register's value, thus get instruction's address; finally use jalr, the first term is the current's next instruction's address, the second is the jump one's instruction's address
- jalr and jal:jump register& jump address table
- ![[Pasted image 20230516113101.png]]
## Basic Blocks
- No embedded branches
- No branch targets/branch labels
- used for optimization and acceleration
# 2.8 Supporting procedures in computer hardware
## Instruction for procedures
- caller: jal x1, ProcedureAddress
- callee: jalr x0, 0(x1)
## Steps
- Place parameters in a place where the prodecure can access them
- Transfer control to the prodedure
- Acquire the storage resources nedded for the procedure
- Perform the desired task
- Place the result value ina place where the calling program can access it
- Return control to the point of origin
## Leaf procedure
- a basic callee
- not a caller
## Stack
- sp
- fp
- used in caller/callee and recursion
## Register Classification
- preserved ones
- not preserved ones
- for leaf procedure
## Nested Procedure
- use venus to run fact function
## Memory layout
- from top till down
- Stack: for local variables, high to low
- Heap: for dynamic data, low to high
- Data: for static data, low to high
- Text: for code, low to high
- Reserved
# 2.9 Communicating with People Character Data
- Concepts omitted
- String copy example
# 2.10 RISC V Addressing for 32-Bit Immediate and Addresses
## Wide Bit Immediate addressing
- U-type instruction: lui
- Load a 32-bit constant: lui and addi
- ![[Pasted image 20230519080427.png]]
## Addressing in branches
- SB-type instruction: bne, use 12-bit immediate
- Target address = PC + Branch offset = PC + immediate*2
- signextension
## Jump Addressing
- UJ-type instruction: jal, use 20-bit immediate for large range
- ![[Pasted image 20230519080911.png]]
- one way: inserts an unconditional jump to target,beq->bne and jal
## Long Jumps
- beyond SB and UJ, 32-bit absolute address
- lui: load address[31:12] to temp register
- jalr: add address[11:0] and jump to target
## Branch Offset in Machine Lauguage
- All RISC-V instructions are 4 bytes long
- PC-relative addressing refers to the number of halfwords
## Addressing Ways
- Immediate addressing
- Register addressing
- Base addressing
- PC-relative addressing
## RISC-V Disassembly