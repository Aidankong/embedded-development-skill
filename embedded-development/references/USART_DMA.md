# USART + DMA Reference

Use this reference when adding UART DMA support in a CubeMX `.ioc` file.

## Example: USART2 on STM32F103

```ini
Mcu.IP0=ADC1
Mcu.IP1=DMA
Mcu.IP2=NVIC
Mcu.IP3=RCC
Mcu.IP4=SYS
Mcu.IP5=USART2
Mcu.IPNb=6

Mcu.Pin0=PA2
Mcu.Pin1=PA3
Mcu.Pin2=VP_SYS_VS_Systick
Mcu.PinsNb=3

PA2.Locked=true
PA2.Mode=Asynchronous
PA2.Signal=USART2_TX

PA3.Locked=true
PA3.Mode=Asynchronous
PA3.Signal=USART2_RX

USART2.BaudRate=115200
USART2.Dmaenabledrx=1
USART2.Dmaenabledtx=1
USART2.IPParameters=BaudRate,Dmaenabledrx,Dmaenabledtx,Mode,VirtualMode
USART2.Mode=Asynchronous
USART2.VirtualMode=VM_ASYNC
USART2.WordLength=WORDLENGTH_8B
USART2.Parity=PARITY_NONE
USART2.StopBits=STOPBITS_1

Dma.Request0=USART2_RX
Dma.Request1=USART2_TX
Dma.RequestsNb=2

Dma.USART2_RX.0.Direction=DMA_PERIPH_TO_MEMORY
Dma.USART2_RX.0.Instance=DMA1_Channel6
Dma.USART2_RX.0.MemDataAlignment=DMA_MDATAALIGN_BYTE
Dma.USART2_RX.0.MemInc=DMA_MINC_ENABLE
Dma.USART2_RX.0.Mode=DMA_NORMAL
Dma.USART2_RX.0.PeriphDataAlignment=DMA_PDATAALIGN_BYTE
Dma.USART2_RX.0.PeriphInc=DMA_PINC_DISABLE
Dma.USART2_RX.0.Priority=DMA_PRIORITY_LOW
Dma.USART2_RX.0.RequestParameters=Instance,Direction,PeriphInc,MemInc,PeriphDataAlignment,MemDataAlignment,Mode,Priority

Dma.USART2_TX.1.Direction=DMA_MEMORY_TO_PERIPH
Dma.USART2_TX.1.Instance=DMA1_Channel7
Dma.USART2_TX.1.MemDataAlignment=DMA_MDATAALIGN_BYTE
Dma.USART2_TX.1.MemInc=DMA_MINC_ENABLE
Dma.USART2_TX.1.Mode=DMA_NORMAL
Dma.USART2_TX.1.PeriphDataAlignment=DMA_PDATAALIGN_BYTE
Dma.USART2_TX.1.PeriphInc=DMA_PINC_DISABLE
Dma.USART2_TX.1.Priority=DMA_PRIORITY_LOW
Dma.USART2_TX.1.RequestParameters=Instance,Direction,PeriphInc,MemInc,PeriphDataAlignment,MemDataAlignment,Mode,Priority

NVIC.USART2_IRQn=true\:0\:0\:false\:false\:true\:true\:true\:true
NVIC.DMA1_Channel6_IRQn=true\:0\:0\:false\:false\:true\:false\:true\:true
NVIC.DMA1_Channel7_IRQn=true\:0\:0\:false\:false\:true\:false\:true\:true

ProjectManager.functionlistsort=1-SystemClock_Config-RCC-false-HAL-false,2-MX_GPIO_Init-GPIO-false-HAL-true,3-MX_DMA_Init-DMA-false-HAL-true,4-MX_USART2_UART_Init-USART2-false-HAL-true
```

## Important Generated-Code Constraint

`MX_DMA_Init()` must run before `MX_USART2_UART_Init()`.

## Runtime Pattern

```c
HAL_UART_Receive_DMA(&huart2, rx_buffer, sizeof(rx_buffer));
HAL_UART_Transmit_DMA(&huart2, tx_buffer, sizeof(tx_buffer));
```
