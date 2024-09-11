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

It is possible to open up Pluto's hull to work with the interior components if necessary. To open up Pluto's hull, first ensure that the sensor rig, screen and any other lose components residing on Pluto will not fall or be damaged. Second, undo the three hinges on the left side of the robot hull. You can now pull open the top hull (think similarly to a pirate treasure chest!). 

![screenshot](images/pluto_second_layer.jpg)

Having opened the chassis, there is a second lid that can also be opened to reveal the engines and batteries (and some additional electronics). This results in Pluto having three different levels (see image):

![screenshot](images/pluto_third_layer.jpg)


# Hardware

## Sensor Hardware
Pluto comes equipped with a wide variety of sensor modalities. The main sensors are located in a mast on the front of the vehicle (see image below). This includes 

- 1x Ouster Os-1 Lidar, with 360 degree coverage
- 1x Livox Mid-70 Lidar, with front facing coverage
- 2x Intel realsense D455 RGBD cameras, with overlapping front facing coverage
- 1x VectorNav 200 IMU, mounted in between the lidars

![screenshot](images/sensor_rig_manual.png)

However, there is also a GNSS mounted towards the rear of the vehicle (see image below). This sensor is mounted separately, as the OS-1 Lidar severely affects the reception capability of the GNSS antenna. The GNSS module is an Emlid Reach M2, with capability for RTK and PPK augmentations.

![screenshot](images/GNSS_manual.png)

Manuals/specifications for these sensors are included in the folder named "datasheets". However, two things to also note:

1. The GNSS does not have a pdf reference, please instead see https://docs.emlid.com/reach/reference/specifications/specs/
2. The D455 cameras have a light sensitivity issue. We have included a document with description from Intel on this problem, and solved it by using NE06B filters from https://www.thorlabs.com/newgrouppage9.cfm?objectgroup_id=5011

## Computational Hardware
The robot has several different computer architectures on board. To collect data, the sensor rig has a separate Intel NUC, with x86 architecture. Pluto also has an older Intel NUC on the second level of the chassis, as well as an ARM based Nvidia Jetson AGX Orin.

Note that at the time of writing, the Jetson is not currently utilized by Pluto. This is planned to change in the future.

## Mechanical & Electrical Hardware
We use a wireless controller of the type "Logitech F710 Wireless Gamepad" to control the robot movement. The wireless reciever for this controller is connected to the Intel NUC on the second level of the robot chassis. To interact with the sensor rig, any type of bluetooth keyboard can be used.

There are four electrical DC Gearmotors in the vehicle, produced by Bison Gear & Engineering Corp. These motors are separately connected to each of the four wheels of the robot through toothed belts. As with most electric vehicles, this gives greater control opportunities, and Pluto is able to produce pure rotation without translation because of this. The motors each have the following electro-mechanical properties

- 0.25 Horsepower
- 24 Volt (DC)
- 10.78 Amps 
- 168 RPM
- 9.8 N-m Torque
- 11:1 Gear ratio

The robot has recently had its batteries replaced (mid 2024). While it used to run on EnerSys 12HX135FR lead acid batteries, it currently runs with four Victron LiFePO4 batteries, which each are 12,8V 20Ah. These power the engines, the two computers and the GNSS on Pluto. The sensor rig uses a separate power source, a TB47 DJI intelligent flight battery. The documentation on the Victron battery is included as a pdf. Also note that the drone lab currently has four TB47 batteries, but also four TB48 batteries which can be used interchangeably for the sensor rig if the need arises in the future (but are currently used for the DJI M300 drone).

## CAD files for 3D printing parts
TODO: add CAD files, talk about what the parts are used for. Also print part for separating batteries

# Software
In general, software for sensors and actuation runs with Ubuntu 20.4, and ROS Noetic.

## Sensor Rig
The sensor rig has a few scripts to make collecting data easier. We include these scripts in the software section, in case these are needed. With a (wireless) keyboard connected to the sensor rig NUC, operation then becomes very simple (see operation section).

TODO: ADD SCRIPTS

## GNSS
The GNSS is separately interfaced with, using the Emlid Flow app (available for android and iOS) and wifi. This allows for the collection of data in a RINEX format, which is very useful for post-processing with any avaiable software on the market.

## Robot Platform
TODO: give link to miguels software, explain. Talk about how bootup is handled automatically, but mentuion that it is possible to ssh to pluto wifi with passwords inside.

# Operation

## Charging Batteries
Note: Charging batteries is a potential fire hazard. Make sure you are aware of the safety regulations at RPL, and where batteries are allowed to be charged before doing this.

The batteries used in Pluto can be accessed in the third level, beneath the two lids. Here, you can charge the batteries by connecting the Anderson power connectors one by one as shown in the figure below. We use a Victron blue smart 12V 15A charger, which can also be connected with over bluetooth (using VictronConnect app, the passwords for pairing are written on the side of the chargers) to control the charging cycle, or view charging details. Currently there are two such chargers at RPL, so charging can be done with two batteries at the same time to speed up the process. There is also a connector at the back of Pluto which connects to the power grid, and enables charging all four connected batteries at the same time, however we do not currently have a charger with compatible connection to this port. 

