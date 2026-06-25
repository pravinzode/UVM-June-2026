# #  UVM Reporting Macro Timing Example
## — Day-01 Advanced Exercises

## Exercise-01 — Write UVM code to:   
-- Throw a warning at 50 ns  
-- Throw an error at 100 ns  
-- Forcefully stop simulation at 200 ns  
  
---
## Solution  
  
```systemverilog  
module test;  
  
import uvm_pkg::*;  
`include "uvm_macros.svh"  
  
initial begin  
  
// Warning at 50 ns  
#50;  
`uvm_warning("WARN",  
"Warning generated at 50 ns")  
  
// Error at 100 ns  
#50;  
`uvm_error("ERROR",  
"Error generated at 100 ns")  
  
// Fatal at 200 ns  
#100;  
`uvm_fatal("FATAL",  
"Simulation stopped at 200 ns")  
  
end  
  
endmodule  
```  
  
---  
## Expected Behavior  
  
| Time | Macro | Action |  
|---|---|---|  
| 50 ns | `uvm_warning` | Warning message displayed |  
| 100 ns | `uvm_error` | Error message displayed |  
| 200 ns | `uvm_fatal` | Simulation terminates

---
## Timing Exercises 
# UVM Reporting Macro Timing Exercises

---

# Exercise 1
## Task
- Print info message at 20 ns
- Print warning at 40 ns
- Stop simulation at 80 ns

---

# Exercise 2
## Task
- Print warning at 25 ns
- Print error at 75 ns
- Print fatal at 150 ns

---

# Exercise 3
## Task
- Print info messages at:
  - 10 ns
  - 20 ns
  - 30 ns

---

# Exercise 4
## Task
- Print warning every 20 ns for 5 times

---

# Exercise 5
## Task
- Print error message after:
```systemverilog
#100;
```

---

# Exercise 6
## Task
- Print:
  - info at 50 ns
  - warning at 100 ns
  - error at 150 ns
  - fatal at 200 ns

---

# Exercise 7
## Task
- Print counter value every 10 ns from 1 to 5 using:
```systemverilog
`uvm_info
```

---

# Exercise 8
## Task
- Generate warning at 30 ns if temperature > 50
- Generate error at 60 ns if temperature > 80

---

# Exercise 9
## Task
- Print simulation time at:
  - 25 ns
  - 50 ns
  - 75 ns
  - 100 ns

---

# Exercise 10
## Task
- Print:
  - startup message at 0 ns
  - processing message at 50 ns
  - completion message at 100 ns
  - fatal stop at 150 ns
  
