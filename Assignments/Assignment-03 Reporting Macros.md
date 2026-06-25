
# UVM Reporting Macros — Day-02 Lab Exercises

## Exercise 1 — Simple Info Message
- Print `"Hello UVM"` using:
```systemverilog
`uvm_info
```
---

## Exercise 2 — Simple Warning Message
- Print `"Temperature High"` using:
```systemverilog
`uvm_warning
```
---
## Exercise 3 — Simple Error Message
- Print `"Invalid Data"` using:
```systemverilog
`uvm_error
```
---
## Exercise 4 — Simple Fatal Message
- Print `"Simulation Stopped"` using:
```systemverilog
`uvm_fatal
```
---
## Exercise 5 — Message ID Usage
- Use message ID `"TEST1"` with:
```systemverilog
`uvm_info
```
---
## Exercise 6 — Multiple Info Messages
- Print three different info messages sequentially.
---
## Exercise 7 — Using Verbosity
- Print info message using:
```systemverilog
UVM_LOW
```
---
## Exercise 8 — Print Integer Value
- Declare integer variable and print its value using:
```systemverilog
$sformatf()
```
---
## Exercise 9 — Print Two Variables
- Declare two integer variables and print both values in one message.
---
## Exercise 10 — Loop Printing
- Use loop from 1 to 5 and print loop counter using:
```systemverilog
`uvm_info
```
---
## Exercise 11 — Simulation Time
- Print current simulation time using:
```systemverilog
$time
```
---
## Exercise 12 — Delay and Reporting
- Print message after:
```systemverilog
#10;
```
delay.

---

## Exercise 13 — Repeated Printing
- Print same message 5 times using loop.

---
## Exercise 14 — Even Number Detection
- Check whether number is even and print:
```text
Even Number
```
---
## Exercise 15 — Odd Number Warning
- Check whether number is odd and print warning message.
---
## Exercise 16 — Positive Number Check
- If number > 0, print:
```text
Positive Number
```
---
## Exercise 17 — Negative Number Error
- If number < 0, print error message.
---
## Exercise 18 — Print Student Information
- Print:
  - Name
  - Roll Number
  - Branch
using reporting macros.
---
## Exercise 19 — Counter Display
- Increment counter from 0 to 3 and print counter value.
---
## Exercise 20 — All Macros Together
- Demonstrate:
```systemverilog
`uvm_info
`uvm_warning
`uvm_error
`uvm_fatal
```
in a single simple program.

---