![screenshot](images/charging.jpg)

To charge the batteries used in the sensor rig, one needs to use a DJI hex charger. This allows connecting and charging up to 6 batteries at the same time. To charge the batteries, connect the hex charger to a wall socket with a computer power cord. Attach the batteries to be charged as seen in the figure below. Ensure that the lights on the batteries turn on, indicating charging.

![screenshot](images/charging_dji.jpg)

## Getting It Moving
The first step is to turn on the power. This is controlled by the breaker mounted on the outside of the lower rear hull of Pluto. After this, one needs to press the knob that controls the Pluto console - at this point the fans should begin spinning, and after a short delay the console will boot and light up.

Wait a little bit, and then you can begin to turn off the brakes. There are two separate brakes which we call "real" and "virtual". The real brakes are controlled by the Pluto console, while the virtual brake is controlled by the Intel NUC of Pluto and its ROS software.

We illustrate the components needed for the following steps in three images below. To turn off the real brakes, ensure that the activation key is in a horizontal position. Then navigate to the brake menu in the Pluto console, and press the console knob. To then turn off the virtual brakes, press the upper left trigger on the handheld controller. It is now possible to control and move Pluto, using the left stick of the handheld controller. If you quickly need to reapply the brakes, use the emergency buttons located on all four corners of Pluto if reachable. Otherwise, apply the virtual brake from the handheld controller.

![screenshot](images/starting_instructions1.png)

![screenshot](images/starting_instructions2.png)

![screenshot](images/starting_instructions3.png)

Note: There are no active brakes in the system. The brakes being applied relies on the inertia of the motors (which is quite tough to move, but the system can still be dragged/pushed at low speeds with the wheels turning slowly).

## Collecting Data

### Sensor Rig
Ensure that the sensor rig battery is charged and turned on. To turn on this battery, press the button once, and then hold the button. After this, turn on the NUC (power button is available from underneath). A screen is available to view the output of the sensors, and ensure that the collection is going well. As the NUC turns on, ensure that a keyboard is connected. With a keyboard connected to the NUC in the sensor rig, you can now use the follwing shorthand commands:

- Press CTRL + 1 to start the ROS nodes for sensors.  
- Press CTRL + 5 to start collecting sensor data in a rosbag.
- Press CTRL + 0 to stop collection, and turn off sensor nodes.

Assuming a screen is connected to the sensor rig, it would be expected to start looking like the following once CTRL + 1 is pressed (with a slight delay after pressing until everything turns on)

![screenshot](images/ros.png)

Note that once pressing CTRL + 5 to turn on collection, a separate terminal will pop up as well that controls the bag node. A word of advice is to collect some short data, and then inspect the data with the "rqt" command (needs a roscore running in a separate terminal). The bags are saved in a folder simply named "bags". You can inspect the bag and see that all the data is coming in as expected. A bag might look like the following.

![screenshot](images/rqt.png)

### GNSS
TODO: discussion on how to collect GPS data and postprocess it 


# FAQ

## I would like to use Pluto for a project, who can I talk to?
The robot is owned by professor Patric Jensfelt, and used for projects by doctoral student Waqas Ali (2024-), reach out if you are interested.

## The robot is making noise during operation, is this normal?
There are several sources of noise, which are not cause for alarm. The sounds that are emitted normally but which might be interpreted as problematic are the lidar and engine belts. While the sensor rig is on, the Livox lidar emits a "grinding", almost "sandy" noise. When the robot moves, it sometimes emits a sharp thumping sound. This is a sound coming from an engine belt.

It can be hard to recognize if these are the sounds that are being heard. Think critically on if you believe the sounds emanating are actually signs of damage, or just normal operation.

## Why is the robot not moving?
Here are the most likely reasons for why the robot is not moving. Check in the following order

- Ensure that BOTH the real brake and virtual brakes are turned off. See "Operation/Getting It Moving".
- Wait a little for the ROS software to turn on before you try to deactive the virtual brake.
- Ensure that you have not accidentally pressed "mode" on the handheld controller. 
- Is there enough charge in the main batteries that power the engine? Check the battery voltage in the console. A nominal voltage with fully charged batteries will display anything in the range of 25.4 to 26 Volt. If you are several Volt below that, there is reason to suspect this cause.
- Are the batteries (2xAA) in the handheld controller dead?
- The USB based reciever for the handheld controller has been accidentally disconnected from the NUC inside Pluto.
- Open up the chassis fully to check the engine level. There are several motor driver PCBs which are connected to the upper level by an ethernet cable. This cable can become loose - if the lights of the PCBs at the lowest level are red (blinking or solid color), then the cable is not fully connected and cannot transmit a signal. Try wiggling the cable which connects the upper and lower level at the connection point (not forcefully), or replace it.
