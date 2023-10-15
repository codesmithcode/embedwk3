Repo for the week 3 assignment on blinky lights
https://classpert.com/classpertx/courses/making-embedded-systems/cohort

Board: 
======

stm32f3discovery (https://www.st.com/en/evaluation-tools/stm32f3discovery.html)

Summary:
========
- Button used to turn on / off playback of LED sequence
- Button signal is debounced
- Debugging info via printf / uart
- Button and debounce are implemented via interrupt handling

Build environment:
==================
- STM32CubeMxIDE

Further investigation:
======================

1. What are the hardware registers that cause the LED to turn on and off? (From the processor manual, don’t worry about initialization.)

The LED state is controlled by specific bits set on the GPIOE BSRR HW register

GPIOE: 0x40000000UL + 0x08000000UL + 0x00001000UL = 0x48001000L
BSRR: 0x1A

Bit 9-16 specify control state of LED 3-10


2. What are the registers that you read in order to find out the state of the button?

The button state is exposed by a specific bit on the GPIOA IDR HW register

GPIOA: 0x40000000UL + 0x08000000UL + 0x00000000UL = 0x48000000L
IDR: 0x10
Bit 1 specifies the state of the button


3. Can you read the register directly and see the button change in a debugger or by printing out thes value of the memory at the register’s address?

Yes, by looking at the first bit of the IDR register on GPIOA in the debugger variables or printing out that memory location.

GPIOA: 0x40000000UL + 0x08000000UL + 0x00000000UL = 0x48000000L
IDR: 0x10