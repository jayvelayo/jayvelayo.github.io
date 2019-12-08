---
title: Rise N' Shine
layout: post
category: Project
date: 2018-11-02
---

<img src="/assets/risenshine-files/overview2.JPG" class="fit image"> The Rise N' Shine project aims to automate the opening and closing of blinds based on the current sun position. Its purpose was to utilize the natural sunlight to maximize the amount of light in the room. It also allows a convenient solution for people who depend on sunlight to synchronize their circadian rhythm to the natural sun.

# Project Summary

The project serves as a continuation of embedded system design practice. However, the main focus on this project is the development of software as a tool to practice real-time design. The system should be able to perform the following functions:

* Grab sunrise/sunset times from the internet
* Update the timekeeping system to the current time
* Open and close the blinds as required

The system uses an MSP430G2553 as the main microcontroller with a ESP8266 microchip (in an ESP-01 module) as a Wifi transreceiver. The MSP430 and ESP8266 communicates through UART with a custom API created to ease the communication process. A stepper driver was used to interface the MSP430 and the stepper motor.

The limitation of the MSP430 is the lack of a kernel capable of performing time slicing. As a result, the controller juggles through numerous tasks using event-driven programming. However, the drawback is that each tasks can only be done one at a time.

Overall, the system fulfills the three set requirements. However, this is due that these requirements have soft limits that can easily be broken. For a fully responsive system capable of doing more, a better controller with a concurrent programming functionality will fix the found problems.

# Table of Contents
* auto-gen TOC:
{:toc}

# Electrical and Board Design

The board is similar to the created board found previously in the [AutoSprinker post](https://jayveevelayo.com/project/2018/09/20/Autosprinkler/). However, it accepts a 5V input from the wallwart rather than the 12V. The PDF of the schematic using KiCAD is found [here](/assets/risenshine-files/RiseNShine-schmatics.pdf). It contains the 3.3V voltage regulator shared by the MSP430 and ESP8266. The 5V is fed directly to the ULN2003A driver, which controls the current flow of the stepper motor windings.

# Mechanical Design

<iframe width="560" height="315" src="https://www.youtube.com/embed/u_h9PCJ-8aE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The blinds contain two hanging string that controls the angle of rotation of the blinds. A timing belt is attached to both ends, forming a loop. The stepper motor, located at the windowsill, moves the belt as required to change the angle. The chosen stepper motor, 28BYJ-48, moves one rotation per 4096 steps. It takes 3 rotation for the blinds to move approximately 80 degrees.

# System Software Design

The bulk of the work in the project involves the software portion. From the three requirements set originally, a detailed list can be recreated:

* Establish a communication channel between MSP430 and ESP8266
* Develop a timekeeping module
* Manage the modules of the MSP430

## Message API

With the MSP430 lacking its own wifi capabilities, the ESP8266 is used. Since the ESP8266 only has two GPIO, it can't perform as a standalone microcontroller. Therefore, using UART, a communication protocol is created such that the two chips can send messages to each other. A 9-byte packet is sent between the two for each command. Its structure has a start byte, command byte, 6 data byte which are 3 32-bit data divided into its Most significant and least significant byte, and a checksum byte. 

<img src="/assets/risenshine-files/packet_uml.png" class="fit image">

To standardize the sending/receiving of packets, a base class called MessageAPI is created. Since each chip have their own implementation of the serial port, derived classes based on the chip is created. The base class allows a unified approach when sending packets to each other, eliminating complexity and sources of errors.

<img src="/assets/risenshine-files/api_uml.png" class="fit image">

## Real-time Design challenge

The MSP430 is in charge of numerous tasks from its modules. To tackle the juggling of multiple tasks without the capabilities of multithreading, event-driven programming is used. Each tasks is given a hardware interrupt which will raise a flag that it should be processed. The main loop polls for each flag and checks if a task requires to be processed. The biggest drawback in this design is that a task will not start until the current task has finished being processed. This may cause some tasks to miss its deadline if a task takes too long to finish. However, because the times are soft limits, tasks can be completed with a large margin of time error. For example, even if the opening of blinds is delayed by 1 minute, in the grander scheme of things, this is inconsequential. Therefore, for this specific purpose, the use of such design is sufficient.

# Testing and Validation

## Mechanical Test

A custom program was created such that the controller accepts commands through UART. This test judges if the programmed state machine is working correctly when used. It also measures how many steps required to change the angle of the blinds. It's shown during test that the stepper may skip steps if the strings are caught within the blinds. An addition of a sensor to measure the angular position would greatly improve the mechanical system.

## Software Test

<div class="row">
	
<div class="column">To test the functionality of the Message API, a custom C# program was created. This simulates the sending of packets using the GUI. The two columns translates the data into different format. The left column represent the raw value of the byte. The right column translates the bytes into its ASCII values. The right column is used primarily as a debugging tool to place strategic <i>Serial.print()</i> to see if certain lines are being executed.
</div>
<div class="column"><img class="fit image" src="/assets/risenshine-files/gui.png"></div>
</div>

# Conclusion

The greatest challenge I faced in this project is the assurance that the tasks can be done within its deadline. For a limited microcontroller, the event-driven approach fulfill its specified functionalities. However, there are some aspects that are still open for improvements. An example is to implement a much more effective low power strategy to reduce power consumption. Overall, it was a great experience working with both MSP430 and ESP8266 to design an effective software program.




