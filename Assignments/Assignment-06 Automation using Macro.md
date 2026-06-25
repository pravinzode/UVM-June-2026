# UVM Field Automation and Printer Policy Assignments

## Objective

The purpose of these assignments is to understand:

- UVM Field Automation Macros
- UVM Printer Policies
- Field Registration
- Printing Formats
- UVM_NOPRINT
- UVM_BIN, UVM_DEC, UVM_HEX
- Object Introspection

---

## Base Code

```systemverilog
`include "uvm_macros.svh"
import uvm_pkg::*;

class obj extends uvm_object;

  function new(string path = "obj");
    super.new(path);
  endfunction

  rand bit [3:0] a;
  rand bit [7:0] b;

  `uvm_object_utils_begin(obj)
    `uvm_field_int(a, UVM_NOPRINT | UVM_BIN)
    `uvm_field_int(b, UVM_DEFAULT | UVM_DEC)
  `uvm_object_utils_end

endclass

module tb;

  obj o;

  initial begin
    o = new("obj");
    o.randomize();
    o.print(uvm_default_table_printer);
  end

endmodule
```

---

# Exercise 1: Observe the Printed Output

## Problem Statement

Compile and execute the given code.

### Tasks

1. Observe the generated output.
2. Identify which fields are printed.
3. Explain why field `a` is not displayed.

### Learning Outcome

Understanding the effect of:

```systemverilog
UVM_NOPRINT
```

---

# Exercise 2: Enable Printing of Field a

## Problem Statement

Modify the code so that field `a` is also printed.

### Tasks

1. Remove the `UVM_NOPRINT` option.
2. Execute the simulation.
3. Compare the output before and after modification.

### Learning Outcome

Understanding field visibility control.

---

# Exercise 3: Binary Printing

## Problem Statement

Print both fields in binary format.

### Tasks

Modify field registration as follows:

```systemverilog
`uvm_field_int(a, UVM_BIN)
`uvm_field_int(b, UVM_BIN)
```

### Questions

1. How many bits are displayed for each field?
2. Why are leading zeros shown?

### Learning Outcome

Understanding binary printer formatting.

---

# Exercise 4: Decimal Printing

## Problem Statement

Print both fields in decimal format.

### Tasks

Use:

```systemverilog
`uvm_field_int(a, UVM_DEC)
`uvm_field_int(b, UVM_DEC)
```

### Learning Outcome

Understanding decimal representation.

---

# Exercise 5: Hexadecimal Printing

## Problem Statement

Display both fields in hexadecimal format.

### Tasks

Use:

```systemverilog
`uvm_field_int(a, UVM_HEX)
`uvm_field_int(b, UVM_HEX)
```

### Questions

1. Compare hexadecimal output with binary output.
2. Which format is more compact?

### Learning Outcome

Understanding hexadecimal formatting.

---

# Exercise 6: Mixed Printing Formats

## Problem Statement

Display different fields using different formats.

### Requirements

- Print `a` in binary.
- Print `b` in hexadecimal.

### Expected Registration

```systemverilog
`uvm_field_int(a, UVM_BIN)
`uvm_field_int(b, UVM_HEX)
```

### Learning Outcome

Understanding field-specific formatting.

---

# Exercise 7: Add a New Field

## Problem Statement

Add another random field.

### Declaration

```systemverilog
rand bit [15:0] data;
```

### Tasks

1. Register the field using field macros.
2. Print it using hexadecimal format.
3. Randomize and observe the output.

### Learning Outcome

Registering additional fields.

---

# Exercise 8: Compare Different Printer Policies

## Problem Statement

Print the same object using different printer policies.

### Tasks

Print using:

```systemverilog
o.print(uvm_default_table_printer);
```

```systemverilog
o.print(uvm_default_tree_printer);
```

```systemverilog
o.print(uvm_default_line_printer);
```

### Questions

1. Which output is easiest to read?
2. Which output occupies the least space?

### Learning Outcome

Understanding UVM printer policies.

---

# Exercise 9: Print Multiple Objects

## Problem Statement

Create multiple object instances.

### Tasks

Create:

```systemverilog
obj o1;
obj o2;
obj o3;
```

Randomize all objects and print them using:

```systemverilog
uvm_default_table_printer
```

### Learning Outcome

Observing different randomized values.

---

# Exercise 10: Selective Field Printing

## Problem Statement

Hide one field and print the remaining fields.

### Tasks

1. Hide field `b` using:

```systemverilog
UVM_NOPRINT
```

2. Print the object.
3. Verify that only field `a` appears.

### Learning Outcome

Selective visibility control.

---

# Exercise 11: Packet Class

## Problem Statement

Create a packet class containing:

```systemverilog
rand bit [7:0] addr;
rand bit [7:0] data;
rand bit write;
```

### Tasks

1. Register all fields.
2. Print:

- addr in HEX
- data in DEC
- write in BIN

### Learning Outcome

Using different print formats within the same object.

---

# Exercise 12: Analyze UVM Field Automation

## Problem Statement

Comment out all field macros.

### Tasks

Remove:

```systemverilog
`uvm_field_int(...)
```

and run:

```systemverilog
o.print(uvm_default_table_printer);
```

### Questions

1. What happens to the output?
2. Why does UVM fail to print the fields automatically?

### Learning Outcome

Understanding the role of field automation macros.

---

# Challenge Exercise

## Custom Printer Configuration

Modify:

```systemverilog
uvm_default_table_printer.knobs.show_radix = 1;
uvm_default_table_printer.knobs.show_root = 1;
```

### Tasks

1. Print the object.
2. Observe the effect of printer knobs.
3. Document the changes in output.

### Learning Outcome

Understanding printer customization.
