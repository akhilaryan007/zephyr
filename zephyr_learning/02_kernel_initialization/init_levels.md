# Initialization Levels

## Overview

Zephyr uses multiple initialization levels to control the order in which subsystems are initialized.

This ensures dependencies between subsystems are respected.

---

## Initialization Levels

Zephyr defines the following levels:

```
EARLY
PRE_KERNEL_1
PRE_KERNEL_2
POST_KERNEL
APPLICATION
```

---

## Execution Mechanism

Initialization functions are executed using:

```
z_sys_init_run_level()
```

The function iterates through registered initialization entries.

Example code pattern:

```
for (entry = levels[level]; entry < levels[level+1]; entry++) {
    const struct device *dev = entry->dev;
    int result = 0;
}
```

---

## Purpose of Each Level

EARLY
Low level system setup.

PRE_KERNEL_1
Hardware initialization before kernel services are available.

PRE_KERNEL_2
Additional driver initialization.

POST_KERNEL
Drivers requiring kernel services.

APPLICATION
Application level initialization.

---

## Key Insight

Initialization levels ensure **correct driver startup order**.
