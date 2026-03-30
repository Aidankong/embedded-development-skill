# Microcontroller Programming

Load this reference for bare-metal, register-level, and peripheral bring-up work.

## Typical Scope

- GPIO configuration and atomic writes
- Timer interrupts and PWM
- EXTI setup and ISR structure
- ADC single-shot and DMA modes
- UART register-level setup
- System clock initialization
- Watchdog integration
- Sleep, stop, and standby entry

## Core Practices

- Enable the clock tree before touching a peripheral
- Use `volatile` where hardware-visible state requires it
- Clear interrupt flags inside ISRs
- Keep handlers short and deterministic
- Use `BSRR` or equivalent atomic GPIO registers when available
- Add timeout guards around polling loops

## Patterns To Prefer

- GPIO writes through atomic set/reset registers
- Timer-generated periodic work instead of busy loops
- DMA for sustained ADC/UART/SPI transfers
- Wakeup-driven low-power entry rather than polling

## When Editing Existing Projects

- Match the repo's chosen abstraction level
- Do not mix raw-register code into a HAL-heavy module unless the project already does so
- Keep startup, linker, and clock assumptions explicit
