# Power Optimization

Load this reference when the device is battery-powered or must meet a sleep-current budget.

## Main Areas

- Sleep, stop, and standby mode selection
- Dynamic clock scaling
- Peripheral clock gating
- GPIO leakage reduction
- Wakeup source planning

## Design Rules

- Pick the lowest power mode that still meets wakeup latency requirements
- Reconfigure clocks correctly after stop-mode wakeup
- Disable unused peripherals and GPIO banks
- Put unused pins into analog mode or another leakage-safe state
- Base power choices on measured activity windows, not assumptions

## Common Tradeoffs

- Lower clock speed reduces power but increases execution time
- Deeper sleep saves more current but increases wake latency and restore complexity
- Aggressive peripheral gating saves power but can add reinit overhead and protocol latency
