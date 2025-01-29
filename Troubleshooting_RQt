# Troubleshooting RQt

While following <https://docs.ros.org/en/jazzy/Tutorials/Beginner-CLI-Tools/Introducing-Turtlesim/Introducing-Turtlesim.html>, the following occured:

    $ rqt
    QSocketNotifier: Can only be used with threads started with QThread

ChatGPT says this is "Usually Non-Critical: This error is often just a warning and does not typically affect the functionality of rqt unless there is a deeper threading issue in your ROS2 or Qt setup. If rqt works fine, you can safely ignore this message."

After spawning turtle2, refreshing the service list, and choosing a service from the drop down list, the following occurs in the terminal that invoked rqt

    Wayland does not support QWindow::requestActivate()

ChatGPT says that one option is to use X11 instead of Wayland, which is the default in Ubuntu.

Apparently this issue can also affect Rvis and Gazebo, though those were not tried at the time of troubleshooting the RQT issue. Tried the following fix per <https://wiki.t-firefly.com/en/Firefly-Linux-Guide/ros.html> which was in line with ChatGPT's fix suggestion.

  echo "export QT_QPA_PLATFORM=xcb" >> ~/.bashrc

Closed terminal that invoked RQT and then started RQT in a new terminal. All warnings and errors resolved.
