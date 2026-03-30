# embedded-development-skill

Codex skill for embedded firmware work.

## Included Scope

- STM32CubeMX `.ioc` editing and headless code generation
- Bare-metal microcontroller programming
- FreeRTOS and RTOS task patterns
- DMA and interrupt-driven peripheral design
- I2C, SPI, UART, and CAN communication patterns
- Memory and power optimization guidance

## Structure Decision

This repository keeps a single primary skill: `embedded-development`.

The older `stm32-cubemx` material is folded into this repository as STM32CubeMX-specific references instead of a second top-level skill. That keeps discovery cleaner and avoids splitting one embedded workflow into two competing entry points.

## Repository Layout

- `embedded-development/SKILL.md`
- `embedded-development/agents/openai.yaml`
- `embedded-development/references/`
- `embedded-development/legacy/`
