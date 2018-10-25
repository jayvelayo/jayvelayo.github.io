---
layout: post
title: AutoSprinkler using MSP430
category: Project
date: 2018-09-20
---
<img src="/assets/images/fulls/autosprinkler.JPG" class="fit image"> The Automatic Sprinkler system uses an MSP430G2553 to monitor and control soil moisture levels of multiple plants. The idea behind this system is that different potted plants may require different watering needs. Its automated system aims to provide the user the ease of mind with regards to the health of the plants. 

# Project Description

The project serves as a practice opportunity to showcase embedded system design principles. The system is considered a success if it fulfills the following requirements:

* Power regulation to provide 12V, 5V and 3.3V for individual modules
* Integrated relay module to control water pump
* Constant monitoring of soil moisture levels
* Consistent timer interval
* Implement power saving techniques when possible

The designed board contains the power regulation, relay, and controller which requires a 12V power source. Two LM317T IC is used to step the 12V down to 5V and 3.3V. The relay uses a TIP120 Darlington pair transistors to power the water pump using the controller. 


The system uses MSP430G2553 as the controller of the system. The controller’s features such as low-power mode, ADC, and integrated timer makes it an ideal component. It’s responsible of collecting readings from the moisture sensor, activating the relay for the water pump, and controlling the servo to redirect water flow. When not in use, the controller enters low power mode to save energy. Every 24 hours, the controller wakes up from low power mode to collect data and perform the appropriate actions.

# Table of Contents
* auto-gen TOC:
{:toc}

# Electrical and Board Design

<img src="\assets\Autosprinkler-files\board.JPG" class="fit image">

Because this project was a way to showcase my skill in embedded system design, I've used the MSP430 instead of an Arduino. This allowed me to build the board from the ground up which would give me valuable insight in the design of the board. I separated the board design into three distinct parts - the power regulator, the microcontroller, and the electronic switch. I constructed each parts in the order I mentioned and performed functional tests to ensure that the system will become operational. This is a [PDF of the schmatic made using KiCAD](\assets\Autosprinkler-files\AutoSprinkler_schematics.pdf).

## Power Regulation design

The system is fed a 12V DC source using a wallwart. A diode is placed in series right after the 12V Barrel jack as a protection in case of a reverse polarity. Decoupling capacitors are placed at the input and at each output to reduce noise. This subsystem proved to be a challenge since I learned that the power regulation is usually the cause of headaches to junior designers. This forced me to research and learn about good design practice to ensure system stability and safety.

## Controller and Switch design

The controller design was straightforward due to the information provided by the datasheet. The challenge was the installation of the 32.768kHz crystal. Initially, the clock wasn't working due to possibly stray capacitance or shorting of the XIN/XOUT pins. This was solved by simply adding a standoff such that there's a minimum of 5mm distance between the board and surface.

The relay switch design features a BJT NPN Darlington-pair transistor. I specifically chose the Darlington-pair due to its high gain, which would require a low current from the microcontroller. A flyback diode was also added across the pump terminal to protect the pump.

# Mechanical Design

The goal of the mechanical design is to direct water flow to individual plants using the least resources required. I initially had numerous ideas such as having a rotating nozzle, or use a rail system to move the nozzle. I ended up designing a "water multiplexer" inspired by the electronic multiplexer. Using a servomotor, I attached the two tubes in opposite direction onto the servo arm. This works by setting spliting the fluid line from the pump right before the servo. At one state of the servo, one line is straight (which allows fluid flow) while the other line is bent at 180 degree angle. If the servo rotates 180 degree, the reverse will be true where the previously bent line will be straight while the other line is closed due to bending.

The pump remains inside a reservoir of water. However, the reservoir must be refilled every week manually. My recommendation to improve the design is to add a reed switch to detect low water supply. It's also possible to connect the water line to an actual water line but steps must be done to reduce water pressure.

# System Software Process

The microcontroller uses two timer A modules, and the ADC10 module. The first timer A module is used to keep track the amount of minutes has elapsed. This is done using the 32.768kHz clock which is further divided by 64. The time tracking is required as the system wakes up once per day to check the sensor readings and water the plant if needed. My rationale behind the long interval is that the plant doesn't really need to be watered as soon as they're dry. The other timer A module is used for a 50Hz PWM signal. This is powered by the internal DCO clock and is used to control the servomotor. 

The ADC10 module is used to collect analog signal from the moisture sensor. The 3.3V reference gives a 3.22mV resolution which is more than enough for this application. The moisture sensor is simply a variable resistor which is dependent on the moisture level. Higher voltage readings signifies less moisture in the soil. Two values are important for each plant, the wet and dry value. Readings above the dry value tells the system its time to water the plants. Readings below the the wet value indicates that the soil has reached desired moisture level and water flow should be stopped.

The source code can be found [here](https://github.com/jayvelayo/AutoSprinkler).

The main advantage I found in using the MSP430G2553 is the low power features. Because the system only wakes up once a day, I'm able to utilize the various low power features. For example, when not in use, the system enters low power mode with the 32.768kHz clock only running. In this state, current draw is only around the 1uA range.

The overall system process is straight forward. No concurrency programming techniques used due to the mechanical bottleneck and flexible time sequence. A flowchart is [shown here](\assets\Autosprinkler-files\Flowchart.png)

# Testing and Validation

Throughout the project, unit tests, regression tests, and system test are employed to ensure system meets functionality. The following section discusses the methodology used:

## Electrical Tests

As mentioned, the process of building the custom board was done by adding subcomponents and performing regression tests. In this case, I built the power regulator first to create my power supply for every other component. The test result is simple, I should have a line regulation of about +/- 0.1V. I didn't do a load regulation test since theoretically, the system should draw little output current at all. The next stage was adding the microcontroller chip. Connection from the chip legs to the header pins is tested using the continuity mode of the multimeter. Lastly, the electronic switch is tested in combination with the next mechanical test.

## Mechanical Tests

The mechanical part of the system has the pump and servo. The pump is tested by programming the microcontroller to accept a button press to activate the electronic switch. Each button press will toggle the output of the base pin of the BJT transistor. The servo test is done by adding the previous program to allow rotation the servo arm by 180 degree with a button press. The goal is that only one of the two water tube will allow water flow at a time.

## Software Tests

With the microcontroller, I used the clock, timer, and ADC module. Using the clock and the 32.768kHz crystal, I am able to obtain a 1Hz interrupt interval. Because I don't have an oscilloscope, I programmed an LED to toggle each interval tick. This is compared against a clock to measure 1Hz frequency. The other use of the timer module was to create a PWM for the servo. This is a simple test where I aim to rotate the servo by 180 degrees by changing the values of register. Lastly, the ADC is tested using the soil sensor. I was also able to use this opportunity to calibrate the threshold values for the plants.

# Conclusion

I left the AutoSprinkler for a week to see its effectiveness. The research and tests I've performed paid off as the system met its functional requirements. In the week of independence, the plants have not (and hopefull will not) withered due to dehydration.

After reviewing my code, I also found some opportunities to improve my code. For one, I maintained to have delay_cycles. Despite it only being 1 second long, it still can be improved by using the existing timer to generate another interrupt.

As a first personal project, this was an exciting process where I learned numerous design practices first hand. This has also assured me that this types of projects aligns with my passionin building embedded systems. I'm starting another project so stay tuned for more!

# References

* [Electrical Schematics](\assets\Autosprinkler-files\AutoSprinkler_schematics.pdf)
* [Source code](https://github.com/jayvelayo/AutoSprinkler)


