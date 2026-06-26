# UVM Factory Override Example using Tea Analogy

This example demonstrates the concept of **Factory Override** in UVM.

Suppose we have two classes:

- `tea` (Parent Class)
- `ginger_tea` (Child Class)

Normally, when we create a `tea` object, the factory creates a **Basic Tea**.

Using **Factory Override**, we instruct the factory to create a **Ginger Tea** object whenever someone requests a `tea` object.

---

# Example 1 : Without Factory Override

```systemverilog
`include "uvm_macros.svh"
import uvm_pkg::*;

//----------------------------------------------------
// Parent Class
//----------------------------------------------------
class tea extends uvm_object;

   `uvm_object_utils(tea)

   function new(string name="tea");
      super.new(name);
   endfunction

   virtual function void prepare();
      $display("Preparing Basic Tea");
   endfunction

endclass

//----------------------------------------------------
// Child Class
//----------------------------------------------------
class ginger_tea extends tea;

   `uvm_object_utils(ginger_tea)

   function new(string name="ginger_tea");
      super.new(name);
   endfunction

   function void prepare();
      $display("Preparing Ginger Tea");
   endfunction

endclass

//----------------------------------------------------
// Testbench
//----------------------------------------------------
module tb;

   tea t;

   initial begin

      $display("---------------------------");
      $display("WITHOUT FACTORY OVERRIDE");
      $display("---------------------------");

      t = tea::type_id::create("t");

      t.prepare();

   end

endmodule
```

## Output

```
---------------------------
WITHOUT FACTORY OVERRIDE
---------------------------
Preparing Basic Tea
```

The factory creates a **tea** object because no override is applied.

---

# Example 2 : With Factory Override

```systemverilog
`include "uvm_macros.svh"
import uvm_pkg::*;

//----------------------------------------------------
// Parent Class
//----------------------------------------------------
class tea extends uvm_object;

   `uvm_object_utils(tea)

   function new(string name="tea");
      super.new(name);
   endfunction

   virtual function void prepare();
      $display("Preparing Basic Tea");
   endfunction

endclass

//----------------------------------------------------
// Child Class
//----------------------------------------------------
class ginger_tea extends tea;

   `uvm_object_utils(ginger_tea)

   function new(string name="ginger_tea");
      super.new(name);
   endfunction

   function void prepare();
      $display("Preparing Ginger Tea");
   endfunction

endclass

//----------------------------------------------------
// Testbench
//----------------------------------------------------
module tb;

   tea t;

   initial begin

      $display("---------------------------");
      $display("WITH FACTORY OVERRIDE");
      $display("---------------------------");

      // Factory Override
      tea::type_id::set_type_override(
         ginger_tea::get_type()
      );

      t = tea::type_id::create("t");

      t.prepare();

   end

endmodule
```

## Output

```
---------------------------
WITH FACTORY OVERRIDE
---------------------------
Preparing Ginger Tea
```

Notice that the code still says:

```systemverilog
t = tea::type_id::create("t");
```

But because of the factory override,

```systemverilog
tea::type_id::set_type_override(
    ginger_tea::get_type()
);
```

the factory actually creates a **ginger_tea** object.

---

# Factory Operation

## Without Override

```
Request

Create Tea
     |
     V
 UVM Factory
     |
     V
 Basic Tea
```

---

## With Override

```
Request

Create Tea
     |
     V
 UVM Factory
     |
 Factory Override
     |
     V
 Ginger Tea
```

---

# Key Observation

The request never changes.

```systemverilog
tea::type_id::create("t");
```

Only the **Factory** changes **what object is created**.

---

# One-Line Definition

**Factory Override** means:

> Whenever someone asks the UVM Factory to create an object of class **A**, the factory silently creates an object of class **B** instead, without modifying the existing code.
