# Reset Handler

## Overview

The Reset Handler is the first piece of code executed after a microcontroller reset.
It performs minimal system setup and transfers execution to the C runtime initialization.

In Zephyr, the Reset Handler is implemented in assembly language.

---

## Why Assembly is Used

Assembly is required because:

* The C runtime environment is not initialized yet
* Stack pointer must be configured manually
* Memory sections must be prepared before C code runs

---

## Reset Handler Responsibilities

The Reset Handler performs the following steps:

1. Load the initial stack pointer
2. Set up minimal CPU state
3. Disable interrupts
4. Branch to `z_prep_c()`

---

## Code Location

The Reset Handler for ARM Cortex-M systems is located in:

```
arch/arm/core/cortex_m/reset.S
```

---

## Execution Flow

```
Reset Occurs
      ↓
CPU Reads Vector Table
      ↓
Jump to Reset_Handler
      ↓
Assembly Initialization
      ↓
Call z_prep_c()
```

---

## Important Observation

At this stage:

* No scheduler exists
* No threads exist
* No drivers are initialized

The CPU is still running in a **bare-metal state**.
