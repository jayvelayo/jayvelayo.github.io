---
title: Updated RiseNShine
layout: post
category: Project
---


The updated RiseNShine aims to make use of the FreeRTOS-ESP8266 SDK to fulfill new software requirements. These new software requirements enhances the product by providing a covenient user interface to allow debugging or monitoring. 

# Project Summary

Using the NodeMCU board, the MSP430 and ESP8266 is combined to create a real-time system. The FreeRTOS will be used to fulfill time-based requirements and allow multi-module communication. This upgrade aims to compact the hardware as well as create a more cohesive and responsive software.

New functional requirements for the RiseNShine project as follows:

1. Regularly obtain current/sunset/sunrise times using HTTP GET
2. Parse obtained JSON information to extract data
3. Control stepper motor as required
4. Manage system clock
5. Create TCP Server
6. Respond to client request on TCP server
7. Request current time using NTP (optional)

The above functional requirements will be the underlying guide when designing the workflow of the software.

# Software Architecture

From the above requirements, tasks are created with differing priorities. I decided to go with the following structure in decreasing priorities:

ISR:
RTOS Kernel: FreeRTOS
Task 1: TCP server management
Task 2: Blinds controller
Task 3: Processing and Idle tasks

This TCP server management is given the highest priority as user experience is highly desired. Therefore, the most important deadline that the system should meet is the handling and response to the client. Contrasting this to the requirement of the updating of sunrise and sunset time, failure to update time doesn't affect the experience nor the purpose of the system. 


## Interrupt Service Routines

This one controls the system time and check if it's time to update

## TCP server management

The TCP server is used such that clients are able to communicate and enter commands for the risenshine system. The client should be able to:

* Retrieve saved sunset, sunrise and system time
* Manually control the blinds as needed which includes rehoming the blinds
* Change configuration setting

As of now, the system can accept the first two requests. However, the goal of the TCP server is to allow remote access as a developer to debug and modify system configuration. This is saved for future builds.



## Blinds controller

Because the MSP430 has been removed, the ESP8266 has to take up the new responsibilities. The biggest advantage of this move is that there is less latency as it doesn't require UART communication to send data. While this may add strain to the kernel, the added work should not affect significantly affect the performance.

## Idle tasks

HTTP GET AND PARSE IS IN HERE


## FreeRTOS initialization

Communication using Qs

# Modules


