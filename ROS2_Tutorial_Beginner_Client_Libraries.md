# ROS 2 Tutorial - Beginner: Client libraries

The following are notes for <https://docs.ros.org/en/jazzy/Tutorials/Beginner-Client-Libraries.html>:

## Using colcon to build packages

### Create a workspace & Add some sources

Run the following:

    mkdir -p ~/ros2_ws/src
    cd ~/ros2_ws
    git clone https://github.com/ros2/examples src/examples -b jazzy

Now use an IDE to view the code. If you are using VS Code on a separate computer or VM, use the Remote-SSH extension to connect. Then open ~/ros_ws/src. Trust the folder and enable all features. Go to Terminal/New Terminal in VS Code and it should appear in the bottom right of VS Code.
