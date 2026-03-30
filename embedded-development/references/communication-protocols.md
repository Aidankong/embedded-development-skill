# Communication Protocols

Load this reference for bus and link-layer firmware work.

## Covered Areas

- I2C master transactions with timeout handling
- SPI master transfers and DMA-based streaming
- UART polling, IRQ, ring-buffer, and DMA patterns
- CAN initialization, filters, transmit, and receive paths

## Design Rules

- Always use timeouts for bus waits and state transitions
- Prefer interrupt or DMA-driven transfers over long polling loops
- Protect shared buffers accessed from ISR and task contexts
- Validate frame integrity where the protocol supports CRC or checksums
- Keep alternate-function pin mapping and clocking aligned with the target MCU

## Preferred Patterns

- Ring buffers for UART RX
- DMA for high-throughput SPI or UART traffic
- Register-read helper patterns for I2C devices
- Explicit error recovery for overrun, NACK, or bus-stuck conditions
