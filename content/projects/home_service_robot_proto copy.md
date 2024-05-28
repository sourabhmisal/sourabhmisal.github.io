---
title: " Prototype of Home service robot in virtual world using TurtleBot"
description: "Hobby"
hideSummary: true
dateString: "Apr 2020 - Jun 2020 | 3 mos"
draft: false
tags: ["ROS", "C++", "Localization", "SLAM", "Dijkstra's algorithm", "AMCL", "GPIO", "USB", "UART", "ADC", "CI/CD", "Reverse Engineering", "Shell scripting"]
showToc: false
weight: 306
--- 

### Description

* This project was done with the aim of demonstrating the knowledge of Simultaneous Localization and Mapping (SLAM) and Navigation Goal mode of a robot.
* I had done the simulation setup on gazebo for interfacing robot with different ROS packages, some of which are official ROS packages and others are packages that are created.
* The navigation of robot to specified pick-up and drop-off zones within the Gazebo world using localization is done using AMCL and trajectory planning through ROS Navigation stack, which relies on Dijkstra's algorithm.
* The Navigation Goal Node is developed that facilitates the communication with the ROS Navigation stack, enabling the autonomous transmission of successive goals for the robot to achieve.
* A virtual model of Tutlebot3 was used as home service robot where the it navigates to pick up and deliver virtual objects (using markers).
* Shell scripts were written to execute home service simulation.











