# ROS 2 Network

The following configuration works well on a network that you control, such as a home network, or a travel network created using a travel router. The network requires Internet access. The nodes with ROS2 installed need to be able to send and receive to each other on the network.

## Base

This Ubuntu LTS computer or virtual machine contains the full installation of ROS2 and an SSH server. This computer needs to support GUI applications using X11 such as rqt and rviz. If the base is a laptop, it probably should not go to sleep when the display is off and it is on non-battery power.

## IDE

An IDE, such as Visual Studio Code, can be installed on the Base, or another computer or virtual machine. If the Visual Studio Code is not on the Base, the "Remote - SSH" extension can be used to access the Base. (See [Remote Development using SSH](https://code.visualstudio.com/docs/remote/ssh#_remember-hosts-and-advanced-settings) for more information.)

## Robots

A robot, can include a Raspberry PI, running Ubuntu LTS with an installation of ROS2 and SSH server.
