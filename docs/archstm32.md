## Install the tools

- CubeMX
- GNU ARM Embedded Toolchain
	- arm-none-eabi-gcc
	- arm-none-eabi-gdb
	- arm-none-eabi-newlib
- make
- OpenOCD
	- On-Chip Debugger software that will upload compiled code to the STM32
- vscode (optional)
	- stm32-for-vscode extension

## CubeMX Configuration

- Configure Project output to Makefile
```bash
Project Manager->Project->Toolchain/IDE
set to Makefile
```
- Set project to copy all used libraries to the project folder
```bash
Code Generator tab
enable 'Copy all use libraries into the project folder'
```
- Do whatever ever configuration then build
```bash
click 'GENERATE CODE'
```

## VSCode (optional)
- Open the project in vscode
- Write code
```bash
Use Extension Icon or Open the command palette (Ctrl+Shift+P) or Ctrl+Shift+B
Build STM32 Project
Flash STM32
```

## CLI

- cd in to the project
- make (build your code)
    - You'll need to source your toolchain if not already on path
- create this `openocd.cfg` file in your project root
```
# Programmer, can be changed to several interfaces
source [find interface/stlink.cfg]

# The target MCU. This should match your board
source [find target/stm32f4x.cfg]
```
- Program your stm32
```bash
openocd -f ./openocd.cfg -c "program build/<program_name>.elf verify reset exit"
```
