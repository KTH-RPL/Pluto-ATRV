# Pluto-ATRV
A manual for the all terrain vehicle (ATRV) Pluto.

## Table of contents
- [Introduction](#Introduction)
- [Hardware](#Hardware)
    - [Computational Hardware](##Computational-Hardware)
    - [Sensor Hardware](##Sensor-Hardware)
    - [Mechanical & Electrical Hardware](##Mechanical-&-Electrical-Hardware)
- [Software](#Software)
    - [Sensor Rig](#Sensor-Rig)
    - [Robot Platform](#Robot-Platform)
- [Operation](#Operation)
    - [Getting It Moving](#Getting-It-Moving)
    - [Collecting Data](#Collecting-Data)
    - [Charging Batteries](#Charging-Batteries)
- [FAQ](#FAQ)
    - [Stuck!](##Stuck!)


# Introduction
Pluto is a bright red all terrain vehicle, produced by iRobot in the early 2000s (this is the Sr model, also called the ATRV-II). The company no longer offers support for this robot, which can make technical issues with the vehicle seem more daunting. While the chassis and lower level electronics remain similar to the old robot, a lot has been replaced or added to this robot. This manual aims to make it easier for future users to figure out the capabilities of Pluto, and to make use of it in their project.

The instructions and explanations in the following sections contain several locations, with directions such as "rear", "front", "left" and "right". To make clear the use of this language, we illustrate the following:

PHOTO

Furthermore, it is possible to open up Pluto's hull to work with the interior components if necessary. To open up Pluto's hull, first ensure that the sensor rig, screen and any other lose components residing on Pluto will not fall or be damaged. Second, undo the three hinges on the left side of the robot hull. You can now pull open the top hull, as one would with a pirate chest. Note that you may have to pull towards the left side as well, as the top is not completely rigid when not secured. 

![screenshot](images/pluto_second_layer.jpg.png)

Having opened the chassis, there is a second lid. This results in Pluto having three different levels (see image):

![screenshot](images/pluto_third_layer.jpg.png)


# Hardware

## Sensor Hardware
Pluto comes equipped with a wide variety of sensor modalities. The main sensors are located in a mast on the front of the vehicle. This includes 

- 1x Ouster Os-1 Lidar, with 360 degree coverage
- 1x Livox Mid-70 Lidar, with front facing coverage
- 2x Intel realsense D455 RGBD cameras, with overlapping front facing coverage
- 1x VectorNav 200 IMU, mounted in between the lidars

However, there is also a GNSS mounted towards the rear of the vehicle. This sensor is mounted separately, as the OS-1 Lidar severely affects the reception capability of the GNSS antenna. The GNSS module is an Emlid Reach M2, with capability for RTK and PPK augmentations.

Manuals/specifications for these sensors are included in the folder named "datasheets". However, two things to also note:

1. The GNSS does not have a pdf reference, please instead see https://docs.emlid.com/reach/reference/specifications/specs/
2. The D455 cameras have a light sensitivity issue. We have included a document with description from Intel on this problem, and solved it by using NE06B filters from https://www.thorlabs.com/newgrouppage9.cfm?objectgroup_id=5011

2 Pictures - sensor rig, GPS

## Computational Hardware
The robot has several different computer architectures on board. To collect data, the sensor rig has a separate Intel NUC, with x86 architecture. Pluto also has an older Intel NUC on the second level of the chassis, as well as an ARM based Nvidia Jetson AGX Orin. The documentation for these are included. 

Note that at the time of writing, the Jetson is not currently utilized by Pluto. This is planned to change in the future.

Intel nucs, NVIDIA jetson

2 pictures - Intel NUC, Jetson
3 documentations (each nuc version, and jetson)

## Mechanical & Electrical Hardware
We use a wireless controller of the type "Logitech F710 Wireless Gamepad" to control the robot movement. The wireless reciever for this controller is connected to the Intel NUC on the second level of the robot chassis. To interact with the sensor rig, any type of bluetooth keyboard can be used.

There are four electrical DC Gearmotors in the vehicle, produced by Bison Gear & Engineering Corp. These motors are separately connected to each of the four wheels of the robot through toothed belts. As with most electric vehicles, this gives greater control opportunities, and Pluto is able to spin on location because of this. The motors each have the following electro-mechanical properties

- 0.25 Horsepower
- 24 Volt (DC)
- 10.78 Amps 
- 168 RPM
- 9.8 N-m Torque
- 11:1 Gear ratio

The robot has recently had its batteries replaced (mid 2024). It currently runs with four Victron LiFePO4 batteries, which each are 12,8V 20Ah. These power the engines, the two computers and the GNSS on Pluto. The sensor rig uses a separate power source, a 


Motors, battery, controllers

2 pictures - Motor & battery, controller & reciever
3 documentations - controller, motors, batteries

# Software
In general, software for sensors and actuation runs with Ubuntu 20.4, and ROS Noetic.

## Sensor Rig
The sensor rig has a few scripts to make collecting data easier. We include these scripts in the software section, in case these are needed. With a keyboard connected to the sensor rig NUC, operation then becomes very simple (see operation section).

## GNSS
The GNSS is separately interfaced with, using the Emlid Flow app (available for android and iOS) and wifi. This allows for the collection of data in a RINEX format, which is very useful for post-processing with any avaiable software on the market.

## Robot Platform
give link to miguels software

# Operation

## Charging Batteries
Discuss how to charge batteries (both pluto and sensor rig)
also discuss safety of battery charging
1 picture of batteries being charged

## Getting It Moving
The first step is to turn on the power. This is controlled by the breaker mounted on the outside of the lower rear hull of Pluto. 

discuss how to turn on power
discuss how to turn off brakes (key, real brakes, virtual brakes)
discuss how to move the robot
mention the emergency brakes

4 pictures - power switch & key, old driving computer, controller, emergency brakes


## Collecting Data

### Sensor Rig
Ensure that the sensor rig battery is charged and turned on. To turn on this battery, press the button once, and then hold the button. After this, turn on the NUC (power button is available from underneath). A screen is available to view the output of the sensors, and ensure that the collection is going well. As the NUC turns on, ensure that a keyboard is connected. With a keyboard connected to the NUC in the sensor rig, you can now use the follwing shorthand commands:

- Press CTRL + 1 to start the ROS nodes for sensors.  
- Press CTRL + 5 to start collecting sensor data in a rosbag.
- Press CTRL + 0 to stop collection, and turn off sensor nodes.

1 picture of screen with nodes on, so on

A word of advice is to collect some short data, and then inspect the data with the "rqt" command (needs a roscore running in a separate terminal). The bags are saved in a folder simply named "bags". You can inspect the bag and see that all the data is coming in as expected.

1 picture of data collected in rqt

### GNSS



# FAQ

## I would like to use Pluto for a project, who do I speak to?


## Why is the robot not moving?
Here are the most likely reasons for why the robot is not moving, and what to do

- Ensure that BOTH the real brake and virtual brakes are turned off. See "Operation/Getting It Moving".
- Ensure that you have not accidentally pressed "mode" on the handheld controller. 
- 
