---
layout: post
title: AutoSprinkler using MSP430
date: 2018-09-20
---
<img src="/images/fulls/autosprinkler.jpg" class="fit image"> The Automatic Sprinkler system uses an MSP430G2553 to monitor and control soil moisture levels of multiple plants. The idea behind this system is that different potted plants may require different watering needs. Its automated system aims to provide the user the ease of mind with regards to the health of the plants. 

# Project Description

The project serves as a practice opportunity to showcase embedded system design principles. The system is considered a success if it fulfills the following requirements:

* Power regulation to provide 12V, 5V and 3.3V for individual modules
* Integrated relay module to control water pump
* Constant monitoring of soil moisture levels
* Consistent timer interval
* Implement power saving techniques when possible

The designed board contains the power regulation, relay, and controller which requires a 12V power source. Two LM317T IC is used to step the 12V down to 5V and 3.3V. The relay uses a TIP120 Darlington pair transistors to power the water pump using the controller. 
The system uses MSP430G2553 as the controller of the system. The controller’s features such as low-power mode, ADC, and integrated timer makes it an ideal component. It’s responsible of collecting readings from the moisture sensor, activating the relay for the water pump, and controlling the servo to redirect water flow. When not in use, the controller enters low power mode to save energy. Every 24 hours, the controller wakes up from low power mode to collect data and perform the appropriate actions.
