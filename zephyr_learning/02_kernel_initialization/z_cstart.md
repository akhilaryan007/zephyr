# z_cstart()

## Overview

The function `z_cstart()` is the main entry point for the Zephyr kernel.

It is responsible for initializing the kernel and preparing the system for multitasking.

File location:

```
kernel/init.c
```

---

## Responsibilities

The main responsibilities of `z_cstart()` include:

1. Initializing kernel data structures
2. Creating static threads
3. Initializing system objects
4. Running initialization levels
5. Starting the scheduler

---

## Important Operations

Some critical functions called during initialization:

```
z_sys_init_run_level()
z_init_static_threads()
z_thread_system_init()
```

---

## Thread Creation

During initialization, the kernel creates important system threads:

* **Idle thread**
* **Main thread**
* **Static system threads**

---

## Execution Flow

```
z_cstart()
     ↓
Kernel initialization
     ↓
SYS_INIT execution
     ↓
Thread creation
     ↓
Scheduler start
```

---

## Key Insight

This function marks the transition from **system startup** to a **fully operational RTOS kernel**.
