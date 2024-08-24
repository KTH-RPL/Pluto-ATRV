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
Pluto is a bright red all terrain vehicle, produced by iRobot in the early 2000s. While the chassis and lower level electronics remain much the same, a lot has been replaced or added to this robot. This manual aims to make it easier for future users to figure out the capabilities of Pluto, and to make use of it in their project.

The instructions and explanations in the following sections contain several locations, with directions such as "rear", "front", "left" and "right". To make clear the use of this language, we illustrate the following:

1 picture of pluto from above

Furthermore, it is possible to open up Pluto's hull to work with the interior components if necessary. To open up Pluto's hull, first ensure that the sensor rig and any other lose components residing on Pluto will not fall or be damaged. Second, undo the three hinges on the left side of the robot hull. You can now pull open the top hull, as one would with a pirate chest. Note that you may have to pull towards the left side as well, as the top is not completely rigid when not secured. 

Having opened the chassis, there is a second lid. This results in Pluto having three different levels (see image):

2 pictures of opened pluto, different levels


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
The robot 

Intel nucs, NVIDIA jetson

2 pictures - Intel NUC, Jetson
3 documentations (each nuc version, and jetson)

## Mechanical & Electrical Hardware
Motors, battery, controllers

2 pictures - Motor & battery, controller & reciever
3 documentations - controller, motors, batteries

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
Discuss how to operate sensor rig to collect data

## Possible Errors
list possible problems in descending order of likeliness
- 