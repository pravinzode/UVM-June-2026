# UVM Config DB Exercises


---

## 📘 What is uvm_config_db?

`uvm_config_db` is used in UVM to pass configuration data between components without direct connections.

It provides:
- Loose coupling
- Reusable components
- Centralized configuration

---

## 🟢 Simple Exercises (Beginner Level)

### Exercise 1: Change Value
Store `20` instead of `12` and print it in env.

Expected Output:
Value of data : 20

---

### Exercise 2: Store Another Integer
Store:
data = 10
Retrieve and print in env.

---

### Exercise 3: Two Values
Store:
data = 5  
addr = 15  
Retrieve both and print.

---

### Exercise 4: String Value
Store:
name = "UVM"  
Retrieve and print.

---

### Exercise 5: Bit Variable
Store:
enable = 1  
Retrieve and print.

---

### Exercise 6: Wrong Key Test
Store:
data = 100  
Try retrieving:
value  

Expected Output:
UVM_ERROR Unable to access the Value

---

## 🟡 Moderate Exercise

### Exercise 11: Test → Env → Driver Configuration

Hierarchy:
test
 └── env
      └── driver

Step 1 (Test):
uvm_config_db#(int)::set(this, "e.driver", "packet_size", 64);

Step 2 (Driver):
int packet_size;

if(uvm_config_db#(int)::get(this, "", "packet_size", packet_size))
  `uvm_info("DRV", $sformatf("Packet Size = %0d", packet_size), UVM_LOW)
else
  `uvm_error("DRV", "Packet size not found");

Expected Output:
DRIVER Packet Size = 64

---

## ⭐ Tips

- Always call set() before get()
- Key names must match exactly
- Prefer hierarchical paths over hardcoded names
