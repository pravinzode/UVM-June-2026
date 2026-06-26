# UVM Object Field Automation Assignments (Digital Design Applications)

## Exercise 1: ALU Operation Packet
Design a UVM object for an ALU.

**Hint**
- Create an enum for operations: `ADD`, `SUB`, `AND`, `OR`, `XOR`.
- Randomize the operation.
- Store the ALU version as a string.
- Print the object using the table printer.

---

## Exercise 2: Traffic Light Controller
Create a configuration object for a traffic light controller.

**Hint**
- Create an enum for the current state.
- Store the junction name.
- Store the green-light duration.
- Display the object.

---

## Exercise 3: D Flip-Flop Configuration
Create a UVM object for a D Flip-Flop.

**Hint**
- Store the flip-flop name.
- Store setup time and hold time as real variables.
- Register all fields and print the object.

---

## Exercise 4: Multiplexer Family
Design a configuration object for multiplexers.

**Hint**
- Create an enum representing `2:1`, `4:1`, `8:1`, and `16:1`.
- Store the propagation delay.
- Display the selected multiplexer configuration.

---

## Exercise 5: UART Configuration
Create a UART configuration object.

**Hint**
- Create an enum for parity (`NONE`, `EVEN`, `ODD`).
- Store the baud rate as a real variable.
- Store the UART instance name.

---

## Exercise 6: Sequence Detector
Create an object representing a sequence detector.

**Hint**
- Create an enum for the detected sequence (`1010`, `1101`, `1110`).
- Store the detector name.
- Store the detection latency.

---

## Exercise 7: FSM Controller
Create a UVM object representing an FSM.

**Hint**
- Create an enum for FSM states (`IDLE`, `FETCH`, `DECODE`, `EXECUTE`).
- Randomize the current state.
- Print the object using the tree printer.

---

## Exercise 8: Clock Divider
Create a clock divider configuration.

**Hint**
- Create an enum for divide ratios (`÷2`, `÷4`, `÷8`, `÷16`).
- Store the input clock frequency.
- Print the configuration.

---

## Exercise 9: ADC Configuration
Design a UVM object for an ADC.

**Hint**
- Create an enum for resolution (`8-bit`, `10-bit`, `12-bit`, `16-bit`).
- Store the reference voltage.
- Store the ADC model number.

---

## Exercise 10: FIFO Status Monitor
Create a FIFO status object.

**Hint**
- Create an enum representing FIFO status (`EMPTY`, `PARTIAL`, `FULL`, `OVERFLOW`).
- Store the FIFO name.
- Print the object.

---

## Exercise 11: Printer Comparison
Using any one of the previous objects,

**Hint**
- Print the object using:
  - Table Printer
  - Tree Printer
  - Line Printer
- Compare the outputs.

---

## Exercise 12: Hide Sensitive Information
Modify any previous object.

**Hint**
- Hide one field (for example, version number or delay) using `UVM_NOPRINT`.
- Verify that the field is not displayed.

---

## Exercise 13: Binary Representation
Modify an object containing integer fields.

**Hint**
- Display one field in binary.
- Display another field in hexadecimal.
- Compare the printed formats.

---

## Exercise 14: Multiple DUT Configurations
Create three objects representing three different DUT configurations.

**Hint**
- Randomize all objects independently.
- Print all three objects.
- Compare their outputs.

---

## Exercise 15: Register New Fields
Extend an existing object.

**Hint**
- Add:
  - Design Version (String)
  - Operating Temperature (Real)
  - Design Revision (Integer)
- Register the new fields using the appropriate UVM field macros.

---

## Exercise 16: Constraint-Based Configuration
Modify an FSM or Counter configuration.

**Hint**
- Apply a constraint so that only specific enum values are generated.
- Verify the printed output.

---

## Exercise 17: Compare Manual Printing and Automatic Printing
Create an object containing multiple fields.

**Hint**
- Display the object once using `uvm_info()`.
- Display the same object using `print()`.
- Compare the effort required in both methods.

---

## Exercise 18: Design Your Own Peripheral
Create a configuration object for any digital peripheral of your choice.

**Hint**
Possible choices:
- Timer
- Watchdog Timer
- PWM Generator
- Cache Controller
- Interrupt Controller

Include at least:
- One enum
- One string
- One real variable

Register all fields and print the object.

---

## Exercise 19: Create a Nested Configuration
Create two UVM objects:

- `clock_cfg`
- `uart_cfg`

**Hint**
- Register `clock_cfg` inside `uart_cfg` using the appropriate UVM object field macro.
- Print the parent object and observe the hierarchical output.

---

## Exercise 20: Design a Complete DUT Configuration
Create a configuration object for any combinational or sequential circuit studied in Digital Electronics.

**Hint**
Possible DUTs:
- Carry Lookahead Adder
- Kogge-Stone Adder
- Barrel Shifter
- Booth Multiplier
- Johnson Counter
- Ring Counter
- Sequence Detector
- Traffic Light Controller
- Vending Machine FSM

Include suitable enum, string, real, and integer fields. Register all fields using UVM field automation macros and display the complete configuration using the UVM table printer.
