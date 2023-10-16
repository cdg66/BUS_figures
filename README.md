# IP-Bus
**Inter-Protocol Bus**

![Bus Layout](https://github.com/cdg66/IP-BUS_figures/blob/main/BUS_layout.svg)

## What is IP-Bus?

 It's a serial bus design to aggregate to one to multiple differential pair many low speed serial bus found in modern electronics.
 As low speed serial bus examples are UART, SPI, I2C, CAN, PWM, PCM, etc.
 
 This bus can also support more general usage like, humain-machine interface (keyboard), audio (I2S, SPDIF), low-resolution video (spi tft lcd), motor control (stepper), General Purpose Input Output (GPIO), etc.
 
IP-Bus is also great for general purpose communication between controller because of its simple and modular protocol.

## Bus design

The Bus is based on the M-LVDS(aka, TIA/EIA-899). It's design to support multipoint from the get go. Up to 32 device (30controler/brige and 2 endbus bridge) can be connected to a single differential lane. Multiple serial connection (like in a backplane) can be added to increase speed. The clock is embeded into the datastream so no need to add a clock lane. An optional clock can be added to sychronise function like audio.

## Bus Devices

![Protocol stack](https://github.com/cdg66/IP-BUS_figures/blob/main/Controller_Bridge.svg)

## Packet achitecture

### Protocol layer (P)

### Network layer

#### Contol Messages (C)

#### Interrupt Messages (I)

#### Bomerang Messages (B)

#### Stream Messages (S)

### Bus Position Identification (BPI)

### High level Messages

![Protocol stack](https://github.com/cdg66/IP-BUS_figures/blob/main/Protocol_stack.svg)


