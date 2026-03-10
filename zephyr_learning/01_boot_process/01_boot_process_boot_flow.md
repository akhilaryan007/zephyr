# Zephyr Boot Flow

## Overview

The boot process of Zephyr RTOS begins immediately after the microcontroller reset.
The CPU loads the initial stack pointer and program counter from the **vector table** and starts execution from the Reset Handler.

Understanding the boot flow is important because it shows how the system transitions from **bare hardware** to a **fully running RTOS kernel**.

---

## Boot Sequence

The execution flow during system startup:

```
Hardware Reset
      ↓
Vector Table Loaded
      ↓
Reset_Handler (Assembly)
      ↓
z_prep_c()
      ↓
z_cstart()
      ↓
Kernel Initialization
      ↓
Scheduler Start
      ↓
Main Thread Execution
```

---

## Step 1: Hardware Reset

When the MCU resets:

* The CPU reads the **initial stack pointer** from the vector table.
* The CPU reads the **Reset Handler address**.
* Execution jumps to the Reset Handler.

---

## Step 2: Reset Handler

The Reset Handler is written in **assembly language**.

Responsibilities:

* Set up minimal CPU environment
* Prepare stack pointer
* Jump into the C runtime preparation

File location in Zephyr source:

```
arch/arm/core/cortex_m/reset.S
```

---

## Step 3: C Runtime Preparation

The function `z_prep_c()` prepares the system before the kernel starts.

Main tasks:

* Initialize memory sections
* Clear `.bss`
* Copy `.data` from flash to RAM
* Initialize interrupts
* Configure hardware state

---

## Step 4: Kernel Start

After the system preparation is completed:

```
z_prep_c() → z_cstart()
```

The function `z_cstart()` begins the **Zephyr kernel initialization process**.

---

## Key Observation

After reset, the CPU is essentially **in a raw state** with no operating system running.

The boot process gradually transforms this raw CPU state into a **fully functional RTOS environment**.
