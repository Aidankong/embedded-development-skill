---
name: embedded-development
description: Use when working on embedded firmware or MCU projects, including STM32CubeMX .ioc editing, headless code generation, bare-metal microcontroller programming, RTOS task design, DMA/interrupt-driven peripherals, communication protocols, memory optimization, and low-power design. Suitable for STM32, ESP32, Cortex-M, FreeRTOS, and similar embedded systems work.
---

# Embedded Development

Use this skill for general embedded firmware work, especially when the task spans MCU configuration, driver code, timing constraints, RTOS behavior, communication buses, or resource optimization.

## What This Skill Covers

- STM32CubeMX `.ioc` editing and headless project generation
- Bare-metal firmware and register-level MCU programming
- FreeRTOS task, queue, semaphore, and timer patterns
- Peripheral bring-up for GPIO, timers, ADC, UART, I2C, SPI, and CAN
- DMA and interrupt-driven designs
- RAM, flash, stack, and code-size optimization
- Low-power modes and power-aware peripheral control

## Core Workflow

1. Identify the actual platform and constraints
2. Inspect the project structure, build system, and generated-code boundaries
3. Choose the right implementation mode
4. Implement or modify configuration and code
5. Verify buildability and call out runtime risks

## Step 1: Identify Constraints

Determine:

- MCU family and exact part
- Clock tree and memory limits
- Whether the project uses CubeMX, HAL, LL, ESP-IDF, Arduino, or bare-metal code
- Whether RTOS is present
- Timing, interrupt latency, throughput, and power requirements

## Step 2: Respect Existing Architecture

- Prefer the repo's existing HAL, LL, or register-level style
- Do not overwrite user code inside generated regions unless the project already treats generated code as disposable
- For CubeMX projects, treat the `.ioc` file as the source of truth for peripheral topology
- Keep ISR work short and defer processing to tasks, queues, flags, or ring buffers

## Step 3: Choose The Right Path

### For STM32CubeMX-based projects

Load:

- [references/IOC_CubeMX.md](references/IOC_CubeMX.md)
- [references/USART_DMA.md](references/USART_DMA.md) when UART + DMA is involved

Use this path when the task requires pin, peripheral, DMA, NVIC, or generated-init changes.

### For bare-metal or low-level MCU code

Load:

- [references/microcontroller-programming.md](references/microcontroller-programming.md)

Use this path when working directly with registers, clocks, GPIO, timers, ADC, UART, or low-power entry code.

### For RTOS-based firmware

Load:

- [references/rtos-patterns.md](references/rtos-patterns.md)

Use this path when the task involves FreeRTOS tasks, queues, mutexes, ISR-to-task signaling, or timers.

### For communication stacks or bus drivers

Load:

- [references/communication-protocols.md](references/communication-protocols.md)

Use this path for I2C, SPI, UART, CAN, buffering, and DMA/interrupt transfer patterns.

### For optimization work

Load:

- [references/memory-optimization.md](references/memory-optimization.md)
- [references/power-optimization.md](references/power-optimization.md)

Use these when the task is constrained by RAM, flash, stack, battery life, or sleep behavior.

## High-Value Rules

- Always account for flash, RAM, stack, timing, and power constraints
- Use `volatile` for hardware-visible state and register access patterns that require it
- Keep ISRs short; do not block in interrupt context
- Prefer timeouts for polling loops and bus operations
- Protect shared state with suitable synchronization
- Use DMA when throughput or CPU overhead justifies it
- Avoid unbounded dynamic allocation in long-running firmware unless the project already has a safe allocator strategy
- Add or preserve watchdog handling where reliability matters

## CubeMX-Specific Rules

- Keep `Mcu.IPx` and `Mcu.IPNb` synchronized
- Keep `Mcu.Pinx` and `Mcu.PinsNb` synchronized
- Ensure pin signal mappings exist for generated peripherals
- Keep `ProjectManager.functionlistsort` aligned with generated init functions
- Use absolute paths with STM32CubeMX CLI
- Preserve IOC escaping such as `\:` and `\#`

## Output Expectations

When making embedded changes, provide:

- The configuration or code change itself
- Any assumptions about MCU family, clocking, or middleware
- A brief note on interrupt/timing/power tradeoffs when relevant
- Build or validation status if it was possible to run checks

## References

- [references/IOC_CubeMX.md](references/IOC_CubeMX.md)
- [references/USART_DMA.md](references/USART_DMA.md)
- [references/microcontroller-programming.md](references/microcontroller-programming.md)
- [references/communication-protocols.md](references/communication-protocols.md)
- [references/rtos-patterns.md](references/rtos-patterns.md)
- [references/memory-optimization.md](references/memory-optimization.md)
- [references/power-optimization.md](references/power-optimization.md)
