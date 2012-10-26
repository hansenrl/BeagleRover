BeagleRover
===========

This is an implemention of a semi-intelligent rover for a BeagleBone.
The intelligence of the system comes from an interface to a GPS sensor,
a digital compass, and a USB WiFi adapter for communication with a base
station.

This project includes software for interfacing with the GPS, compass, and
the motors of an RC car. Python scripts are also included to communicate
with the RC car over the network, giving it commands to turn and go forward
as well as query the GPS and compass sensors.

The code is structured for two types of interaction

1. Stand-alone control and navigation
 * main code located in movement.c
2. Remote operation via Python
 * communications layer in Python located in networkPython folder, and shared libraries compiled into sharedLibs folder

    make
    make clean

### Compass

The main compass code is located in *compass.c*. This file includes routines for initialization, calibrating the compass, and reading the heading. Two sample code files are included, *calibrate.c* runs the calibration routine of the compass for 10 seconds, during which time the user should rotate the compass axially twice for calibration. *main.c* will initiaze the compass and print the compass reading at a frequency of 5 Hz. 

These can be complied with gcc, or using make from the project directory
    make CompassExample

### GPS

The main GPS code is located in *gps.c*, and the dataGPS structure for passing around GPS data is located in *gps.h*. An example program that prints the current GPS location is shown in main.c, and can be compiled with gcc or make
    make GPSExample

### Waypoints

Although not fully functional as of 11/12/2012, prototype helper code for waypoint navigation is located in Waypoints.

### Network Python

*boneMovementServer.py* is Python code designed to be run on the Bone, and will setup a server to listen for movement commands from a client. It can be started with the command
    python boneMovementServer.py <IP-ADDRESS> <PORT>
where <IP-ADDRESS> is the IP Address of the BeagleBone and <PORT> is the TCP port to listen on. For example,
    python boneMovementServer.py 192.168.2.2 5005
will start the code listening for connections on port 5005.

*cpMovementClient.py* is Python code designed to run on the controlling base station - any computer that is connected over the network to the Bone and can run python. t can be started with the command
    python cpMovementClient.py <IP-ADDRESS> <PORT>
where <IP-ADDRESS> is the IP Address of the BeagleBone that you want to connect to and <PORT> is the TCP port that the BeagleBone is listening on. For example,
    python cpMovementClient.py 192.168.2.2 5005
will attempt to connect to a BeagleBone at 192.168.2.2 through port 5005.



More details about the project can be found on the project wiki:
http://elinux.org/ECE497_Project_Rover
