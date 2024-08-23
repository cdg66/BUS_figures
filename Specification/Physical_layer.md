# Physical layer

> [!Warning]
>
> Reader must be fammiliar with M-LVDS or LVDS signaling. 
> For more information on the technologie please read ![this](https://www.ti.com/lit/an/slla108a/slla108a.pdf?ts=1724243591163&ref_url=https%253A%252F%252Fwww.google.com%252F).

This section describe the implementation of the lowest level of the SHER-Bus communication protocol.

## Bus configuration 

![Bus Layout](https://github.com/cdg66/SHER-BUS_figures/blob/main/Figures/BUS_layout.svg)

A SHER-Bus communication channel consist of a 100 ohm differential twisted pair. At each end a 100 termination resistor is placed in order to have a half duplex transmission line. 

## Tranceiver



The bus officially support Multipoint Low Voltage Signaling or M-LVDS. Furthermore, SHER-Bus only support Type 2 tranciver as the channel can go into an idle state where nobody talk. The tranceiver can be external or internal to the application IC but fully integrated is recomended as it simplify system mignaturisation. In other word the IC might expose the single ended port or the diffierential port. 

The typical name for the pin of a M-LVDS tranceiver are (A,B,R,RE,DE,D). For clarity in schematic these pins have been renamed.

| M_LVDS Tranciver PIN | Description           | SHER-Bus Rename | Alternative name |
|----------------------|-----------------------|-----------------|------------------|
|           A          | Differential Positive |       SB_p      |        SB+       |
|           B          | Differential Negative |       SB_n      |        SB-       |
|           R          |  Single ended recive  |        R        |        RX        |
|          RE          |     Recive enable     |       REN       |       RX_EN      |
|          DE          |    transmit enable    |       DEN       |       TX_EN      |
|           D          | Single ended transmit |        D        |        TX        |



### Using other tranceiver

Sherbus dosent disallow other tranciver technologie like RS-485 or CAN but strongly discourage their use as they are not tested and will limit the bus speed. It will be the bus implementer responsability of verrify the compatibility.

## Packet coding

A data packet is composed of a 256 bits preceded by 2 start bit. 

## Bus device

![Device_Types](https://github.com/cdg66/SHER-BUS_figures/blob/main/Figures/Controller_Bridge.svg)

There are only 3 types of devices in the bus network, each serving a different function.

First there is the controller that generates data packets for others to parse. They give the bus its function. For instance, the controler can give commands to a bridge for it to read an i2c temperature sensor. The controller then interprets that data and adjusts a SPI DAC to output a value for the control of a Fan. They can also give commands to other controllers on the same bus. So in other words their job is to be the brain of the communication. They consist of mostly of Microcontrollers, Embedded computers (Raspberry pi) or FPGAs.

![controller example](https://github.com/cdg66/SHER-BUS_figures/blob/main/Figures/Controler_example.svg)

Secondly there is the bridge whose job is to close the gap between the new bus and the already existing protocols. They can have mutitude of serial buses (up to 6 and 1 general control channel using [BPI]). They consist of mostly ASICs or FPGAs. Altough at the time of this writing no ASIC or FPGA code as been manufactured/written. Microcontrolers can also act as bridges. Briges can be integrated into already existing designs in die or in multi-die package. Folowing the design-once-reuse-everywhere rule, it helps reduce redesign complexity and speeding up time to market. Bridge implementers need to be careful about licensing of existing buses as some are not free to implement.

![MultiDiedesign](https://github.com/cdg66/SHER-BUS_figures/blob/main/Figures/Intergrated_bridge.svg)

Thirdly, There is the End bridge whose job is to connect multiple SHER-Buses together or other HIGH-SPEED buses (like USB, SDIO or Ethernet). They terminate the bus (where the temination resistor are) that's why they are a limit of 2 that can be connected on the bus. They are complex and not mandatory.

