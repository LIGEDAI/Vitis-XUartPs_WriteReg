# XUartPs_WriteReg
## XUartPs_WriteReg函数用法简介
### 1.基本定义
基本定义为 `XUartPs_WriteReg(BaseAddress, RegOffset, RegisterValue)`，`baseaddr`是外设的基地址；`reg_offset`是寄存器的偏移地址；`RegisterValue`是要写入该寄存器的数据。该函数用于配置uart
### 2.实例:清除接收溢出中断标志
**XUartPs_WriteReg(uart_instance_ptr->Config.BaseAddress , XUARTPS_ISR_OFFSET , XUARTPS_IXR_RXOVR)**
- **uart_instance_ptr**是一个指向**XUartPs**结构体实例的指针，**XUartPs**结构体包含了 UART 配置信息
- **Config.BaseAddress**是该 UART 外设的基地址。
- 通过**uart_instance_ptr>Config.BaseAddress**可以获取当前 UART 外设的基地址。
- **XUARTPS_ISR_OFFSET**是一个宏，表示 UART 外设的  **中断状态寄存器**（ISR）的**偏移地址**。该寄存器保存了中断相关的状态信息。不同的 UART 中断源的状态（如接收溢出、发送完成等）会在该寄存器中设置不同的标志位。
- **XUARTPS_IXR_RXOVR**是一个宏，表示**接收溢出中断**（RXOVR）的标志位值（即指示哪一位代表接收溢出中断）

为了清除中断标志位，软件需要写入1到 ISR 寄存器的相应位置（即写入与 RXOVR对应的值，通常是**XUARTPS_IXR_RXOVR**）。这种“写 1清除”的机制是硬件的设计方式之一。写入1时，硬件将检查中断标志位的当前位置，并将其清除。如果你写入了与某个中断源相对应的值（例如**XUARTPS_IXR_RXOVR**），硬件会识别并清除与该值对应的标志位。
