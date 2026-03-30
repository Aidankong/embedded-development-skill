# Legacy Skill Mapping: stm32-cubemx

This file preserves the intent of the older `stm32-cubemx` skill and maps it into the consolidated `embedded-development` skill.

## Why It Is Not A Separate Top-Level Skill

- `stm32-cubemx` is a specialized subset of embedded firmware work
- its workflow is already covered by the main `embedded-development` skill
- keeping a single entry skill reduces ambiguity during trigger selection
- CubeMX-specific details fit naturally as references instead of a parallel skill

## Equivalent Coverage In This Repository

Use these files instead of a separate `stm32-cubemx` skill:

- `embedded-development/SKILL.md`
- `embedded-development/references/IOC_CubeMX.md`
- `embedded-development/references/USART_DMA.md`

## Legacy Scope

The original `stm32-cubemx` content focused on:

- editing `.ioc` files directly
- configuring pins, peripherals, DMA, and NVIC
- generating code with STM32CubeMX CLI
- validating generated projects with CMake

That scope is intentionally preserved inside the consolidated skill.
