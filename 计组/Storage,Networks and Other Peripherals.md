# A1 Introduction
## Overview
- ![[Orga_Ch6_Risc-v_V1.1.pdf - Adobe Acrobat Pro DC (32-bit) 2023_6_24 10_33_02.png]]
## Characters
- Behavior: input,output,storage
- Partner: human machine
- Data rate
## Performance Messure
### Throughput:
1. how much data in a certain time
2. how many operations in a certain time
### Reponse time
## Amdahl's law
- Sequential part can limit speedup
# A.2 Disk Storage and Dependability
## Time
- seek
- rotational latency
## Behavior
- disk controller: control the transfer between the disk and the memory
- Access time = seek time+ rotational latency+ transfer time+ controller time
## Measure
- MTTF: mean time to failure
- MTTR: mean time to repair
- MTBF: mean time between failures = MTTF+MTTR
- Availability = MTTF/MTBF
### Ways to improve MTTF
- Fault avoidance: by construction
- Fault tolerance: by redundancy
- Fault forecasting
## Array of small disks
### Reliablility
- Reliability of N disks = Reliability of 1 Disk / N
### RAID
- redundant arrays of inexpensive disks
## RAID 0
- No redundancy
## RAID 1
- Disk mirroring/shadowing
## RAID 3
- Bit-Interleaved Parity Disk
- if failed, must read all data from all disks
## RAID 4
- Block-Interleaved Parity
- small write algorithm
## RAID 5
## RAID 6
# A.4 Buses and Other Connections 
## Bus Basics
### Lines
- control lines
- data lines
### Bus transaction
- sending the address
- receiving or sending the data
### Types of buses
- processor-memory
- backplane
- I/O
- ![[Orga_Ch6_Risc-v_V1.1.pdf - Adobe Acrobat Pro DC (32-bit) 2023_6_24 10_33_02 1.png]]
## Synchronous vs Asynchronous
### Asynchronous example
- ![[Orga_Ch6_Risc-v_V1.1.pdf - Adobe Acrobat Pro DC (32-bit) 2023_6_24 12_05_25.png]]
- ![[Orga_Ch6_Risc-v_V1.1.pdf - Adobe Acrobat Pro DC (32-bit) 2023_6_24 12_05_25 1.png]]
- Desciption
0. Processor->rise readreq->put address on data line
1. Memory->get readreq signal then rise ack-> read address
2. IO->see the ack rise->lower readreq->drop data on data line
3. Memory->see readreq lower->lower ack
4. Memory->rise datardy->load data on data line
5. IO->get datardy signal then rise ack->read data
6. Memory0>see the ack rise->lower datardy->drop data on data line
7. IO--> see datardy lower->lower ack
## Bus Arbitration
### Choosing which device
- bus priority
- fairness
## Performance
### Calculate
- Asynchronous
- Synchronous
### Increasing the Bus BandWidth
- 4-word block transfers
- 16-word block transfers
1. increase data bus width
2. use separate address and data lines
3.  tranfer multiple words
# A5 Interfacing I/O Devices
## Communication with the processor
- Polling
- Interrupt
- DMA(direct memory access)
# A6 I/O Performance Measures
