---
title: " Drivn : Autonomous Navigation Kit for existing Battery Operated Pallet Trucks (BOPTs)"
description: "Flux Auto"
hideSummary: true
dateString: "Apr 2022 - Aug 2024 | 2 years 3 mos"
draft: false
tags: ["STM32", "C (Programming Language)", "C++", "FreeRTOS", "Embedded Systems",  "BLDC Motor Control System", "AC Induction Motor Control System", "Communication Protocols", "CANOpen", "I2C", "GPIO", "USB", "UART", "ADC", "CI/CD", "Reverse Engineering", "Case Study", "Version Control", "PID Control Algorithm"]
showToc: false
weight: 301
--- 

### Description
Developed an autonomous navigation kit for existing Battery-Operated Pallet Trucks (BOPTs) as part of Flux Auto's comprehensive warehouse automation solution, following the guidelines of IEC 61508 which is  Functional Safety of Electrical/Electronic/Programmable Electronic Safety-related Systems.

#### Key Technologies and Skills
* ***Communication Protocols :***

    * **CANopen Protocol :** Integrated CANopen for robust communication among submodules of the modularized embedded system architecture. Developed custom CANopen nodes for various components, ensuring seamless interaction with the vehicle’s existing CAN bus and its subsystems and facilitating modular and scalable firmware architecture
    * **Embedded Communication Protocols :** Developed low-level drivers for I2C, CAN, UART, and USB using HAL APIs and libraries provided by silicon vendors.

* ***Embedded Systems and RTOS :***

    * **FreeRTOS :** Deployed FreeRTOS for real-time task scheduling and execution on single-core ARM Cortex-M4 and M7 microcontrollers. Configured tasks for feedback data acquisition, decision-making algorithms and actuator controls, ensuring deterministic behavior and high system reliability.
    * **Event-Driven State Machine :** Engineered an event-driven state machine to manage the autonomous navigation system's states, enabling dynamic responses to environmental changes and system events.

* ***Control Systems :***
    * **PID Control :** 
        * Designed and implemented PID control algorithms for BLDC motor and AC induction motor control systems, optimizing efficiency and performance.
        * Developed software modules for real-time control and monitoring of BLDC motor parameters, ensuring precise speed and torque control.
        * Collaborated with cross-functional teams to integrate PID Control algorithms into embedded systems, enhancing motor performance and reliability.

* ***Device Drivers :***

    * **I2C Protocol :** Developed device drivers for MCP4441 and DS3502 digital potentiometers, and MCP23017 I/O expander, ensuring accurate and reliable communication and control.
    * **UART Protocol :** Implemented drivers for various sensors like ultrasonic sensors, optimizing data transmission and reception. Also used as debugging port for various subsystems.
    * **SPI Protocol :** Wrote a driver for the MCP41010 digital potentiometer, ensuring high-speed data transfer and precise control over the potentiometer.

* ***Robotics and Sensor Integration :***

    * **ROS (Robot Operating System) :** Utilized ROS to develop the robot's motion control stack. Implemented ROS nodes for sensor data processing, lateral motion control and longitudinal motion, facilitating modular and scalable software architecture.
    * **Safety Systems :** Developed safety systems including emergency stops and collision detection using SICK Safety Scanner LiDARs.

* ***Electrical Designs :***

    * Designed electronic control systems for the autonomous control of the vehicle using KiCAD.
    * Reviewed schematics for microcontrollers and connected peripheral components to assist in verifying hardware functionality with cross-functional teams.

* ***Board Bring-up and Integration :***

    * Participated in the board bring-up process for new hardware platforms. Worked closely with hardware engineers and controls experts to validate system functionality and resolve hardware/software integration issues.

#### Key Contributions
* ***Research and Development***
    * Led the research, development, and reverse engineering efforts for a retrofit Autonomous Navigation Kit for Battery-Operated Pallet Trucks (BOPTs) on client vehicles in India and the United States.
    * Spearheaded the research and development process to create a retrofit autonomous navigation kit tailored for integration onto clients' Battery-Operated Pallet Trucks in the warehouses.

* ***System Architecture and Integration***
    * Engineered a fault-tolerant embedded systems architecture to optimize reliability, ensuring continuous autonomous operation of BOPTs.
    * Facilitated seamless communication between BOPT's stock system and the software stack of the Autonomous Navigation kit.
    * Led and contributed to the development of a modular, scalable, and upgradable embedded systems architecture, enabling easy integration of additional features and upgrades.
    * Collaborated with cross-functional teams to ensure the seamless integration of the software stack of the autonomous navigation kit with existing warehouse infrastructure and compatibility with various BOPT models.
    * Provided technical expertise and support during the integration phase, ensuring seamless installation and functionality on clients' BOPTs.

* ***System Optimization and Performance Tuning***
    * Identified bottlenecks and optimized system performance through tuning of priorities, code complexity reduction, and system-level optimizations.

* ***Documentation and Communication***
    * Created and maintained comprehensive technical documentation including design specifications, user guides and release notes.
    * Communicated project status, technical challenges, and solutions in a clear and concise manner to stakeholders and cross-functional teams.


#### Achievements
* Secured a contract with Walmart Inc. for the pilot run of the Autonomous Navigation Kit on five units of their Battery-Operated Pallet Trucks in their Mexican warehouses.
* Successfully delivered an autonomous navigation solution that significantly improved warehouse operational efficiency and safety standards for BOPTs.
* Received positive feedback from stakeholders for the seamless integration and robust performance of the autonomous navigation kit within existing warehouse infrastructure.
* Contributed to Flux Auto's reputation as a pioneer of providing innovative warehouse automation solutions with the existing fleet and infrastructure.

#### Key Learnings
* Gained insights into the complexities of developing autonomous systems for industrial applications, particularly for Battery-Operated Pallet Trucks.
* Enhanced skills in embedded systems design, sensor integration, and cross-functional collaboration within the context of warehouse automation.
* Developed a deeper understanding of safety-critical systems and their importance in industrial automation environments, specifically for BOPTs.


#### Technologies Used
* Communication Protocols (e.g., CANOpen, I2C)
* Safety Systems (Emergency Stop, Collision Detection)
* Event-Driven based Embedded Systems firmware Architecture
* Sensors: 2D Safety LiDARs, Optical Encoders (for tracking wheel movement)









