# Development
## Von Neumann architecture
- Computation and memory are separeated
- Memory that stores data and instructions
- Input and output mechanisms
- Instruction set architecture
## Computer
- Electronic realization
- A set of instructions in a well-defined manner->general-purpose
- Execution of a pre-recorded list of instructions->program-controlled
- Memory that can store instructions and data->stored program
- Ruring-complete in theory->equivalent to Ruring machine
# Computer organization
## Software
### Application software
### System software
- Operation system
- Compiler
- Firmware
## Hardware
### CPU
- Control unit
- Datapath
### Memory
### I/O interface
- Input
- Bidirectional
- Output
# Build processors
## Calculation
- Cost per ide = $$ \frac{Cost\:pre\:wafer}{Dies\:per\: wafer*Yield}$$
- Dies per wafer = wafer area/Die area
- Yield = $$\frac{1}{(1+(Defects\: per\: area*Die\: area/2))^{2}}$$
# Computer design
## Response Time and Throughput
- Reponse time/execution time
- Throughput(bandwidth)
- Impact factor
## Relative Performance
- Performance
- n time faster
## Measuring Execution time
### Elapsed time
- Processing
- I/O
- Idle time
- OS overhead
### CPU Time
### Clock
- Clock period
- Clock frequency
## Fomula
### Clock
- CPU Time = CPU Clock Cycles $\times$ Clock Cycle Time = $\frac{CPU\:Clock\:Cycles}{Clock\:Rate}$
- Improve ways
### Instruction Count and CPI
- $Clock\:Cycles=Instruction\:count\times{Cycles\:Per\:Instruction}$
- $CPU\:Time=Instruction\:Count\times{CPI}\times{Clock\:Cycle\:Time}$ = $\frac{Instruction\:Count\times{CPI}}{Clock\:Rate}$
- Impact factors
### CPI in More Detail
- $Clock\:Cycles=\sum_{i=1}^{n}{(CPI_{i}\times{Instruction\:Count_{i}})}$
- $CPI=\frac{Clock\:Cycles}{Instruction\:Count}=\sum_{i=1}^{n}{(CPI_{i}\times{\frac{Instruction\:Count_{i}}{Instruction\:Count}})}$
### Performance summary
- $CPU\:Time=\frac{Instructions}{Program}\times{\frac{Clock\:cycles}{Instruction}}\times{\frac{Seconds}{Clock\:cycle}}$
- Depends on

## Multiprocessors
- Benchmark
- Power Benchmark
- Amdahl's Law: $$T_{improved}=\frac{T_{affected}}{improvement\:factor}+T_{unaffected}$$
- MIPS: Millions of Instructions Per Second

## Eight Great Ideas
- Design for moore's Law
- Use Abstraction to Simplify Degign
- Make the Common Case Fast
- Performance via Parallelism
- Performance via PipeLining
- Performance via Prediction
- Hierarchy of Memories
- Dependability via Redundancy