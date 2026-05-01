
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
  function new(virtual sub_if vif); this.vif = vif; endfunction
  task drive(transaction tr);
    vif.a = tr.a; vif.b = tr.b; #10;
  endtask
endclass

class monitor;
  virtual sub_if vif;
  function new(virtual sub_if vif); this.vif = vif; endfunction
  function transaction collect();
    transaction tr = new();
    tr.a=vif.a; tr.b=vif.b; tr.diff=vif.diff;
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
    g=new(); d=new(vif); m=new(vif); s=new();
    repeat(5) begin
      transaction tr;
      tr=g.generate(); d.drive(tr); tr=m.collect(); s.check(tr);
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
  function new(virtual mux_if vif); this.vif=vif; endfunction
  task drive(transaction tr);
    vif.a=tr.a; vif.b=tr.b; vif.sel=tr.sel; #10;
  endtask
endclass

class monitor;
  virtual mux_if vif;
  function new(virtual mux_if vif); this.vif=vif; endfunction
  function transaction collect();
    transaction tr=new();
    tr.a=vif.a; tr.b=vif.b; tr.sel=vif.sel; tr.y=vif.y;
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
  generator g; driver d; monitor m; scoreboard s;

  initial begin
    g=new(); d=new(vif); m=new(vif); s=new();
    repeat(5) begin
      transaction tr;
      tr=g.generate(); d.drive(tr); tr=m.collect(); s.check(tr);
    end
    $finish;
  end
endmodule
```
---



