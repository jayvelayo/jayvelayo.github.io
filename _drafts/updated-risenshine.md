---
title: Updated RiseNShine
layout: post
---

The updated RiseNShine aims to make use of the FreeRTOS-ESP8266 SDK to fulfill new software requirements. These new software requirements enhances the product by providing a convenient user interface to allow debugging or monitoring. 

## Project Summary

The new RiseNShine project aims to increase both the responsiveness of the system and maintainability to easily create new features. From updating both the hardware and software aspect of the project, the system was able to be miniaturized and

Updated RiseNShine. Challenges before: not responsive, limited processes, and rigid.

## Project Requirements

New functional requirements for the RiseNShine project as follows:

1. Regularly obtain current/sunset/sunrise times using HTTP GET
2. Parse obtained JSON information to extract data
3. Communicate with MSP430 to update times through UART
4. Accept clients for monitoring and controlling using TCP/IP 

## Software Architecture

Using FreeRTOS as a real-time kernel to develop a responsive system. 

Layers:

* Interrupts
* Kernel
* Clock management
* TCP Server
* Blinds control
* Background tasks

// add figure eg. timing diagram?

## Firmware Development

Modularity of code

## Testing

Since they are modular, it's easy to create unit tests.

## Future opportunities

Enable the RiseNShine_IoT as a hub to control multiple other smart products. PnP capabilities in the future
