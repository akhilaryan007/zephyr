# Memory Sections in Embedded Systems

## Overview

Embedded systems divide program memory into multiple sections to organize code and variables.

Important sections include:

* `.text`
* `.data`
* `.bss`
* `.rodata`

---

## .text Section

The `.text` section contains:

* executable instructions
* program code

Location:

```
Stored in Flash memory
```

---

## .data Section

The `.data` section contains:

* global variables
* static variables
* variables with initial values

Example:

```
int counter = 5;
```

These values are stored in Flash and copied to RAM during system startup.

---

## .bss Section

The `.bss` section stores:

* uninitialized global variables
* static variables without initial values

Example:

```
int buffer[100];
```

---

## Why .bss is Cleared

Instead of storing zeros in Flash (which wastes memory), the system simply:

1. Allocates RAM space
2. Clears the memory to zero during startup

This operation occurs inside:

```
z_prep_c()
```

---

## Embedded Memory Layout

Typical memory structure:

```
Flash Memory
------------
.text
.rodata
.data (initial values)

RAM
------------
.data (runtime copy)
.bss
.heap
.stack
```

---

## Key Insight

Clearing the `.bss` section ensures that all global variables start with a **known value (zero)** when the system boots.
