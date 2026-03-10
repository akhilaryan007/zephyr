# SYS_INIT Mechanism

## Overview

`SYS_INIT` is a macro used in Zephyr to register initialization functions that run during system startup.

It allows drivers and subsystems to automatically initialize without being manually called.

---

## Syntax

Example:

```
SYS_INIT(uart_init, POST_KERNEL, 50);
```

Parameters:

1. Initialization function
2. Initialization level
3. Priority

---

## How It Works

During compilation:

* The macro places the function into a **special linker section**.
* These sections are grouped by initialization level.

At runtime:

```
z_sys_init_run_level()
```

iterates through these sections and executes each function.

---

## Execution Order

Execution order depends on:

1. Initialization level
2. Priority number

Lower priority values run earlier.

Example:

```
Priority 10 → runs before Priority 50
```

---

## Why This Mechanism is Useful

Benefits:

* Modular driver initialization
* Automatic subsystem startup
* Structured boot process
* Flexible dependency management
