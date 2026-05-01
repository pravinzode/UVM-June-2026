
# SystemVerilog Testbench (Minimal Architecture)

## 📌 Overview
This project demonstrates a **minimal SystemVerilog testbench architecture** without using UVM.  
It introduces structured verification concepts like generator, driver, monitor, and scoreboard in a simple and understandable way.

---

## 🎯 Objective
- Understand why SystemVerilog testbenches are used instead of simple Verilog testbenches
- Learn basic testbench components
- Implement automated testing with clean structure

---

## 🧱 Design Under Test (DUT)
### 4-bit Adder
```systemverilog
module adder(input logic [3:0] a, b,
             output logic [4:0] sum);
  assign sum = a + b;
endmodule
```
---
## 🏗️ Testbench Architecture
- The testbench is divided into the following components:
### 1. Interface 
- Connects DUT and Testbench 
- Avoids messy wiring 
```systemverilog
interface adder_if;
  logic [3:0] a, b;
  logic [4:0] sum;
endinterface
```
### 2. Transaction (data packet)
- Represents a single test case
- Encapsulates input/output data
 ```systemverilog
class transaction;
  rand bit [3:0] a, b;
  bit [4:0] sum;
endclass
```
---
