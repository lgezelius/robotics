# Getting Started with ROS 2 Notes

Video: [Getting Started with ROS 2](https://www.youtube.com/watch?v=8aoFndU7jos)

## ROS 2

ROS 2 is a framework for robots. It lets you divide your software into nodes, which are responsible for each part of the robot. 
One node can represent the whole robot. 
Nodes makes it easier to add additional sensors later.
Nodes communicate with each other by passing messages.

### Message Passing

There are 3 main ways to pass messages:

* Topics (publish/subscribe model). There are many message types. But a topic, must use only one message type. A topic can have multiple sender and receiver nodes.
* Services (request/response model). Request and wait for response.
* Actions (request/feedback/response model). Can receive 0 to many feedback messages before response.

### Packages

* One or more more nodes with build instructions. Supports multiple languages. Supports code reuse between developers.

### Tooling

* Recording: Record messages into a rosbag. You can replay the message on your computer.
* Logging
* Visualization
* Tf Library: transformation library. For example, you can automatically figure out location of a gripper in relation to an object viewed by the camera.

### Practical Examples

SLAM (Simultaneous Localization and Mapping) - Turtlebot robot knows its location and maps its environment. Simple for ROS 2 because it knows Turtlebot.

### How to Proceed

Go through ROS 2 tutorials. Use Turtlebot simulator.
