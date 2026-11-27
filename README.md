# SkataBase

## Project Overview

SkataBase is a hardware and software project that aims to combine skateboarding with engineering to develop a platform for capturing, visualising and analysing skateboard tricks.

The project centres around a bespoke, skateboard-mounted motion tracking device that captures inertial measurement data and transmits it wirelessly to an Android companion application.

The longer-term objective is to develop a platform capable of automatically identifying and classifying flatground skateboard tricks using machine learning, while providing meaningful session analytics and visualisations of individual tricks and overall skateboarding performance.

Think Strava for skateboarding, facilitated by a purpose-built piece of hardware.

## Project Origins

The idea for SkataBase first came to me while studying Robotics as an undergraduate. At the time, I was skateboarding regularly and developing an interest in machine learning and its potential applications.

Exploring this idea led me to several academic papers investigating inertial sensor-based skateboard trick classification. One particularly relevant paper was:

[IMU-based Trick Classification in Skateboarding](https://www5.cs.fau.de/Forschung/Publikationen/2015/Groh15-ITC.pdf)

With the increasing accessibility of low-cost microcontrollers, inertial measurement units (IMUs) and embedded development platforms, I realised that the concept was technically feasible.

I decided to turn the idea into a practical engineering project, bringing together embedded systems, sensor fusion, mobile application development, mechanical design and machine learning.

## System Overview

SkataBase is composed of several interconnected hardware and software components, working together to capture skateboard motion, process inertial sensor data and ultimately translate it into meaningful information about individual tricks and skateboarding sessions.

The system is built around an embedded motion-tracking device mounted to the underside of a skateboard, which communicates wirelessly with an Android companion application.

### System Architecture

The following diagram illustrates the overall system architecture, from inertial data acquisition through to the planned trick classification and session analytics capabilities.

### Embedded System & Firmware

The embedded system is responsible for capturing and processing skateboard motion data.

An ESP32-C6 microcontroller interfaces with an ICM-20948 nine-axis inertial measurement unit over SPI. The IMU provides accelerometer, gyroscope and magnetometer measurements, which are used to estimate the orientation and movement of the skateboard.

The firmware handles sensor configuration and calibration, real-time data acquisition, orientation estimation using a Madgwick sensor fusion filter and BLE communication.

Processed sensor measurements and orientation data are encoded into structured packets and transmitted wirelessly to the Android application.

### Android Application

The Android application acts as the primary user interface for interacting with the motion-tracking device.

It connects to the embedded system over Bluetooth Low Energy, receives and processes incoming sensor data, and provides a real-time 3D visualisation of the skateboard's orientation.

The application also supports session recording and manual trick annotation, providing a mechanism for collecting labelled motion data during skateboarding sessions.

Future development will build upon this foundation to introduce automated trick classification, session analytics and visualisations of skateboarding performance.

### Custom Hardware

A custom-designed PCB is being developed to consolidate the embedded system into a compact, purpose-built hardware platform.

The design integrates the ESP32-C6 microcontroller, IMU interface, battery connection and supporting electronics, with consideration for power management, physical dimensions and manufacturability.

### Mechanical Design & Enclosure

A bespoke enclosure is being designed using CAD software and intended for manufacture through 3D printing.

The enclosure will house and protect the electronics while providing a compact and secure mounting solution for attachment to the skateboard, with particular consideration for vibration, impact resistance and accessibility.

## Current Development Status

SkataBase is currently in the prototype and hardware development phase. The initial proof of concept has demonstrated successful motion tracking, wireless data transmission and preliminary skateboard trick event detection.

The following outlines the current implementation status and remaining development objectives.

### Embedded System & Firmware

- [x] ESP32-C6 embedded development platform established.
- [x] ICM-20948 IMU integration over SPI.
- [x] Accelerometer, gyroscope and magnetometer data acquisition.
- [x] Sensor calibration and bias compensation.
- [x] Madgwick sensor fusion for orientation estimation.
- [x] Real-time roll, pitch and yaw estimation.
- [x] BLE communication and structured sensor data transmission.
- [ ] Improved magnetometer calibration.
- [ ] Stationary detection and periodic sensor bias correction.
- [ ] Automatic BLE reconnection and connection management.
- [ ] Low-power operation and battery management.

### Android Application

- [x] Kotlin Android application established using Jetpack Compose.
- [x] BLE device discovery and connection.
- [x] Incoming sensor packet reception and decoding.
- [x] Real-time orientation data processing.
- [x] 3D skateboard orientation visualisation.
- [x] Session data collection and recording.
- [x] Manual trick annotation and data labelling.
- [ ] Improved session management and data export.
- [ ] Enhanced trick visualisation and playback.
- [ ] Automated trick classification integration.
- [ ] Session analytics and performance statistics.

### Hardware Development

- [x] Initial breadboard prototype assembled and operational.
- [x] SPI communication validated between ESP32 and IMU.
- [x] Initial skateboard-mounted prototype constructed.
- [x] Successful preliminary skateboard field testing.
- [x] Initial custom PCB schematic and layout developed in KiCad.
- [ ] PCB design finalisation and design rule verification.
- [ ] Custom PCB fabrication and assembly.
- [ ] Battery power management and charging integration.
- [ ] Physical enclosure design and 3D printing.
- [ ] Mechanical integration and skateboard mounting validation.

### Data Collection & Machine Learning

- [x] Initial motion data collection workflow established.
- [x] Manual trick annotation workflow implemented.
- [x] Preliminary motion-based trick event detection.
- [ ] Larger labelled skateboard motion dataset.
- [ ] Data preprocessing and feature extraction pipeline.
- [ ] Evaluation of suitable machine learning approaches.
- [ ] Initial trick classification model.
- [ ] Model evaluation across different tricks and skateboarding conditions.
- [ ] Integration of automated classification into the Android application.

### Project Infrastructure

- [x] Separate Android, firmware and hardware repositories established.
- [x] GitHub project hub established.
- [x] Individual repository documentation and READMEs created.
- [ ] Consolidated project documentation and development roadmap.
- [ ] Release and versioning strategy.


## Application Showcase

The SkataBase Android application provides the primary interface for interacting with the motion-tracking device, visualising skateboard movement and collecting motion data.

Developed using Kotlin and Jetpack Compose, the application communicates with the embedded system over Bluetooth Low Energy (BLE).

### Device Connectivity

![](Images/ScreenShots/Scanning.png)

Discovery and connection to the skateboard-mounted motion-tracking device.

### Live Motion Visualisation

![](Images/ScreenShots/Orientation.png)
![](Images/ScreenShots/Animation.png)

Real-time visualisation of skateboard orientation using incoming IMU data.

### Session Recording & Data Collection

![](Images/ScreenShots/Training.png)
![](Images/ScreenShots/Annotation.png)

Recording skateboarding sessions and collecting motion data for subsequent analysis and annotation.

### Future Analytics

<!-- IMAGE: Placeholder for future analytics interface -->

Planned functionality includes automated trick classification, trick attempt tracking and session performance analytics. For this, research will be undertaken into what classification algorithms will be used (CNNs) and how it will be trained and run within the application. The idea is that it will generate a prediction for the trick that was performed with an associated confidence score against said prediction.

## Hardware Journey

Over the past few months there have been developments in the hardware prototypes used to build and test the application, with more upgrades in the works.

![](Images/Hardware/Hardware0.jpg)

The first iteration of the system used an ESP32 DevKit board, with the 20948 IMU. It also used the TP4056 charging module and a small salvaged LiPo battery from a disposable vape. The board shown here was quite unrefined as you can see by the electrical tape.

![](Images/Hardware/Hardware1.png)

A small wooden platform was made out of salvaged pallet wood to loosely resemble a skateboard.

![](Images/Hardware/Hardware2.png)

The mini skateboard idea was extended and I got out the angle grinder and grinded down another piece of pallet wood to have a rough concave shape, I sourced some real skateboard griptape to cover the top to make it look the real deal. This activity was non essential but working with my hands was a nice break from the computer work and produced a nice test platform for demos and desk development.

![](Images/Hardware/Hardware3.png)

The next development step was to make a better prototype board. I chose to use the Seeed Studio Xiao ESP32-C6 as the MCU, I chose this for the significantly smaller footprint, which is fine for this project because only a small number of GPIOs are required. Additionally it has built in battery management, meaning a BMS board such as the TP4056 is no longer required, the LiPo solders directly to the underside of the ESP32 so the system is charged via the USB-C port of the device. A latch push button is soldered in series with battery supply.

![](Images/Hardware/Hardware4.png)

This image shows the second prototype PCB board, not the significantly smaller layout.

![](Images/Hardware/Hardware5.png)

This image shows the use of an old snus container to act as the housing for the prototype PCB. The wires in this image differ slightly from the previous. This is because the SPI protocol was chosen over I2C as it was observed to be more robust.

![](Images/Hardware/Hardware6.png)

Here the prototype sensor is shown in situ attached to the skateboard using velco tape. (Dont worry the lid was on whilst riding) Unfortunately the device would frequently fly off after performing flip tricks due to the centripetal force acting on it during fast rotations so not allot of data was collected after the first session.


![](Images/Hardware/Hardware7.png)

The current stage of development is looking at PCB design, Kicad is being used for the development. A prelimianry design has been produced but further refinement will be taken before manufacturing. This work goes in parallel with the 3S CAD design which is happening currently. More updates coming soon.

