# ROS 2 Tutorial - Beginner: Client libraries

The following are notes for <https://docs.ros.org/en/jazzy/Tutorials/Beginner-Client-Libraries.html>:

## Creating a workspace

If you have created a ros2_workspaces symlink to /mnt/hgfs/ros2_workspaces, then do the following on the VM:

    mkdir -p ~/ros2_workspaces/ros2_ws/src
    cd ~/ros2_workspaces/ros2_ws

On the host machine cd to the src directory and clone the examples repo.

    git clone https://github.com/ros2/examples src/examples -b jazzy

