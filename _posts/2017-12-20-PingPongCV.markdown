---
layout: post
title: Ping Pong arm using CV
date: 2017-12-20
---

<img src="/assets/images/fulls/paddlearms.jpg" class="fit image"> The Computer Vision controlled Ping Pong arm serves as a senior mechatronic project. The system has the ability to track a Ping Pong ball and return it using its motor-controlled paddle. It simulates playing Ping Pong with a human opponent. It's made by a two-person team [Jayvee Velayo](http://github.com/jayvelayo) and [Lynx Lu](https://github.com/LynxHack)

<iframe width="560" height="315" src="https://www.youtube.com/embed/_ZPYBEtIChI" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

# Project Description
The project was divided into two main components, the tracking system and the ball return system. The tracking system is primarily done in a C# program to provide user interface and sends commands for the ball return system. To track the ball, it uses two PS4 Eye camera to determine the position coordinates of the ball. Based on individual frames, the program tracks the ball and uses a Kalman filter to predict the trajectory of the ball. It calculates the coordinates of the ball when it reaches the ball return plane and sends the corresponding commands to the hardware.

The ball return system uses a two-ended paddle which uses a 2D coordinate system. The system’s hardware includes two servo motors and two controllers. An MSP430F2274 is used to control a servomotor which is implemented using a DC motor with a rotary encoder. This provides more than 360 degrees precise rotation to move the paddle horizontally. An Arduino is used to control another servo which provides rotational control of the paddle. The controllers receives instructions from the C# program using UART. Together, they are able to control the XY Coordinates of the paddle.

## Locating the Ping Pong using Camera

The hardware set-up uses 2 PS3EYE to cover all three ball position axis of X,Y, and Z location. In order to get a higher stability for the ball color detection, a higher resolution of 640x480 at 60Hz was chosen instead of 320x240 at 120Hz which still provided enough sampling rate to pinpoint a fast moving ball. Due to the flickering of the ball as it changes position (there may be shadows that affect the circle contour detection). A Kalman filter was implemented to provide some stability to the ball detection. 

<img src="\assets\pingpongCV-files/flowchart.jpg" class="fit image">
 
In order to process each frame, each individual frame capture is taken and converted into HSV color space (hue, saturation, and value) to allow for color filtering of the orange ping pong ball. 

Each of the hue, saturation, and value is then split up into individual images and converted into grayscale. A sliding bar is used to set the threshold range of the grayscale intensity in which any pixel value in between is a 1 while any pixel value outside is a 0. This is then converted into a binary image as can be seen in the figure below. 

<img src="\assets\pingpongCV-files\binarymap.png" class="fit image">

This binary image is then used to trace out the approximated contour by using cvFindContours function to first box the pixel cluster’s minimum and maximum x and y values. It then proceeds to form a best fit circle using the center of the rectangle. From here, the multiple possibilities of ball locations are placed into a sequence. The ball is then drawn by using the average of width and height as its radius.

In order to convert the ball positions in pixels to real world value (later on to be used for paddle actuation), the dimensions of the camera image is measured and used to scale the pixels to centimeters length. It is approximated that the value is 133 cm:320 pixels and 83 cm:240 pixels height for the two cameras mounted 1m away from the table. However, this is subjected to some deviations, since the camera is at a distance away from the table and induces a fish eyes lense type effect. Therefore, the further away from the center the ball is, the more inaccurate the ball position is. 

## Blocking Arm Design

The block arm is a rod with two paddle at each ends. This will help in the reduction of the time response needed to react and block the ping pong ball as each paddle can cover half of the coverage area. The design involves using a servo arm to rotate the arm to reach the upper and lower halves. Two motors are required for this system. One servo is used to rotate the arm 180deg. This servo is then responsible for reaching the vertical coordinates. Another motor is then used to move the arm horizontally on the rail. The motor used is a DC motor with an encoder in order to cover the distance required.

<img src="\assets\pingpongCV-files\dcmotor.jpg" class="fit image">

The approach of this problem involves determining the corresponding two inputs for both motors to determine the fastest response time in ensuring the paddle will be able to block the trajectory of the ball. The team decided that a coverage area of 0.8m x 0.6m (width x height) is a reasonable and attainable result. The MG966R servo is able to rotate the arms at 90 degrees for an approximate 0.6seconds. The FIT0493 DC motor with encoder is able to travel one end to another in 1.5seconds.

