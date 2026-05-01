
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
