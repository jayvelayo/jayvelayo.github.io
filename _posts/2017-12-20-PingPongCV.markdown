---
layout: post
title: Ping Pong arm using CV
date: 2017-12-20
---

<img src="/images/fulls/PingpongCV.png" class="fit image"> The Computer Vision controlled Ping Pong arm serves as a senior mechatronic project. The system has the ability to track a Ping Pong ball and return it using its motor-controlled paddle. It simulates playing Ping Pong with a human opponent.

# Overview

The Computer Vision controlled Ping Pong arm serves as a senior mechatronic project. The system has the ability to track a Ping Pong ball and return it using its motor-controlled paddle. It simulates playing Ping Pong with a human opponent.

<iframe width="560" height="315" src="https://www.youtube.com/embed/_ZPYBEtIChI" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

# Project Description
The project was divided into two main components, the tracking system and the ball return system. The tracking system is primarily done in a C# program to provide user interface and sends commands for the ball return system. To track the ball, it uses two PS4 Eye camera to determine the position coordinates of the ball. Based on individual frames, the program tracks the ball and uses a Kalman filter to predict the trajectory of the ball. It calculates the coordinates of the ball when it reaches the ball return plane and sends the corresponding commands to the hardware.
The ball return system uses a two-ended paddle which uses a 2D coordinate system. The system’s hardware includes two servo motors and two controllers. An MSP430F2274 is used to control a servomotor which is implemented using a DC motor with a rotary encoder. This provides more than 360 degrees precise rotation to move the paddle horizontally. An Arduino is used to control another servo which provides rotational control of the paddle. The controllers receives instructions from the C# program using UART. Together, they are able to control the XY Coordinates of the paddle.
