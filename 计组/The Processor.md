# 4-1 Introduction
## CPU performance factors
- Instruction count: determined by ISA and compiler
- CPI and Cycle time: determined by CPU hardware
## Overview of implementation
- Step1: Fetch the instruction from the memory
- Step2: Decode and read register
- Step3: ALU operation
- Step4: Send PC to the code memory
- Step5: Read one or two register
- ![[Pasted image 20230523094956.png]]
# 4.2 Logic Design Convention
- ommited
# 4.3 Building a Datapath
## Instruction executeion in RISC-V
### Fetch
- take instructions from the instruction memory
- modify PC to point the next instruction
### Instruction decoding & Read Operand
- translate into machine control command
- read register operands, whether or not to use
### Executive Control
- Control the implementation of the corresponding ALU operation
### Memory access
- Write or Read data from memory
- only ld/sd/lw/sw.etc
### Write results to register
- if R-type, ALU results are written to rd
- if I-type, instructions,memory data are written to rd
### Modify PC
- for branch instructions
## Full Datapath
- ![[Pasted image 20230528122554.png]]
# 4.4 A simple Implementation Scheme
## Signales
- 7+4
- RegWrite: decide whether write into register or not
- ALUSrc: decide the source of second operand: register 2 or immediate
- Branch: decide the next pc
- Jump: decide PC+4/branch tarrget or jump
- MemRead
- MemWrite
- MemtoReg: from alu or data memory or pc+4
## Decoder
- 2-lever decoder
- first level: ALUOp![[Pasted image 20230528144533.png]]
- second level: ALU control![[Pasted image 20230528145010.png]]
# 4.5 An overview of pipelining 
## Stages
- IF: Instruction fetch from memory
- ID: Instruction decode& register read
- EX: Execute operation or calculate address
- MEM: Access memory operand
- WB: Write result back to register
## Pipeline Speedup
- If not balanced, speedup is less
- Speed up due to increased throught
- Latency(time for each instruction) doesn't decrease
## Pipelining and ISA Design
- All instructions are 32-bits
- Few and regular instruction formats
- Load/Store addressing: Can calculate address in 3rd stage, access memory in 4th stage
## Hazards
- overview
- Structure hazards: a required resource is busy
- Data hazards
- Control hazards
# 4.6 RISC-V Pipelined Datapath
## Pipeline registers
- To hold information produced in previous cycle
- Hold what?
1. Previous Stage: data pass from ahead and data computed
2. Next Stage: data needed
## Single-clock-cycle
- show pipeline usage in a single cycle
- highlight resources used
## Multi-clock-cycle
- graph of operation over time
- here on column is the single-clock cycle
## Structure hazards
- A required resource is busy
# 4.7 Data hazards
## Condition
1. EX/MEM.rd = ID/EX.rs1/rs2
2. MEM/WB.rd= ID/EX.rs1/rs2
3. EX/MEM.regwrite/ MEM/WB.regwrite = 1
4. rd != x0
- new datapath
## Double Data Hazard
- when conflict between ex and mem
- only mem when ex is wrong
- condition for mem hazard: 
- $$ \begin{flalign} 
& if(MEM/WB.RegWrite\\
& and\space  (MEM/WB.RegisterRd \neq 0)\\ 
& and\space not(EX/MEM.RegWrite\space and(EX/MEM.RegisterRd\neq 0)\\ 
& \space \space \space and(MEM/WB.RegisterRD=ID.EX.RegisterRs1))\\
& and(MEM/WB.RegisterRd=ID/EX.RegisterRs2))\\
& ForwardA=01
\end{flalign} $$
- 01: The ALU operand is forwarded from data memory or an earlier ALU result, the fomula above shows the second situation
## Load-Use Hazard Detection
$$\begin{flalign}ID/& EX.MemRead and\\
& ((ID/EX.RegisterRd=IF/ID.RegisterRs1 or\\
& (ID/EX.RegisterRd=IF/ID.RegisterRs2))\end{flalign}$$
- If detected, stall and insert bubble
## How to Stall the Pipeline
### Force control values in ID/EX register to 0
- EX,MEM and WB do nop(no-operation), because duplicate operation has been done before
- and the set won't harm previous operation because previous control has passed down to EX/MEM register
### Prevent updata of PC and IF/ID register
- Using instruction is decoded again
- Following instruction is fetched again
- 1-cycle stall allows MEM to read data for ld, and subsequently forward to EX stage
## Stalls and Performance
- Stalls reduce performance
- Compiler can arrange code to avoid hazards
# 4.8 Branch Hazards
## Reducing Branch Delay
- Move hardware to determine outcome to ID stage
- target address adder
- register comparator
## Dynamic Branch Prediction
- 2-bit predictor: only change predicion on two successive mispredictions
- ![[Pasted image 20230623180256.png]]
- ![[Pasted image 20230623180303.png]]

# 4.10 Instruction-Level Parallelism(ILP)
## To increase ILP
### Deeper pipeline
- less work per stage-> shorted clock cycle
### Multiple issue
- Replicate pipeline stages-> multiple pipelines
- Start multiple instructions per clock cycle
- CPI < 1, use IPC
- Dependencies reduce this in practice
## Multiple Issue
### Static multiple issue
### Dynamic multiple issue
## Speculation
### Definition
- start operation as soon as possible
- check whether guess was right, if so, complete the operation, if not, roll-back and do the right thing
### Process
- Predict branch and continue issuing: don't commit until branch outcome determined
- Load speculation
### Compiler/Hardware Speculation
### Static speculation
### Dynamic speculation
## Static Multiple Issue
### Compiler groups instructions into "issue packets"
- Group of instructions that can be issued on a single cycle
- Determined by pipeline resources required
### Think of an issue packet as a very long instruction
- Specifies mutiple concurrent operation
- VLIW
## Scheduling Static Multiple Issue
### Compiler must remove some/all hazards
- Reorder instructions into issue packets
- No dependencies with a packet
- Possibly some dependencies between packets
- Pad with nop if necessary
## RISC-V with Static Dual Issue
- Two-issue packets
- Hazards
- Example
- Loop Unrolling: use rename
## Dynamic Multiple Issue
### Characteristc
- Superscaler processors
- CPU decides whether to issue 0,1,2... each cycle->avoid structural and data hazards
- Avoids the need for compiler scheduling->by cpu
### Dynamic Pipeline Scheduling
- allow the cpu to execute instructions out of order to avoid stalls
### Dynamically scheduled CPU
![[Orga_Ch4_Risc-v_Part2_v1.1.pdf - Adobe Acrobat Pro DC (32-bit) 2023_6_23 19_21_09.png]]
### Register Renaming
## Why Do Dynamic Scheduling
- not all stalls are predicable
- can't always schedule around branches
- different implementatons of an ISA have different latencies and hazards
