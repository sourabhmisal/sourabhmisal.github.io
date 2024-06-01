---
title: " Ceres : Autonomous Navigation Kit for Tractors"
description: "Flux Auto"
hideSummary: true
dateString: "Apr 2021 - Aug 2024 | 3 years 4 months"
draft: false
tags: ["STM32", "C (Programming Language)", "FreeRTOS", "Embedded Systems", "DC Motor Control System", "Stepper Motor Control System", "Servo Motor Control System", "Actuator Control System", "Communication Protocols", "CANOpen", "I2C", "GPIO", "USB", "UART", "ADC", "CI/CD", "Reverse Engineering", "Case Study", "PID Control algorithm", "JTAG Debugging"]
showToc: false
weight: 303
--- 

### Description
Designed and implemented embedded control systems of autonomous navigation kit for tractors as part of Flux Auto's comprehensive agricultural automation solution, following the guidelines of ISO 18497 and 25119-1 which is Agricultural machinery and tractors — Safety of partially automated, semi-autonomous and autonomous machinery

#### Key Technologies and Skills
* ***Communication Protocols :***

    * **CANopen Protocol :** Integrated CANopen for robust communication among submodules of the modularized embedded system architecture. Developed custom CANopen nodes for various components, ensuring seamless interaction with the vehicle’s existing CAN bus and its subsystems and facilitating modular and scalable firmware architecture
    * **Embedded Communication Protocols :** Developed low-level drivers for I2C, CAN, UART, and USB using HAL APIs and libraries provided by silicon vendors.

* ***Embedded Systems and RTOS :***

    * **FreeRTOS :** Deployed FreeRTOS for real-time task scheduling and execution on single-core ARM Cortex-M4 and M7 microcontrollers. Configured tasks for feedback data acquisition, decision-making algorithms and actuator controls, ensuring deterministic behavior and high system reliability.
    * **Event-Driven State Machine :** Engineered an event-driven state machine to manage the autonomous navigation system's states, enabling dynamic responses to environmental changes and system events.
    
* ***Control Systems :***
    * **PID Control :** 
        * Designed and implemented PID control algorithms for DC motor, Stepper Motor, Servo Motor and Actuator Control Systems optimizing efficiency and performance.
        * Developed software modules for real-time control and monitoring of various motor parameters, ensuring precise speed and torque control.
        * Collaborated with cross-functional teams to integrate PID Control algorithms into embedded systems, enhancing motor performance and reliability.

* ***Device Drivers :***

    * **I2C Protocol :** Developed device drivers for PCA9685 Timer IC and DS3502 digital potentiometers ensuring accurate and reliable communication and control.
    * **UART Protocol :** Implemented drivers for real-time debugging and status update, optimizing data transmission and reception.

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
    * Spearheaded the research and development process to create a retrofit autonomous navigation kit tailored for integration onto clients’ tractors in agricultural settings.
    * Provided technical expertise and support during the integration phase of retrofit autonomous navigation kit, ensuring seamless installation and functionality on clients’ tractors.

* ***System Architecture and Integration***
    * Engineered a fault-tolerant embedded systems architecture to optimize reliability, ensuring continuous autonomous operation of tractors. 
    * Facilitated seamless communication between tractor control systems and the software stack of the Autonomous Navigation kit.
    * Led and contributed to the firmware development of a modular, scalable and upgradable embedded systems architecture using FreeRTOS, C, C++, ROS and state machines, enabling easy integration of additional features and upgrades to meet evolving agricultural automation needs.
    * Demonstrated proficiency in developing and optimizing low-level drivers and peripheral interfaces for firmware of embedded systems. Ensured seamless integration with hardware components and safety sensors, resulting in maximized system performance and reliability.
    * Reviewed and validated schematics for microcontrollers and peripheral components, ensuring hardware functionality aligned with project objectives. Collaborated with hardware teams to troubleshoot and optimize electrical designs for embedded systems.
    * Utilized advanced debugging and testing tools, including JTAG, multimeters, and oscilloscopes, to ensure the functionality and reliability of embedded systems. Conducted thorough testing procedures to diagnose and resolve hardware and software issues, ensuring optimal performance of autonomous navigation kits for tractors.

* ***System Optimization and Performance Tuning***
    * Identified critical bottlenecks and optimized system performance through code refinement and strategic priority tuning, ensuring efficient operation of autonomous navigation systems for tractors.
    * Collaborated with cross-functional teams to ensure the seamless integration of the software stack of the autonomous navigation kit with existing agricultural infrastructure and compatibility with various tractor models.


#### Achievements:
* Secured a contract with agricultural facilities in India for the pilot run of the Autonomous Navigation Kit on five units of their tractors.
* Successfully delivered an autonomous navigation solution that significantly improved agricultural operational efficiency and safety standards.
* Received positive feedback from stakeholders for the seamless integration and robust performance of the autonomous navigation kit within existing agricultural infrastructure.
* Contributed to Flux Auto’s reputation as a reliable provider of innovative agricultural automation solutions.


#### Key Learnings:
* Gained insights into the complexities of developing autonomous systems for agricultural applications.
* Enhanced skills in embedded systems design, sensor integration, and cross-functional collaboration.
* Developed a deeper understanding of safety-critical systems and their importance in agricultural automation environments.


#### Technologies Used
* Communication Protocols (e.g., CANOpen, I2C)
* Safety Systems (Emergency Stop, Collision Detection)
* Event-Driven based Embedded Systems firmware Architecture
* Safety Systems (Emergency Stop, Collision Detection)
* Sensors : 2D Safety LiDARs