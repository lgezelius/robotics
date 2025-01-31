# ROS 2 Tutorial - Beginner: Client libraries

The following are notes for <https://docs.ros.org/en/jazzy/Tutorials/Beginner-Client-Libraries.html>:

## Using colcon to build packages

### Create a workspace & Add some sources

Run the following:

    mkdir -p ~/ros2_ws/src
    cd ~/ros2_ws
    git clone https://github.com/ros2/examples src/examples -b jazzy

Now use an IDE to view the code. If you are using VS Code on a separate computer or VM, use the Remote-SSH extension to connect. Then open ~/ros_ws/src. Trust the folder and enable all features. Go to Terminal/New Terminal in VS Code and it should appear in the bottom right of VS Code.

### Build the workspace

Run colcon.

    cd ~/ros2_ws
    colcon build --symlink-install

This returned a WARNING that "Some selected packages are already built in one or more underlay workspaces." Apparently that is OK.

### Run tests

Run colcon test.

    colcon test

Finshed in 50 seconds, with the following warning summary:

    test/test_flake8.py::test_flake8
      Warning: This process (pid=20332) is multi-threaded, use of fork() may lead to deadlocks in the child.

## Creating a workspace

### Create a new directory

The tutorial asks you to create the same ~/ros2_ws/src directory as in the previous section, and then asks you to pull from a different GitHub repo. You end up with two directories under src (examples and ros_tutorials). The tutorial makes more sense if you remove ~/ros2_ws first:

    $ rm -r ~/ros2_ws
    rm: remove write-protected regular file '/home/larry/ros2_ws/src/examples/.git/objects/pack/pack-3316a67d22a752815959eeb652211065250579ac.rev'? y
    rm: remove write-protected regular file '/home/larry/ros2_ws/src/examples/.git/objects/pack/pack-3316a67d22a752815959eeb652211065250579ac.pack'? y
    rm: remove write-protected regular file '/home/larry/ros2_ws/src/examples/.git/objects/pack/pack-3316a67d22a752815959eeb652211065250579ac.idx'? y

### Tasks

#### 4 Resolve dependencies

The following occured when trying to resolve dependencies. This should be a one-time occurence.

    ~/ros2_ws$ rosdep install -i --from-path src --rosdistro jazzy -y

    ERROR: your rosdep installation has not been initialized yet.  Please run:

        sudo rosdep init
        rosdep update

    ~/ros2_ws$ sudo rosdep init
    Wrote /etc/ros/rosdep/sources.list.d/20-default.list
    Recommended: please run

      rosdep update

    ~/ros2_ws$ rosdep update
    reading in sources list data from /etc/ros/rosdep/sources.list.d
    Hit https://raw.githubusercontent.com/ros/rosdistro/master/rosdep/osx-homebrew.yaml
    Hit https://raw.githubusercontent.com/ros/rosdistro/master/rosdep/base.yaml
    Hit https://raw.githubusercontent.com/ros/rosdistro/master/rosdep/python.yaml
    Hit https://raw.githubusercontent.com/ros/rosdistro/master/rosdep/ruby.yaml
    Hit https://raw.githubusercontent.com/ros/rosdistro/master/releases/fuerte.yaml
    Query rosdistro index https://raw.githubusercontent.com/ros/rosdistro/master/index-v4.yaml
    Skip end-of-life distro "ardent"
    Skip end-of-life distro "bouncy"
    Skip end-of-life distro "crystal"
    Skip end-of-life distro "dashing"
    Skip end-of-life distro "eloquent"
    Skip end-of-life distro "foxy"
    Skip end-of-life distro "galactic"
    Skip end-of-life distro "groovy"
    Add distro "humble"
    Skip end-of-life distro "hydro"
    Skip end-of-life distro "indigo"
    Skip end-of-life distro "iron"
    Skip end-of-life distro "jade"
    Add distro "jazzy"
    Skip end-of-life distro "kinetic"
    Skip end-of-life distro "lunar"
    Skip end-of-life distro "melodic"
    Add distro "noetic"
    Add distro "rolling"
    updated cache in /home/USER/.ros/rosdep/sources.cache

    ~/ros2_ws$ rosdep install -i --from-path src --rosdistro jazzy -y
    #All required rosdeps installed successfully

#### 5 Build the workspace with colcon

    $ colcon build
    [0.243s] WARNING:colcon.colcon_core.package_selection:Some selected packages are already built in one or more underlay workspaces:
      'turtlesim' is in: /opt/ros/jazzy
    If a package in a merged underlay workspace is overridden and it installs headers, then all packages in the overlay must sort their include directories by workspace order. Failure to do so may result in build failures or undefined behavior at run time.
    If the overridden package is used by another package in any underlay, then the overriding package in the overlay must be API and ABI compatible or undefined behavior at run time may occur.

    If you understand the risks and want to override a package anyways, add the following to the command line:
      --allow-overriding turtlesim

    This may be promoted to an error in a future release of colcon-override-check.
    Starting >>> turtlesim
    Finished <<< turtlesim [27.5s]                       

    Summary: 1 package finished [27.7s]

#### 6 Source the overlay

You don't need to source the underlay, because that is done automatically in each bash terminal session by ~./bashrc, but you do need to source the overlay:

    cd ~/ros2_ws
    source install/local_setup.bash

You have to run the following from Ubuntu Desktop:

    ros2 run turtlesim turtlesim_node

#### 7 Modify the overlay

This is the first opportunity to use VS Code to make a change! Install extensions recommended by VS Code.

## Creating a package

Catkin and Ament are build systems for ROS 1 and ROS 2 respectively. (A catkin and an ament are both names for a type of flower cluster that is long and cylindrical.)

## Writing a simple publisher and subscriber (C++)

