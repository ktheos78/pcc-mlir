# pcc - picoC Compiler

## About

Compiler for a simple subset of C (picoC) implemented with Polygeist and xDSL, targetting ARM architectures.

## Usage

`./pcc.py [--emit-all] <filename>.c`



**IMPORTANT NOTE**: The environment variable `CGEIST_PATH` must be set to your Polygeist installation's ./bin/ directory in order to use the program:

`export CGEIST_PATH=~/Documents/Polygeist/build/bin`

## Implementation

The compilation pipeline is as follows:
- Polygeist turns the input \*.c file into high-level MLIR (\*.mlir)
- The backend applies optimizations to the high-level MLIR code like Dead Code Elimination (DCE), Common Subexpression Elimination (CSE), and various other peephole optimizations (`backend_optimization.py`)
- The backend lowers the high-level MLIR code into a custom ARM dialect (`backend_arm-dialect.py`)
- Finally, the ARM MLIR code is printed as (usable!) ARM assembly into a .s file (`backend_printer.py`)

## Requirements

- xDSL
- Polygeist

## Additional Notes

The compiler currently supports multiple functions per file, and functions with parameters passed to them (the ARM calling convention is followed). The target subset of C is currently only arithmetic operations, with support for control flow soon to be added.