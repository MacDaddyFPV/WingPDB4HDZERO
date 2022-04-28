![alt text](https://github.com//MacDaddyFPV/WingPDB4HDZERO/blob/main/Resources/HD0WB1.png?raw=true)

# Wing PDB For HDZERO

## Introduction

I will start by saying I am not affiliated with HDZERO or DIVIMATH besides being a user of the system.

This project was created from a desire to use the HDZERO video transmission system on wings and planes without a flight controller.
As the HDZERO system requires MSP communication to transmit and display OSD inormation, it is required to use some sort of microcontroller to do this.

It was suggested that a cheap flight controller could be used, but generally there are not cheap flight controllers which also have pdb style pads and regulators with sufficient amperage to power servos via a pwm reciever. The flight controllers also have a lot of unused components for this use case such as gyro and osd chip. With all this in mind, I decided to delve into designing a board which has minimal required components to save on cost and also provide the power supply requirements for a standard wing. This is my first ever PCB design and I learnt through the process of studying other designs, getting feedback from other designers and of course, trial and error.

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

### Placing an Order

To start:
- Dowload these files from github the in a browser fo to https://jlcpcb.com  
- Create an account and sign in  
- Click on "Order Now" and make sure you are on the PCB tab  
- Click on "Add gerber file" and select the Gerber zip file that was downloaded  
- After the file has uploaded you should see a front and rear picture of the PCB layout  
- Select the PCB Qty for the number of boards you wish to order and leave the remainder of the settings as defualt  
- Scroll down to the bottom and on the SMT Assembly panel press the switch button to open up more options  
- Leave Assemble Top side and Tooling holes by JLCPCB, select the QTY (Above 5 it is fixed to the number of boards ordered) and agree to the Terms  
- Select "Confirm" then the "Next" over on the right side of the page  
- Click on "Add BOM File" then select the BOM file that was downloaded  
- Click on "Add CPL File" and select the Pick and Place file that was downloaded  
- Select a usage description form the drop down such as Electronics and Hobbies - DIY then click Next  
- On this page you want the total parts detected and total parts confirmed to match. If not the case then see **Choosing Alternate Parts** 
- If all parts are confirmed then click Next  
- Review the order and then click "Save To Cart"  
- In the cart enter your address, choose shipping method and make payment
- Once payment is complete you will be able to monitor the progress of your order under "My Orders"

### Choosing Alternative Parts

If you find that not all of the parts are available at the time of ordering you have a few options:
- You could wait until all parts become available again. You can check for stock levels here https://jlcpcb.com/parts
- You can click on the Magnifying Glass icon (search) for the item/s that are out of stock which will bring up a list of components that may be compatible. You will want to select an item with the same footprint and similar attributes. For example there are a number of f411 MCUs that could work as a direct replacement (STM32F411CEU6TR, STM32F411CCU6TR). These replacements should work but are untested.
- You can clone the design and change out the components for something else that will work in its place. If you go with this method it would be appreciated if after the design is confirmed to work, that the Fabrication files along with a link to the design is committed to this repository.

## Flashing

Once you recieve your board from the manufacturer you will need to flash it with the hex file found in the resources folder.  
First You will need to download INAV configurator 4.1 https://github.com/iNavFlight/inav-configurator/releases/tag/4.1.0.  
I would also recomend that if you don't already have the ImpulseRC Driver Fixer that you download it.

To flash:
- Open the INAV 4.1 configurator and click "Firmware Flasher" on the left
- Put the board into DFU mode by plugging in the USB whilst holding the boot button
- If this does not work try running the ImpulseRC Driver Fixer the do the same process
- Once in DFU mode select "Load Firmware [local]" then select the downloaded hex file then click "Open"
- click "Flash Firmware" (ensure "full Chip Erase" is selected) and wait for the flashing to complete
- A new COM Port connection should show up, click "Connect" with this selected to connect

## Setup

