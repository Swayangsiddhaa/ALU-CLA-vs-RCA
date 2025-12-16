# 8-Bit ALU Comparative Analysis: RCA vs. CLA

![Verilog](https://img.shields.io/badge/Language-Verilog_HDL-blue)
![Tool](https://img.shields.io/badge/Tool-Xilinx_Vivado-red)
![Status](https://img.shields.io/badge/Status-Completed-success)

This repository contains the design and comparative analysis of an **8-bit Arithmetic Logic Unit (ALU)** implemented using two different adder architectures:
1.  **Ripple Carry Adder (RCA)** – Optimized for Low Area (Resource Efficient).
2.  **Carry Lookahead Adder (CLA)** – Optimized for High Speed (Performance Efficient).

The project is structured into two separate implementations to allow for distinct synthesis and timing analysis in Xilinx Vivado.

## 📂 Project Structure

To avoid module conflicts, the designs are separated into two distinct setups.

| Implementation | Description | Top Module File | Key Characteristics |
| :--- | :--- | :--- | :--- |
| **Project 1: RCA** | Uses a cascaded Full Adder structure. | `alu_8bit_rca.v` | Simple, Modular, Slower. |
| **Project 2: CLA** | Uses parallel Generate/Propagate logic. | `alu_8bit.v` | Complex, Fast, Scalable. |

## ⚙️ Supported Operations

Both ALU designs support the same set of arithmetic and logical operations, controlled by the Selection (`S`) and B-Select (`Bsel`) lines.

### 1. Arithmetic Operations (S = 000)
| Operation | Bsel | Description | Formula |
| :--- | :--- | :--- | :--- |
| **ADD** | `00` | Addition | $A + B$ |
| **SUB** | `01` | Subtraction | $A + (\sim B) + 1$ |
| **INC** | `10` | Increment | $A + 1$ |
| **DEC** | `11` | Decrement | $A - 1$ |

### 2. Logic Operations
| Operation | Selector (S) | Description |
| :--- | :--- | :--- |
| **AND** | `001` | Bitwise AND |
| **OR** | `010` | Bitwise OR |
| **XOR** | `011` | Bitwise XOR |
| **NAND** | `100` | Bitwise NAND |
| **NOT** | `101` | Bitwise NOT (Invert A) |
| **XNOR** | `110` | Bitwise XNOR |
| **NOR** | `111` | Bitwise NOR |

## 📊 Performance Analysis Results

The designs were synthesized on Xilinx Vivado (Artix-7 Family) to compare "Power, Performance, and Area" (PPA).

| Comparison Metric | Ripple Carry Adder (RCA) | Carry Lookahead Adder (CLA) | Conclusion |
| :--- | :--- | :--- | :--- |
| **Speed (Timing Slack)** | 1.636 ns | **2.160 ns** | **CLA is 32% Faster** |
| **Area (LUTs)** | **23** | 28 | **RCA is Smaller** |
| **Delay Behavior** | Linear ($O(N)$) | Logarithmic ($O(\log N)$) | CLA scales better |
| **Static Power** | 0.095 W | 0.095 W | Identical |

**Final Verdict:** The **CLA** is essential for high-speed processors where timing is critical, while the **RCA** is sufficient for low-cost, area-constrained embedded systems.

## 🚀 How to Run the Code

Since the modules share names (like `B_selection`), it is recommended to run them as **two separate Vivado projects** or independent runs.

### Option A: Running the RCA Design
1.  Create a project and add these source files:
    * `alu_8bit_rca.v` (Top Module)
    * `rca_8bit.v`
    * `full_adder.v`
    * `logic_unit.v`
    * `B_selection.v`
2.  Add the testbench: `alu_8bit_rca_tb.v`.
3.  Add the constraints: `constraints_rca.xdc`.
4.  Run **Behavioral Simulation** to check waveforms.
5.  Run **Synthesis** to verify the 23 LUT resource count.

### Option B: Running the CLA Design
1.  Create a project and add these source files:
    * `alu_8bit.v` (Top Module)
    * `cla.v`
    * `logic.v`
    * `B_selection.v`
2.  Add the testbench: `alu_8bit_tb.v`.
3.  Add the constraints: `constraints_cla.xdc`.
4.  Run **Behavioral Simulation**.
5.  Run **Synthesis** to verify the 28 LUT count and superior timing slack.

## 👥 Contributors

* **Sarbatriki Jana**
* **Soumyarup Dutta**
* **Raina Das**
* **Meesha Sinha**

**Institute:** Institute of Engineering & Management (IEM), Kolkata


