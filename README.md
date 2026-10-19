# STM32F103C8T6 流水灯（课后作业）

基于 STM32F103C8T6 最小系统板 + 面包板 4 个 LED，用软件实现流水灯效果。

## 功能说明

- 4 个 LED 接在 PA1 ~ PA4，依次点亮，每个亮 300ms，循环往复，形成"光点流动"效果
- 逻辑位置：`Core/Src/main.c` 的 `while(1)` 循环内（`USER CODE 3` 区）

## 硬件连接

| LED | 引脚 | 限流电阻 | 接法 |
|-----|------|----------|------|
| LED1 | PA1 | 220Ω ~ 1kΩ | 3.3V → 电阻 → LED 阳极 → LED 阴极 → GPIO（低电平点亮） |
| LED2 | PA2 | 220Ω ~ 1kΩ | 同上 |
| LED3 | PA3 | 220Ω ~ 1kΩ | 同上 |
| LED4 | PA4 | 220Ω ~ 1kΩ | 同上 |

> 代码按「低电平点亮」编写（`GPIO_PIN_RESET` 点亮）。若实际接法是 GPIO → 电阻 → LED → GND（高电平点亮），把代码里的 `RESET` / `SET` 互换即可。

## 开发环境

- IDE：CLion 2026.2（CMake 工程）
- 编译器：arm-none-eabi-gcc
- 配置工具：STM32CubeMX（STM32Cube FW_F1 V1.8.7）
- 下载/调试：ST-Link + OpenOCD（SWD：PA13 / PA14）
- 芯片：STM32F103C8T6，LQFP48，主频 8MHz（HSI）

## 编译与烧录

1. 用 CLion 打开本工程（`clion_demo666.ioc` 为 CubeMX 配置）
2. 选择 CMake Profile（Debug）
3. Build
4. 连接 ST-Link，Run / Download 烧录到开发板

## 目录说明

```
Core/            用户代码（main.c、gpio.c、HAL 配置）
Drivers/         STM32F1 HAL 库与 CMSIS
cmake/           GCC 交叉编译工具链配置
CMakeLists.txt   工程构建脚本
startup_stm32f103xb.s  启动文件
STM32F103xx_FLASH.ld   链接脚本
clion_demo666.ioc      STM32CubeMX 工程配置
```

## 效果

面包板上 4 个 LED 从左到右依次点亮、熄灭，形成流水灯效果，循环往复。
