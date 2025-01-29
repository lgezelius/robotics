# ROS 2 Tutorial: Using turtlesim, ros2, and rqt

Create the first node.

    ros2 run turtlesim turtlesim_node

List nodes.

    $ ros2 node list
    /turtlesim
    
It would be possible to create multiple turtlesim nodes, using the --ros-args flag when running turtlesim.

    $ ros2 topic list
    /parameter_events
    /rosout
    /turtle1/cmd_vel
    /turtle1/color_sensor
    /turtle1/pose

The following tells us that the /turtle1/color_sensor topic has 1 publisher (turtlesim) but no subscribers.

    $ ros2 topic info /turtle1/color_sensor --verbose
    Type: turtlesim/msg/Color

    Publisher count: 1

    Node name: turtlesim
    Node namespace: /
    Topic type: turtlesim/msg/Color
    Topic type hash: RIHS01_74492579ec0d734707aede0e742ab76c55ac50d3ff917381e5163624cb657fe5
    Endpoint type: PUBLISHER
    GID: 01.0f.95.56.be.21.83.00.00.00.00.00.00.00.1f.03
    QoS profile:
      Reliability: RELIABLE
      History (Depth): UNKNOWN
      Durability: VOLATILE
      Lifespan: Infinite
      Deadline: Infinite
      Liveliness: AUTOMATIC
      Liveliness lease duration: Infinite

    Subscription count: 0

List services.

    $ ros2 service list
    /clear
    /kill
    /reset
    /spawn
    /turtle1/set_pen
    /turtle1/teleport_absolute
    /turtle1/teleport_relative
    /turtlesim/describe_parameters
    /turtlesim/get_parameter_types
    /turtlesim/get_parameters
    /turtlesim/get_type_description
    /turtlesim/list_parameters
    /turtlesim/set_parameters
    /turtlesim/set_parameters_atomically

The first four services are global. There is only one namespace (/).

List actions.

    $ ros2 action list
    /turtle1/rotate_absolute

It would be possible to create multiple turtlesim nodes, using the --ros-args flag when running turtlesim.

Create the second node by running the following from another terminal.

    ros2 run turtlesim turtle_teleop_key

Apparently the /teleop_turtle node publishes to the /turtle1/cmd_vel topic by default.

    $ ros2 topic info /turtle1/cmd_vel -v
    Type: geometry_msgs/msg/Twist

    Publisher count: 1

    Node name: teleop_turtle
    Node namespace: /
    Topic type: geometry_msgs/msg/Twist
    Topic type hash: RIHS01_9c45bf16fe0983d80e3cfe750d6835843d265a9a6c46bd2e609fcddde6fb8d2a
    Endpoint type: PUBLISHER
    GID: 01.0f.95.56.4c.22.c6.d9.00.00.00.00.00.00.14.03
    QoS profile:
      Reliability: RELIABLE
      History (Depth): UNKNOWN
      Durability: VOLATILE
      Lifespan: Infinite
      Deadline: Infinite
      Liveliness: AUTOMATIC
      Liveliness lease duration: Infinite

    Subscription count: 1

    Node name: turtlesim
    Node namespace: /
    Topic type: geometry_msgs/msg/Twist
    Topic type hash: RIHS01_9c45bf16fe0983d80e3cfe750d6835843d265a9a6c46bd2e609fcddde6fb8d2a
    Endpoint type: SUBSCRIPTION
    GID: 01.0f.95.56.be.21.83.00.00.00.00.00.00.00.1d.04
    QoS profile:
      Reliability: RELIABLE
      History (Depth): UNKNOWN
      Durability: VOLATILE
      Lifespan: Infinite
      Deadline: Infinite
      Liveliness: AUTOMATIC
      Liveliness lease duration: Infinite

List the nodes again.

    $ ros2 node list
    /teleop_turtle
    /turtlesim

The topic list is unchanged.

List services.

    $ ros2 service list
    /clear
    /kill
    /reset
    /spawn
    /teleop_turtle/describe_parameters
    /teleop_turtle/get_parameter_types
    /teleop_turtle/get_parameters
    /teleop_turtle/get_type_description
    /teleop_turtle/list_parameters
    /teleop_turtle/set_parameters
    /teleop_turtle/set_parameters_atomically
    /turtle1/set_pen
    /turtle1/teleport_absolute
    /turtle1/teleport_relative
    /turtlesim/describe_parameters
    /turtlesim/get_parameter_types
    /turtlesim/get_parameters
    /turtlesim/get_type_description
    /turtlesim/list_parameters
    /turtlesim/set_parameters
    /turtlesim/set_parameters_atomically

