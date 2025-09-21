---
date: 2025-09-21
draft: false
title: Adding CANBus to my 3D Printer with an EBB Upgrade
categories: [3D Printing]
tags: [CANBus, EBB, 3D Printing, Klipper, Bigtreetech]
---

Recently I added an upgrade to my 3D printer that I'm really excited about as it takes advantage of quite a few different technologies that I haven't used before. Primarily the use of CANBus and Klipper's multi-MCU processing capabilities.

In short the upgrade uses CANBus to communicate between the printer's mainboard and the PCB placed on the tool head, drastically reducing the number of cables down from ten plus down to four, two for twelve volt power and a twisted pair of CANBus wires for data and signalling.

What makes this great is that it reduces the number of wires that take up my electronics box in the base of the printer. Before I had a number of fan wires, a stepper motor cable, sensor wires and hotend heater cables but now all I have is the CANBus wires plugged into a simple 2 pin header on the board with the power connections being handled outside the electronics box. 

This means that I don't have to manage the lengths of ten different cables and how they'll all route around the print head, down the printer and into the controls box. Should I want to make any other upgrades in the future it also clears the way for an additional motor driver. My mainboard of choice, a Bigtreetech Manta E3EZ arrived equipped with five motor drivers, X, Y, Z, Extruder Zero and Extruder One. By moving the motor driver to the print head I now have two additional motor driver ports should I wish to hook up and independent Z axis or and additional motor for the Y axis which drives the now quite heavy heated bed.

Setup on the software side was a little finicky requiring complex button combinations to put the STM32 microprocessor into DFU mode to install Klipper but after that (and enabling USB to CAN mode on the E3EZ) it operated flawlessly. 

Though this upgrade didn't affect print quality too much it will make any maintenance a breeze in the future.