# RTOS Patterns

Load this reference when the project uses FreeRTOS or a similar task scheduler.

## Covered Areas

- Task creation and priority assignment
- Queue-based producer/consumer patterns
- Mutexes for shared peripheral access
- ISR-to-task signaling with semaphores
- Software timers and event groups

## Design Rules

- Use `vTaskDelayUntil()` for periodic tasks that require stable cadence
- Use queues for ownership transfer and decoupling
- Use mutexes for shared buses such as I2C or UART
- Use `...FromISR()` APIs in interrupts
- Yield from ISR only when a higher-priority task was woken
- Keep critical sections short

## Failure Modes To Watch

- Priority inversion
- Queue overflow under burst traffic
- Stack under-sizing
- Doing too much work in callbacks or timer contexts
