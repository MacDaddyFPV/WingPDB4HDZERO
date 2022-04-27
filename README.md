# Wing PDB For HDZERO

## Introduction

This project was created from a desire to use the HDZERO video transmission system on wings and planes without a flight controller.
As the HDZERO system requires MSP communication to transmit and display OSD inormation, it is required to use some sort of microcontroller to do this.

It was suggested that a cheap flight controller could be used, but generally there are not cheap flight controllers which also have pdb style pads and regulators with sufficient amperage to power servos via a pwm reciever. The flight controllers also have a lot of unused components for this use case such as gyro and osd chip. With all this in mind, I decided to delve into designing a board which has minimal required components to save on cost and also provide the power supply requirements for a standard wing.

## Design

The deign was created using the free EasyEDA software. This software is provided by JLCPCB in can output files that can be used directly for ordering PCBs.
A feature of this design that I aimed for was to enable the components to be assembled by JLCPCB directly so they boards can be used without any components needing to be attached by the user. To acheive this the board only has components on one side, this also means it is easier to tape or glue down inside a wing bay or fusalage.

The board uses an stm32f411 mcu to recieve voltage via ADC and send OSD via MSP. The firmware used for the board is currently INAV 4.1 as it is easy to setup and provides a stable OSD output to the VTX. This is achieved by flashing a custom hex file which has been compiled with minimal required settings required for the board to function and provide OSD.

The board has a number of solderable pads for connecting to the peripherals. They are:

* Esc and Power Pads - These are interconnected to provide direct battery voltage to one or two ESCs
* RX Power and Ground - This is the connection point for the PWM RX which has wide trace and is close to the 5v regulator
* TX1, RX1, 5v and Ground - This is for connecting a plug to allow the connection of a hot swap sbus/fport/crsf rx to allow stick commands to be used on the ground
* TX2, RX2, VBAT, Ground - this is for connecting the HDZERO VTX to the board.

The pads (besides the power pads) on the revision 1.4 have been spaced and have the hole sizes to fit standard Dupont pins.

## Ordering

It is recommended that if possible, find a number of people who wish to also buy some of these boards and do an order together. The more boards ordered at once, the lower the cost will become per board.

The files provided in this repository under Fabrication can be used directly with JLCPCB to order boards. These files are:

* Gerber file (.zip)
* BOM (.csv)
* Pick and place file (.csv)

To start, dowload these files from github the in a browser fo to https://jlcpcb.com
Create an account and sign in.
Click on "Order Now" and make sure you are on the PCB tab
Click on "Add gerber file" and select the Gerber zip file that was downloaded
After the file has uploaded you should see a front and rear picture of the PCB layout
Select the PCB Qty for the number of boards you wish to order and leave the remainder of the settings as defualt
