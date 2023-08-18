<!--
SPDX-FileCopyrightText: 2023 Jan Nieuwstad <jan.sources@nieuwstad.net>

SPDX-License-Identifier: CC-BY-SA-4.0
-->

### Ownership and License


### Overview

The DCL8010 electronic load module features a DC Electronic Load with several modes and protections.
This project is the for the development boards for this project.

### Specifications

* Modes: Constant Current (CC), Constant Voltage (CV), Constant Power (CP) and Constand Resistance (CR). CC and CV are implemented in hardware, CP and CR are software controlled and have a slower dynamic response.
* Limits:
** Current: 1mA - 10A set and read
** Voltage: 0.5V - 80V (set), 1mV-80V read
** Power: 80W

* Protections:
In hardware:
** Over Voltage Protection, clamps load off 
** Over Current Protection, clamps load off
With software support:
** Over Power Protection
** Over Temperature Protection

* Other hardware features:
** Von: The minimum voltage needs to be present before the load is turned on. This can be set with or without latching.
** Temperature based fan controll
** Fan RPM readout
** Heatsing temperature readout

### Limitations / Issues

* The ADC and DAC are on a seperate PCB's. This causes some offset errors. Especially in the Imon/Umon. This might also be caused by the next issue
* The current implementations use TL431 for voltage reference. This is not good enough. 
* Von causes some oscillation when the voltage slowly decreases to the set level. This is noticable in a typical battery discharge test. As this ia a very valid and common
* The power supply board is a very simplistic set of 78** / 79**. Ok for testing, but needs to be replaced with something decend
* Reverse polarity is a very crude diode: Implement a proper reverse polarity circuit preferabbly with a detection to software (nice to have)
* Add a fuseholder
* Test with real LM3/150 heatsink using screwmounting and isolation.


Hardware changed needed to become a proper DIB module/BB3 module:

* This is a DIB module size but it needs:
** DIB connectors in place
** move the ADC and DAC to analog board
** Implement a connector for a piggy board containing an MCU (probably a RP2040). This board has 2x SPI , 1x I2C. I think this is needed because of size, but not sure.
** add banana connectors 
* design front panel
* consider reversing the BB3 airflow 

### TODO

* Replace TL431 reference with an REF5025
* Move the ADC and DACs to the Analog board. The connection to digital will be SPI & I2C only
* Replace the -2.5 volt power for a proper LDO. Currently a TL431 with a resistor is used.
* Test the ADC clamp circuits, they are on the PCB but I didn't test it yet.
* Implement voltage range switching. 
* Implement a low current range (if needed/feasible)
* 
