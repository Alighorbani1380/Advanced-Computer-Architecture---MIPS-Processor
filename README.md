# Advanced Computer Architecture - MIPS Pipeline Processor Implementation

This repository contains my solutions to the advanced computer architecture exercises for the first semester of 1403-1404 at the University of Tehran. The project includes Verilog implementations and comprehensive reports for each exercise, focusing on building a MIPS pipeline processor and handling data and control hazards.

## Project Overview

### Exercise 1: Single-Cycle MIPS Processor
In the first exercise, a single-cycle MIPS processor was designed to execute instructions using Verilog. Key features implemented include:
- **Instruction Execution**: Support for basic MIPS instructions in a single-cycle format.
- **Hazard Management**: Basic methods to address data and control hazards using `NOP` instructions.
- **Testing**: A custom MIPS assembly program was developed to find the largest element in a signed integer array of 32-bit integers. The program was converted to machine code and used to test the processor functionality.

### Exercise 2: Pipelined MIPS Processor
Building on the single-cycle design, the second exercise introduces pipelining to improve processor performance. This includes:
- **Pipeline Stages**: A 5-stage pipeline architecture with Fetch, Decode, Execute, Memory, and Write-back stages.
- **Hazard Detection and Forwarding**: Hardware-based detection of data and control hazards, using advanced mechanisms to maintain efficiency in the pipeline.
  
#### Hazard Control Methods
To ensure the processor handles hazards correctly, the following control methods were implemented:
  - **Data Forwarding (Bypassing)**: When a dependent instruction requires data that is not yet written back, data forwarding routes the required value from the appropriate pipeline stage. This prevents unnecessary stalls.
  - **Stalling**: In cases where data forwarding cannot resolve a dependency, the pipeline is stalled, preventing the Fetch and Decode stages from progressing until the required data is available.
  - **Control Hazard Handling (Flush)**: For branch instructions, control hazards are handled by flushing instructions in the pipeline that are fetched speculatively but should not be executed. This is managed by the use of control signals to clear the pipeline stages selectively.
  - **Speculative Execution**: Speculation is applied to reduce the performance cost of control hazards. When a branch instruction is encountered, the processor speculatively fetches and begins executing the next instructions, assuming the branch will not be taken. If the speculation is incorrect, the pipeline flushes the speculative instructions and continues with the correct branch path. This approach reduces stalls while managing the risk of incorrect predictions.

- **Testing and Validation**: The same test program from Exercise 1 was used, with verification by simulation to confirm correct data propagation and hazard handling.

## Directory Structure
- **CA1.pdf**: Problem statement for Exercise 1, including single-cycle MIPS processor requirements.
- **CA2.pdf**: Problem statement for Exercise 2, outlining the pipeline requirements and hazard handling.
- **Gozaresh.pdf**: Report detailing the design choices, Verilog code, and test results.

## Features
- **ALU Operations**: Support for basic operations (`add`, `sub`, `and`, `or`, `slt`, etc.).
- **Pipeline Registers**: Design of inter-stage pipeline registers to maintain instruction data across stages.
- **Hazard Handling**: Techniques like data forwarding, stalling, flushing, and speculation to manage dependencies and control hazards between instructions.

## Getting Started
### Prerequisites
To run this project, you’ll need:
- **Verilog Compiler**: Any Verilog-supported environment (e.g., ModelSim, Quartus).
- **Test Bench**: Use the provided machine code in `instructionmemory.txt` and `datamemory.txt` for loading into memory modules.

### Running Simulations
1. Load the Verilog files into your simulation environment.
2. Compile and run the simulation using the provided test program files.
3. Observe the pipeline registers and memory contents to verify correct processor operation.
