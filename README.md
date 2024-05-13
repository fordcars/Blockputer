# Blockputer
8-bit Minecraft computer built using redstone. Also see [assembler](https://github.com/fordcars/BlockputerASM) and [virtual machine](https://github.com/fordcars/BlockputerVM) for easier program development.

**Note:** This project was purely for fun and to learn more about CPU architectures. Even though it is fully functional, it is so excessively slow that it has no real-world use. However, since it does not use any fancy Minecraft features, and is built solely using redstone, torches and repeaters, it is *relatively* easy to understand and could be a good reference for understanding how a basic 8-bit computer functions.

![Screenshot](https://github.com/fordcars/Blockputer/blob/main/misc/overview.png?raw=true)

## Features
* Built only using redstone (no moving parts or command blocks)
* Harvard architecture with accumulator design
* 16-instruction ISA, including 8 ALU operations
* Conditional jumping
* 9 general purpose registers
* 256-byte ROM
* Support for 256-byte RAM (not yet implemented)
* Program-blocking user input
* 1-byte decimal output
* Most-importantly, **ultra slow!!!**

## Getting Started
The provided Minecraft save file includes a demo program (Fibonacci). Simply load the save and press the `Run/Continue` button on the user interface. The program will request a number of iterations to calculate, and will then print each value of the Fibonacci sequence until the specified number of iterations is met. See [fibonacci.txt](https://github.com/fordcars/BlockputerASM/blob/main/test_files/fibonacci.txt) for source (assembly).

It is a good idea to set your render distance and simulation distance to at least 20 chunks to make sure all chunks are simulated correctly. You should also press the `Force chunk loading` button on the interface (next to the map) before running the computer to force load all relevant chunks.

Programs are written using redstone torches on the ROM lines. For simplicity, it's advisable to write your program in assembly, and then convert it into machine code using the [assembler](https://github.com/fordcars/BlockputerASM). Then, you can transcribe the result using torches in Minecraft.

**Note:** This computer is sloooowwwwwww. For example, calculating 3 fibonacci numbers takes a couple minutes using the demo program. I'm sure the computer could be greatly optimized, but I'm honestly never gonna bother :')

## Instruction Set Architecture
### Instruction Format

| Bits 7:4 | Bits 3:0 |
| --- | --- |
| Opcode | Operand |

### Instruction Set

| Mnemonic | Opcode | Operand (if present) | Description |
| -------- | ------ | ----------- | -------------------- |
| MVRA     | 0000   | Register id | `ACC` = reg |
| MVAR     | 0001   | Register id | reg = `ACC` |
| STA      | 0010   |  | `M[MEMA]` = `ACC` |
| LDA      | 0011   |  | `ACC` = `M[MEMA]` |
| JUMPN    | 0100   |  | Jump to `INSTA` if `ACC` is negative. |
| JUMPZ    | 0101   |  | Jump to `INSTA` if `ACC` is zero. |
| MVAH     | 0110   | Immediate (4-bits) | `ACC[7:4]` = immediate |
| MVAL     | 0111   | Immediate (4-bits) | `ACC[3:0]` = immediate |
| MUL      | 1000   | Register id | `ACC` = `ACC` * reg |
| SUB      | 1001   | Register id | `ACC` = `ACC` - reg |
| ADD      | 1010   | Register id | `ACC` = `ACC` + reg |
| LLS      | 1011   | Register id | `ACC` = `ACC` << reg, (filled with zeros) |
| LRS      | 1100   | Register id | `ACC` = `ACC` >> reg, (no sign extension) |
| AND      | 1101   | Register id | `ACC` = `ACC` & reg |
| OR       | 1110   | Register id | `ACC` = `ACC` \| reg |
| XOR      | 1111   | Register id | `ACC` = `ACC` ^ reg |

### Registers

| Name  | Id   | Description |
| ----  | ---- | ----------- |
| R0    | 0000 | General purpose |
| R1    | 0001 | General purpose |
| R2    | 0010 | General purpose |
| R3    | 0011 | General purpose |
| R4    | 0100 | General purpose |
| R5    | 0101 | General purpose |
| R6    | 0110 | General purpose |
| R7    | 0111 | General purpose |
| R8    | 1000 | General purpose |
| OUT   | 1001 | Prints to display. |
| IN    | 1010 | Halts program and waits for user input. |
| MEMA  | 1011 | STA/LDA RAM address |
| INSTA | 1100 | Jump destination |
| ZERO  | 1101 | Constant (0) |
| ONE   | 1110 | Constant (1) |
| MIN1  | 1111 | Constant (-1 or 255) |

## Screenshots
### Top-down View
![Top-down View](https://github.com/fordcars/Blockputer/blob/main/misc/topdown.png?raw=true)

### User Interface
![User interface](https://github.com/fordcars/Blockputer/blob/main/misc/input.png?raw=true)

### ROM
![ROM](https://github.com/fordcars/Blockputer/blob/main/misc/ROM.png?raw=true)

### Register File
![Register File](https://github.com/fordcars/Blockputer/blob/main/misc/register_file.png?raw=true)

### ALU
![ALU](https://github.com/fordcars/Blockputer/blob/main/misc/ALU.png?raw=true)