# STM32F407 USART1 作业记录

## 实验现象

STM32F407VGT6 通过 USART1 以约 1 秒为间隔发送 `Hello World!`。串口收发已由本人在开发板上验证；本记录没有附接收界面截图。

## 配置过程

- 使用 STM32CubeMX 配置 USART1 异步模式：PA9 为 TX、PA10 为 RX，115200 波特率、8 位数据、无校验、1 位停止位、无硬件流控。
- 使用 8 MHz HSE，经 PLLM=4、PLLN=168、PLLP=2 得到 168 MHz 系统时钟；AHB=/1、APB1=/4、APB2=/2。PLLQ=7，48 MHz 分支为 48 MHz。
- 在 `main.c` 中初始化 USART1，调用 `HAL_UART_Transmit` 发送字符串，并用 `HAL_Delay(1000)` 控制发送间隔。
- 清理此前 LED 呼吸灯和舵机实验的自编代码。

## 调试记录

- 工程使用 CMake 与 Arm GNU 工具链编译，编译和链接通过。
- 曾遇到 OpenOCD `open failed`，重新连接 ST-Link 后成功烧录；终端显示 `Programming Finished`、`Verified OK` 和 `Resetting Target`。
- 串口调试时使用 115200、8-N-1，并确认开发板和串口接口共地。ST-Link RX 接开发板 TXD，ST-Link TX 接开发板 RXD。

## 结果截图

本次尚未将串口接收截图加入仓库。提交作业前可将截图放入 `docs/`，并在此处添加链接。
