# STM32CubeMX IOC And Headless Generation

Use this reference when the project is driven by STM32CubeMX and `.ioc` files.

## Core Workflow

1. Edit the `.ioc` file
2. Generate code with STM32CubeMX CLI
3. Build the generated project

## Core Rules

- When adding a peripheral, update both `Mcu.IPx` entries and `Mcu.IPNb`
- When adding pins, update both `Mcu.Pinx` entries and `Mcu.PinsNb`
- Ensure pin signal mappings such as `PA2.Signal=USART2_TX` exist
- Keep `ProjectManager.functionlistsort` aligned with generated init functions
- For DMA-backed peripherals, configure both peripheral DMA enable flags and `Dma.*` requests
- Use absolute paths with STM32CubeMX CLI

## Typical Headless Script

```text
config load /absolute/path/to/project.ioc
project generate
exit
```

## Typical Invocation

```bash
/absolute/path/to/STM32CubeMX -q /absolute/path/to/cube_headless.txt
```

## Typical Validation

```bash
cmake --preset Debug
cmake --build build/Debug
```

## Important IOC Areas

### Peripheral inventory

```ini
Mcu.IP0=ADC1
Mcu.IP1=DMA
Mcu.IP2=NVIC
Mcu.IP3=RCC
Mcu.IPNb=4
```

### Pin inventory

```ini
Mcu.Pin0=PA2
Mcu.Pin1=PA3
Mcu.PinsNb=2
PA2.Signal=USART2_TX
PA3.Signal=USART2_RX
```

### DMA and NVIC

```ini
Dma.Request0=USART2_RX
Dma.Request1=USART2_TX
Dma.RequestsNb=2
NVIC.USART2_IRQn=true\:0\:0\:false\:false\:true\:true\:true\:true
```

### Generated init ordering

```ini
ProjectManager.functionlistsort=1-SystemClock_Config-RCC-false-HAL-false,2-MX_GPIO_Init-GPIO-false-HAL-true,3-MX_DMA_Init-DMA-false-HAL-true,4-MX_USART2_UART_Init-USART2-false-HAL-true
```

## Escaping Rules

- `:` as `\:`
- `#` as `\#`
- `=` as `\=`
- space in property names as `\ `

Examples:

```ini
ADC1.Channel-1\#ChannelRegularConversion=ADC_CHANNEL_5
TIM3.Channel-PWM\ Generation1\ CH1=PWM_CHANNEL1
```
