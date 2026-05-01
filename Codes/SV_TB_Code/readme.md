
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
---
## 🏗️ Testbench Architecture
- The testbench is divided into the following components:
### 1. Interface
- Connects DUT and testbench
- Avoids messy wiring

interface adder_if;
  logic [3:0] a, b;
  logic [4:0] sum;
endinterface
2. Transaction
Represents a single test case
Encapsulates input/output data
class transaction;
  rand bit [3:0] a, b;
  bit [4:0] sum;
endclass
3. Generator
Creates randomized inputs
class generator;
  transaction tr;

  function transaction generate();
    tr = new();
    tr.randomize();
    return tr;
  endfunction
endclass
4. Driver
Applies inputs to DUT
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
5. Monitor
Observes DUT signals
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
6. Scoreboard
Checks correctness of output
class scoreboard;

  function void check(transaction tr);
    if (tr.sum != (tr.a + tr.b))
      $display("ERROR: %0d + %0d != %0d", tr.a, tr.b, tr.sum);
    else
      $display("PASS: %0d + %0d = %0d", tr.a, tr.b, tr.sum);
  endfunction

endclass
7. Top Testbench
Connects all components
module tb;

  adder_if vif();

  adder dut(.a(vif.a), .b(vif.b), .sum(vif.sum));

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

      tr = gen.generate();
      drv.drive(tr);
      tr = mon.collect();
      sb.check(tr);
    end

    $finish;
  end

endmodule

