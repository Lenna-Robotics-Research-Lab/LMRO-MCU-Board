# LMR Bardia MCU Board Design

## Overview

The Bardia Board, designed as an open-source hardware by Lenna Robotics Lab, is the MCU board for the LMR v1.1. The Schematics and PCB of this board is free to use under open-source licensing. 

![Alt text](https://github.com/Lenna-Robotics-Research-Lab/LMR-MCU-Board/blob/main/Documetns/images/Lenna_Board_2.png "LMR v1.1 Bardia Board")
![Alt text](https://github.com/Lenna-Robotics-Research-Lab/LMR-MCU-Board/blob/main/Documents/images/Lenna_Board_3.png "LMR v1.1 Bardia Board")
</br>

Some highlights on the board are listed below:

1. STM32F407VGT6 ARM Microcontroller 
2. On-board L298 Motor Driver 
3. USB to Serial (CH340G) 
4. Simultaneous USB and Battery Power Support 
5. Dedicated ADC for Reading Battery Level
6. Dedicated Fan Slot  
7. Ports(1x I2C Bus, 1x UART, 1x SPI, 1x CAN, 20x GPIO)
8. Dedicated SRF-04 Ultrasonic Sensor Slots (4x)
9. Ethernet Connectivity (DP83848 Physical Layer) 
 
## Microcontroller 

<p align="justify">
The microcontroller unit (MCU) is a critical component in the design, as it serves as the central processing unit for the robot. Selecting the right MCU was crucial, and our primary considerations were the available peripherals and their compatibility with various subsystems of the robot, as well as the local availability of the MCU in our region.<p>
<p align="justify">
After careful evaluation, STM32F407VGT6 was chosen as the MCU for this project. This powerful microcontroller offers a wealth of features that make it an ideal choice, including multiple of each communication protocols like I2C, SPI, and UART, as well as Ethernet support. Moreover, its affordability and widespread availability further solidified its suitability for this project's requirements. <p>

## L298 Driver Motor

<p align="justify">
The on-board L298 H-bridge motor driver simplifies the motor control process. To get started, simply connect the motors correctly and begin using the board. When using two DC motors, the on-board driver is sufficient. However, for projects requiring more motors or higher precision, we recommend using a dedicated motor driver board to avoid potential noise interference with other devices.<p>

### Noise Prevention Measures

To mitigate noise generated by the motor driver, the following precautions have been implemented:
- ***Ground Connections***: The driver ground and circuit ground are connected at a single node using a ferrite bead.
- ***EMI/EMC Reduction***: Stitching is utilized on the driver part of the board to further reduce electromagnetic interference (EMI).

## USB to Serial Interface 

<p align="justify">
The LMR Bardia Board features a USB type-B port, enabling direct connection to your computer. This straightforward setup supports seamless integration with environments like MATLAB and OCTAVE for monitoring and data processing. The board leverages the CH340G IC for USB communication and can be powered through the USB's 5V supply. <p>

## ETHERNET Connectivity 

<p align="justify">
The LMR Bardia board supports Ethernet connectivity, although this feature remains unutilized in the robot's initial release.<p>


# MCU Code

This Section is dedicated to provide a clearer view of the location and the purpose of the used functions and libraries.

**NOTICE** : in the code files, functions that start with LRL are defined by Lenna Robotics Lab and their location will be explained in the documents 

## Board Layout 


For a clearer comprehension of the board's pinout, please refer to the accompanying diagram, which illustrates the layout and pin assignments.
![Alt text](https://github.com/Lenna-Robotics-Research-Lab/LMR-MCU-Board/blob/main/Documents/images/Board_layout.jpg "LMR v1.1 Pinout")

## Motor System Identification and Controller Design

To carry out this part of the project STM32CubeIDE and MATLAB are facilitated. for further details on this section visit documentation on simulation and identification or the simulation folder.  

### System Identification 

<p align="justify">
First step is to calculate motor transfer function, a process carried out in MATLAB SIMULINK. This step is essential for the subsequent design of a controller that will facilitate the robot's ability to reach desired speeds. The preliminary code for this process can be accessed in the simulation branch, where the MATLAB files are also included. To establish a connection between the Microcontroller Unit (MCU) and the computer, The robots USB to Serial interface is utilized. The identification process was made possible through the use of MATLAB's SLDRT (Simulink Desktop Real-Time) tool.<p>

### Controller Design

<p align="justify">
As it is evident the motors used on this robot while having the same part number (ZGA25) they would not necessarily behave the same given the same input. Hence design of a robust controller is of great importance in order to achieve the scope of this robot. For this robot a PID controller is tuned to make sure the speed of the motors match the given input speeds. Further details will be available in the documents of the project.
<p>