Due to the movement in the horizontal rail, the vertical supports must be able to absorb the vibration due to the response of the horizontal movement. Therefore, aluminum L beams are used to hold the entire structure as it provides a stiff base for the rails to attach

### DC Motor Simulation and Test

As the servo is already a fixed set, the remaining component that can be changed is the DC motor. Because the motor is a closed-loop system, optimization within the controller is done to have a critically damped system. Since a P-controller will be used, an approach to find a suitable Kp value is employed. This includes modelling the motor as a first order system. This allows us to model the system using Simulink.

<img src="\assets\pingpongCV-files\simulink.png" class="fit image">

Using the Simulink model, we have found that an ideal Kp value is around 180. Inputting on the actual system, the value of which the system becomes critically damp is 200. This value is reasonable as the motor transfer function doesn’t taken into account the additional inertia of the system when adding the pair of paddles.

Another parameter for the entire system is the total response time of the system. Ideally, the system should be in position to block the ball in approximately 100ms. This value is just an approximation of the time it takes for the ball hit by the user to the point it reaches the blocking plane.

## System Evaluation / Conclusion

The last test involves examining the entire system’s performance with regards to its objective to intercept the ping pong ball. Three evaluation criteria is employed to see if our system meets the desired objective. These are:
1.	Time response of the system
2.	Repeatability of continuous feed of ball
3.	Percentage of blocked balls

The first criteria refers to how fast the system reacts when the ball is approaching the blocking plane. This can be tested by simply entering an X-Y coordinate into the C# program and measuring the time it takes for the paddle to cover the area. The second criteria refers to if the system can consistently react if the ball is continuously thrown at the blocking plane. This is done by continuously throwing the ball. The last criteria is the number of successful blocks the system can do.

The test with the time response of the system showed that that maximum response time of the paddle system is 1.1 seconds. This is found when the paddle had to move the maximum amount of distance, particularly right along its centerline. Moving to its centerline had an approximately 17cm worth of horizontal movement while moving at its far edges resulted in a 12cm distance from the default position.

Testing using the second criteria, its shown that because of the slow movement of the DC motor in the horizontal movement, the cycle time of which the system moves from default state to blocking state and back to default is not ideal. It was timed that the entire sequence takes 1.9 seconds. Therefore at a normal usage, the system will not be able to react fast enough for a person to continuously deflect back the ball.

The last criteria is the number of blocked shots. This test simply involves us lobbing the ping pong ball to the system and see if it can react fast enough. After a few tries, we’ve found the following observations:
1.	Ping pong can only be slowly lobbed rather than being thrown for the system to be able to react at all
2.	Extreme locations such as the center or at the far ends are likely to not be able to be blocked in time
3.	Due to no physical markers, it’s easy to throw the balls out of bounds of the coverage area

The first two observation can be thought of a continuation of the observation found from the second criteria. Because the DC motor moves slowly, and coupled with the delay of the system due to the filter and computation time, farther areas are hard to consistently blocked.

## Reflections

From the project, it can be concluded that while faster systems may require expensive parts, a good trajectory prediction method can help with overall response times. However, if the project were to be done in the future, a higher frame rate would be used instead of 60Hz. As can be seen in the trajectory prediction functional requirement, due to the fast moving nature of the ball, it happens very often that there are not enough sample points for the filtered data to reach the real value. Hence, during demos and testing, the ball has to be launched at a lower speed for the paddles to arrive on time.

In addition, larger pulley for the timing belt would have helped the linear rail reach higher peak speeds. The current design, while able to return balls when minimal X movement is needed, struggles when the balls are in opposite corners. Since the overall assembly of the paddles are 3D printed, there would have been enough torque from the motor even with the higher motor speed.

Overall, the results from this project is excellent. However, upon transporting the whole assembly to the demo location at UBC, many parameters needed to be tuned last minute, since the setup is not completely identical to the one tested at home. This resulted in many technical difficulties. In the future, if a vision based project is to be redone, a method to replicate the camera location and lighting would be helpful.

Many new technical skills were developed in the pursuit of the perfect ping pong robot. Not only in terms of vision software, and fine motor controls in the X-Y plane, but also mechanical design as well. For this, we would like to thanks Iftikhar Azam and Dr. Hongshen Ma for providing us with guidance and the base knowledge needed to pursue this daunting project.

