# SystemVerilog_Data_Types
---

This repository introduces the fundamental **SystemVerilog data types and array constructs** covered in **Day 1** of the SystemVerilog 12-Week Roadmap.

## Topics Covered

* `logic`
* `bit`
* `int`
* `integer`
* ` Packed Arrays `
* ` Unpacked Arrays `
* `typedef`
* `enum`

---

## 1. `logic`

### Description

`logic` is a **4-state variable data type** in SystemVerilog. It can represent:

| Value | Meaning        |
| ----- | -------------- |
| `0`   | Logic Low      |
| `1`   | Logic High     |
| `X`   | Unknown        |
| `Z`   | High Impedance |

It is commonly used for signals and variables in RTL design.

### Syntax

```systemverilog
logic signal;
logic [7:0] data;
```

### Example

```systemverilog
logic enable;
logic [3:0] data;
```

---

## 2. `bit`

### Description

`bit` is a **2-state data type**. It can represent only `0` and `1`.

Unlike `logic`, it does not represent `X` or `Z`.

### Syntax

```systemverilog
bit signal;
bit [7:0] data;
```

### Example

```systemverilog
bit enable;
bit [3:0] count;
```

---

## 3. `int`

### Description

`int` is a **32-bit, 4-state, signed integral data type**.

It is commonly used for calculations, counters, loop variables, and testbench variables.

### Syntax

```systemverilog
int variable;
```

### Example

```systemverilog
int count;

initial begin
    count = 100;
end
```

---

## 4. `integer`

### Description

`integer` is a **32-bit, 4-state, signed integer type** inherited from Verilog.

It is commonly encountered in older Verilog code and testbenches.

### Syntax

```systemverilog
integer variable;
```

### Example

```systemverilog
integer i;

initial begin
    for (i = 0; i < 10; i = i + 1)
        $display("i = %0d", i);
end
```

---

## 5. Packed Arrays

### Description

A **packed array** stores multiple bits together as one contiguous vector.

The packed dimension is written **before the variable name**.

### Syntax

```systemverilog
logic [7:0] data;
```

This creates an **8-bit packed array**.

### Example

```systemverilog
logic [3:0] A;
logic [7:0] data;
```

Individual bits can be accessed using an index:

```systemverilog
A[0]
A[3]
```

### Visualization

```text
logic [3:0] A;

     3   2   1   0
   +---+---+---+---+
A  | 1 | 0 | 1 | 1 |
   +---+---+---+---+
```

---

## 6. Unpacked Arrays

### Description

An **unpacked array** contains multiple separate elements of a particular data type.

The unpacked dimension is written **after the variable name**.

### Syntax

```systemverilog
logic data [7:0];
```

This creates an array containing **8 separate `logic` elements**.

### Example

```systemverilog
int numbers [0:4];

initial begin
    numbers[0] = 10;
    numbers[1] = 20;
    numbers[2] = 30;
end
```

### Packed vs Unpacked

```systemverilog
logic [7:0] data;
```

* `[7:0]` is a **packed array**
* `data` represents one 8-bit vector

```systemverilog
logic data [7:0];
```

* `[7:0]` is an **unpacked array**
* `data` contains 8 separate `logic` elements

---

## 7. `typedef`

### Description

`typedef` creates an **alternative name (alias)** for an existing data type.

It improves code readability, reusability, and maintainability.

### Syntax

```systemverilog
typedef <data_type> <new_type_name>;
```

### Example

```systemverilog
typedef logic [7:0] byte_t;

byte_t data;
```

Here:

```text
byte_t
  ↓
logic [7:0]
```

So `data` is effectively an 8-bit `logic` variable.

### Another Example

```systemverilog
typedef int unsigned uint_t;

uint_t count;
```

---

## 8. `enum`

### Description

`enum` defines a variable that can take one value from a predefined set of **named values**.

Enumerations are particularly useful for representing **FSM states**.

### Syntax

```systemverilog
typedef enum {
    STATE1,
    STATE2,
    STATE3
} state_t;
```

### Example

```systemverilog
typedef enum {
    IDLE,
    START,
    STOP
} state_t;

state_t state;
```

The variable `state` can contain:

```text
IDLE
START
STOP
```

### FSM Example

```systemverilog
typedef enum {
    IDLE,
    LOAD,
    PROCESS,
    DONE
} state_t;

state_t state;
```

This is much more readable than manually defining binary state values such as:

```systemverilog
localparam IDLE    = 2'b00;
localparam LOAD    = 2'b01;
localparam PROCESS = 2'b10;
localparam DONE    = 2'b11;
```

---

# Quick Comparison

| Type / Construct | Description                          |
| ---------------- | ------------------------------------ |
| `logic`          | 4-state variable                     |
| `bit`            | 2-state variable                     |
| `int`            | 32-bit, 4-state, signed integer      |
| `integer`        | 32-bit, 4-state, signed integer      |
| Packed Array     | Groups bits into a contiguous vector |
| Unpacked Array   | Collection of separate elements      |
| `typedef`        | Creates an alias for a data type     |
| `enum`           | Defines named constant values        |

---

# `logic` vs `bit`

| Feature      | `logic`    | `bit`                        |
| ------------ | ---------- | ---------------------------- |
| States       | 4-state    | 2-state                      |
| `0`          | ✓          | ✓                            |
| `1`          | ✓          | ✓                            |
| `X`          | ✓          | ✗                            |
| `Z`          | ✓          | ✗                            |
| Common Usage | RTL design | Testbench / 2-state modeling |

---

# Packed vs Unpacked Arrays

| Feature      | Packed Array              | Unpacked Array         |
| ------------ | ------------------------- | ---------------------- |
| Declaration  | Before variable name      | After variable name    |
| Example      | `logic [7:0] data`        | `logic data [7:0]`     |
| Represents   | Contiguous bits           | Collection of elements |
| Common Usage | Registers, buses, vectors | Memories, arrays       |

---