Run Rqt in another terminal.

    rqt

This creates a third node.

    $ ros2 node list
    /rqt_gui_py_node_8952
    /teleop_turtle
    /turtlesim

The following services were added:

    /rqt_gui_py_node_8952/describe_parameters
    /rqt_gui_py_node_8952/get_parameter_types
    /rqt_gui_py_node_8952/get_parameters
    /rqt_gui_py_node_8952/get_type_description
    /rqt_gui_py_node_8952/list_parameters
    /rqt_gui_py_node_8952/set_parameters
    /rqt_gui_py_node_8952/set_parameters_atomically

Call the /spawn service to create the turtle2 node instance from Rqt. Remember that /spawn is a global service.

The following services were added:

    /turtle2/set_pen
    /turtle2/teleport_absolute
    /turtle2/teleport_relative

The new turtle2/cmd_vel topic has no publishers.

    $ ros2 topic info /turtle2/cmd_vel -v
    Type: geometry_msgs/msg/Twist

    Publisher count: 0

    Subscription count: 1

    Node name: turtlesim
    Node namespace: /
    Topic type: geometry_msgs/msg/Twist
    Topic type hash: RIHS01_9c45bf16fe0983d80e3cfe750d6835843d265a9a6c46bd2e609fcddde6fb8d2a
    Endpoint type: SUBSCRIPTION
    GID: 01.0f.95.56.be.21.83.00.00.00.00.00.00.00.2e.04
    QoS profile:
      Reliability: RELIABLE
      History (Depth): UNKNOWN
      Durability: VOLATILE
      Lifespan: Infinite
      Deadline: Infinite
      Liveliness: AUTOMATIC
      Liveliness lease duration: Infinite

Change the color and width of turtle1's pen by calling /turtle1/set_pen.

Create another telop_turtle node by running the following in another terminal.
This time remap so that the turtle2/cmd_vel node is published to instead of turtle1/cmd_vel.

    ros2 run turtlesim turtle_teleop_key --ros-args --remap turtle1/cmd_vel:=turtle2/cmd_vel

Now the second /telop_turtle publishes to /turtle2/cmd.

    $ ros2 topic info /turtle2/cmd_vel -v
    Type: geometry_msgs/msg/Twist

    Publisher count: 1

    Node name: teleop_turtle
    Node namespace: /
    Topic type: geometry_msgs/msg/Twist
    Topic type hash: RIHS01_9c45bf16fe0983d80e3cfe750d6835843d265a9a6c46bd2e609fcddde6fb8d2a
    Endpoint type: PUBLISHER
    GID: 01.0f.95.56.c2.23.35.6e.00.00.00.00.00.00.14.03
    QoS profile:
      Reliability: RELIABLE
      History (Depth): UNKNOWN
      Durability: VOLATILE
      Lifespan: Infinite
      Deadline: Infinite
      Liveliness: AUTOMATIC
      Liveliness lease duration: Infinite

    Subscription count: 1

    Node name: turtlesim
    Node namespace: /
    Topic type: geometry_msgs/msg/Twist
    Topic type hash: RIHS01_9c45bf16fe0983d80e3cfe750d6835843d265a9a6c46bd2e609fcddde6fb8d2a
    Endpoint type: SUBSCRIPTION
    GID: 01.0f.95.56.be.21.83.00.00.00.00.00.00.00.2e.04
    QoS profile:
      Reliability: RELIABLE
      History (Depth): UNKNOWN
      Durability: VOLATILE
      Lifespan: Infinite
      Deadline: Infinite
      Liveliness: AUTOMATIC
      Liveliness lease duration: Infinite

This is a bit confusing because both teleop_turtle nodes have the same name:

    $ ros2 node list
    WARNING: Be aware that there are nodes in the graph that share an exact name, which can have unintended side effects.
    /rqt_gui_py_node_8952
    /teleop_turtle
    /teleop_turtle
    /turtlesim
