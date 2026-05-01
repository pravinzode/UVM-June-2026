
# SystemVerilog Testbench – 10 Solved Exercises (Minimal Architecture)

## 📌 Overview
This repository demonstrates **SystemVerilog Testbench Architecture (without UVM)** using:
- Interface
- Transaction
- Generator
- Driver
- Monitor
- Scoreboard

All examples follow a **reusable verification pattern**.

---

## 🧱 Common Architecture

Generator → Driver → Monitor → Scoreboard

---

# ✅ Exercise 1: 4-bit Subtractor

```systemverilog
module subtractor(input logic [3:0] a, b,
                  output logic [4:0] diff);
  assign diff = a - b;
endmodule

interface sub_if;
  logic [3:0] a, b;
  logic [4:0] diff;
endinterface

class transaction;
  rand bit [3:0] a, b;
  bit [4:0] diff;
endclass

class generator;
  function transaction generate();
    transaction tr = new();
    tr.randomize();
    return tr;
  endfunction
endclass

class driver;
  virtual sub_if vif;
  function new(virtual sub_if vif); 
    this.vif = vif; 
  endfunction
  task drive(transaction tr);
    vif.a = tr.a; vif.b = tr.b; #10;
  endtask
endclass

class monitor;
  virtual sub_if vif;
  function new(virtual sub_if vif); 
    this.vif = vif; 
  endfunction
  function transaction collect();
    transaction tr = new();
    tr.a=vif.a; 
    tr.b=vif.b; 
    tr.diff=vif.diff;
    return tr;
  endfunction
endclass

class scoreboard;
  function void check(transaction tr);
    if (tr.diff != (tr.a - tr.b)) $display("ERROR");
    else $display("PASS");
  endfunction
endclass

module tb;
  sub_if vif();
  subtractor dut(vif.a,vif.b,vif.diff);
  generator g; driver d; monitor m; scoreboard s;

  initial begin
    g=new(); 
    d=new(vif); 
    m=new(vif); 
    s=new();
    
    repeat(5) begin
      transaction tr;
      
      tr=g.generate(); 
      d.drive(tr); 
      tr=m.collect(); 
      s.check(tr);
    end
    $finish;
  end
endmodule
```
---

# ✅ Exercise 2: 2:1 Multiplexer

```systemverilog
module mux(input logic a,b,sel, output logic y);
  assign y = sel ? b : a;
endmodule

interface mux_if;
  logic a,b,sel,y;
endinterface

class transaction;
  rand bit a,b,sel;
  bit y;
endclass

class generator;
  function transaction generate();
    transaction tr=new(); tr.randomize(); return tr;
  endfunction
endclass

class driver;
  virtual mux_if vif;
  function new(virtual mux_if vif); 
    this.vif=vif; 
  endfunction
  task drive(transaction tr);
    vif.a=tr.a; 
    vif.b=tr.b; 
    vif.sel=tr.sel; 
    #10;
  endtask
endclass

class monitor;
  virtual mux_if vif;
  function new(virtual mux_if vif); 
    this.vif=vif; 
  endfunction
  
  function transaction collect();
    transaction tr=new();
    tr.a=vif.a; 
    tr.b=vif.b; 
    tr.sel=vif.sel; 
    tr.y=vif.y;
    return tr;
  endfunction
endclass

class scoreboard;
  function void check(transaction tr);
    if (tr.y != (tr.sel ? tr.b : tr.a)) $display("ERROR");
    else $display("PASS");
  endfunction
endclass

module tb;
  mux_if vif();
  mux dut(vif.a,vif.b,vif.sel,vif.y);
  generator g; 
  driver d; 
  monitor m; 
  scoreboard s;

  initial begin
    g=new(); 
    d=new(vif); 
    m=new(vif); 
    s=new();
    repeat(5) begin
      transaction tr;
      tr=g.generate(); 
      d.drive(tr); 
      tr=m.collect(); 
      s.check(tr);
    end
    $finish;
  end
endmodule
```
---
# Template (Use for Remaining 8 Exercises)
- Ust replace DUT + logic in scoreboard
# ✅ Exercise 3: Comparator 

```systemverilog
module comp(input logic [3:0] a,b,
            output logic gt,eq,lt);
  assign gt = (a>b);
  assign eq = (a==b);
  assign lt = (a<b);
endmodule
```
- Scoreboard logic  
```systemverilog
if ((tr.a>tr.b && !tr.gt) ||
    (tr.a==tr.b && !tr.eq) ||
    (tr.a<tr.b && !tr.lt))
  $display("ERROR");
```
---

# ✅ Exercise 4: Parity Generator  
```systemverilog
module parity(input logic [7:0] data,
              output logic p);
  assign p = ^data;
endmodule
```
- Scoreboard logic 
```systemverilog
if (tr.p != ^tr.data) $display("ERROR");
```
---
# ✅ Exercise 5: ALU 

```systemverilog
module alu(input logic [3:0] a,b,
           input logic [1:0] op,
           output logic [4:0] y);
  always_comb begin
    case(op)
      0: y=a+b;
      1: y=a-b;
      2: y=a&b;
      3: y=a|b;
    endcase
  end
endmodule
```
---
# ✅ Exercise 6: Counter 

```systemverilog
module counter(input logic clk,
               output logic [3:0] count);
  always_ff @(posedge clk)
    count <= count + 1;
endmodule
```
---
# ✅ Exercise 7: FIFO (Concept) 

```systemverilog
// Scoreboard using queue
queue.push_back(data_in);
queue.pop_front();
```
---

# ✅ Exercise 8: Shift Register 

```systemverilog
module shift(input logic clk, in,
             output logic [3:0] out);
  always_ff @(posedge clk)
    out <= {out[2:0], in};
endmodule
```
---
# ✅ Exercise 9: Priority Encoder 

```systemverilog
module encoder(input logic [7:0] in,
               output logic [2:0] out);
  always_comb begin
    casex(in)
      8'b1xxxxxxx: out=7;
      8'b01xxxxxx: out=6;
      default: out=0;
    endcase
  end
endmodule
```
---
# ✅ Exercise 10: FSM(Traffic Light) 

```systemverilog
module fsm(input logic clk,
           output logic [1:0] state);
  always_ff @(posedge clk)
    state <= state + 1;
endmodule
```
---
