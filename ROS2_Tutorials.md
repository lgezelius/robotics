# ROS 2 Tutorials

* [Beginner: CLI Tools](ROS2_Tutorial_Beginner_CLI_tools.md)
* [Beginner: CLI Libraries](ROS2_Tutorial_Beginner_Client_Libraries.md)
* [Intermediate](ROS2_Tutorial_Intermediate.md)

## Writing an action server and client (Python)

### Tasks

#### 1 Writing an action server

Create and run fibonacci_action_server.py in ~ as instructed.

In a new terminal, send a goal from the ros2 workspace.

    $ cd ~/ros2_ws
    $ source install/local_setup.bash 
    $ ros2 action send_goal fibonacci custom_action_interfaces/action/Fibonacci "{order: 5}"
    Waiting for an action server to become available...
    Sending goal:
        order: 5

    Goal accepted with ID: a1a0722e90704d7c8df027032067e343

    Result:
        sequence: []

    Goal finished with status: ABORTED

#### 2 Writing an action client

Create and run fibonacci_action_client.py in ~ as instructed.

## Writing a Composable Node (C++)

HERE
