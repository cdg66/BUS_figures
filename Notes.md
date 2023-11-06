# Idea notes

things I would like to add to the spec but not sure of there implementation is feaseble.

## Power over twisted pair (POTP)

Wild idea to send power aswel of data over a same twisted pair. We would only need 3 cable instead of 4: A,B,Ground. A power-data decoupler would need to be used before the tranciver.

## have 2 specification

like RISC-V there is two spec privilegied and unprivileged specification. We could do the same for SHER-Bus.

### SHER-Bus Multipoint



### SHER-Bus Point to Point

High speed but only between 2 controler. Use of LVDS instead  SHER-Bus PTP can be connected to a SHER-Bus MTP trough an end bridge.

## SHER-Bus Injection Detection

On many bus like can its easy for and ill intentioned person to inject message that shoun't be present on the bus. heres an [exemple](https://www.youtube.com/watch?v=dkw2iewOjJw). On SHER-Bus beacause we have unique identifier for each controller each one can monitor for someone who try to use its own BPI ID. Or verify for unsupported Application code. Then It can send a Lockdown Command packet and prevent any other packet by sending continus ones preventing any packet. 
