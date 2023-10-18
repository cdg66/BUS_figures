# SHER-Bus
> **Warning**
> Content is not fixed and suject to change without notice!


**SHER-Bus**

**S**ystemwide **H**ub for **E**fficient **R**outing **Bus** 

or

**S**HER-Bus **H**andles **E**xtensive **R**esource **B**ridging, **U**nifying **S**ystems

![Bus Layout](https://github.com/cdg66/SHER-BUS_figures/blob/main/BUS_layout.svg)

## What is SHER-Bus?

 It's a serial bus design to aggregate many low speed serial bus found in modern electronics to one/multiple high sppeed differential(s) pair(s) .
Low speed serial bus examples are SPI, I2C, CAN, PWM, PCM, etc.
 
 This bus can also support more general usage like, humain-machine interface (keyboard,keypad,game controller,joysticks), audio (I2S, SPDIF), low-resolution video (monochome oleds,spi tft lcd), motor control (stepper), General Purpose Input Output (GPIO), etc.
 
SHER-Bus is also great for general purpose communication (like UART , JASON, protobuf, modbus, etc) between controller because of its simple and modular protocol.

## Bus design

The Bus is based on the M-LVDS(aka, TIA/EIA-899). It's design to support multipoint from the get go. Up to 32 device (30controler/bridge and 2 END bridge) can be connected to a single differential lane. Multiple serial connection (like in a backplane) can be added to increase throughput. The clock is embeded into the datastream so no need to add a clock lane. An optional clock can be added to sychronise function like audio.

## Bus Devices

![Device_Types](https://github.com/cdg66/SHER-BUS_figures/blob/main/Controller_Bridge.svg)

## Packet achitecture

### Protocol layer (P)

### Network layer

#### Contol Messages (C)

#### Interrupt Messages (I)

#### Bomerang Messages (B)

#### Stream Messages (S)

### Bus Position Identification (BPI)

### High level Messages

![Protocol stack](https://github.com/cdg66/SHER-BUS_figures/blob/main/Protocol_stack.svg)


