
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
- 👉 Replaces messy wire connections
### 2. Transaction (data packet)
- Represents a single test case
- Encapsulates input/output data
 ```systemverilog
class transaction;
  rand bit [3:0] a, b;
  bit [4:0] sum;
endclass
```
- 👉 Instead of individual signals, we use one object
  
### 3. Generator (creates inputs)
```systemverilog
class generator;
  transaction tr;

  function transaction generate();
    tr = new();
    tr.randomize();   // automatic test generation
    return tr;
  endfunction
endclass
```
-👉 No need to manually write test cases

### 4. Driver (applies inputs to DUT)
```systemverilog
class driver;
  virtual adder_if vif;

  function new(virtual adder_if vif);
    this.vif = vif;
  endfunction

  task drive(transaction tr);
    vif.a = tr.a;
    vif.b = tr.b;
    #10;
  endtask
endclass
```
### 5. Monitor (observes output)
```systemverilog
class monitor;
  virtual adder_if vif;

  function new(virtual adder_if vif);
    this.vif = vif;
  endfunction

  function transaction collect();
    transaction tr = new();
    tr.a = vif.a;
    tr.b = vif.b;
    tr.sum = vif.sum;
    return tr;
  endfunction
endclass
```
### 6. Scoreboard (checks correctness of output )
```systemverilog
class scoreboard;

  function void check(transaction tr);
    if (tr.sum != (tr.a + tr.b))
      $display("ERROR: %0d + %0d != %0d", tr.a, tr.b, tr.sum);
    else
      $display("PASS: %0d + %0d = %0d", tr.a, tr.b, tr.sum);
  endfunction

endclass
```
### 7. Top Testbench (Connects all components)
```systemverilog
module tb;

  adder_if vif();
//DUT Instance 
  adder dut(.a(vif.a), .b(vif.b), .sum(vif.sum));
// components 
  generator gen;
  driver drv;
  monitor mon;
  scoreboard sb;

  initial begin
    gen = new();
    drv = new(vif);
    mon = new(vif);
    sb  = new();

    repeat (5) begin
      transaction tr;

      tr = gen.generate();   // generate stimulus 
      drv.drive(tr);         // apply- drives to DUT
      tr = mon.collect();    // observe- monitor output 
      sb.check(tr);          // verify-  checks results
    end

    $finish;
  end

endmodule
```
---


