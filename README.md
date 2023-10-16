# IP-Bus
**Inter-Protocol Bus**

![Bus Layout](https://github.com/cdg66/IP-BUS_figures/blob/main/BUS_layout.svg)

## What is IP-Bus?

 It's a serial bus design to aggregate to one to multiple differential pair many low speed serial bus found in modern electronics.
 As low speed serial bus examples are UART, SPI, I2C, I2S, SPDIF, CAN, GPIO, PWM, PCM, etc.

IP-Bus is also great for general purpose communication between controller because of its simple protocol.

## Bus design

The Bus is based on the M-LVDS(aka, TIA/EIA-899). It's design to support multipoint from the get go. Up to 32 device (30controler/brige and 2 endbus bridge) can be connected to a single differential lane. Multiple serial connection (like in a backplane) can be added to increase speed. The clock is embeded into the datastream so no need to add a clock lane. An optional clock can be added to sychronise function like audio.

## Packet achitecture

**to be written**

![Protocol stack](https://github.com/cdg66/IP-BUS_figures/blob/main/Protocol_stack.svg)
