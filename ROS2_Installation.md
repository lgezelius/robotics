# ROS 2 Installation

ROS 2 Jazzy Jelasco's primary target is Ubuntu Linux - Noble Numbat (24.04).

## Install Ubuntu 24.04 VM

For a developer with an M-series chip MacBook, a good option is VMware Fusion Pro (free for personal use) and the [Ubuntu 24.04 64-bit ARM (ARMv8/AArch64) desktop image](https://cdimage.ubuntu.com/daily-live/20240421/).

Create a New Virtual Machine using the ISO.

    Virtual Machine Summary
    Guest Operating System Ubuntu 64-bit Arm 24.04
    New Hard Disk Capacity 20 GB
    Memory 4 GB
    Networking Share with my Mac (NAT)
    Device Summary 2 CPU cores, CD/DVD, USB Controller, Sound Card

If this VM is used for personal use, don't select "Use Active Directory". It is overkill for personal use.

When prompted to set a hostname, don't include any periods in it.

Note: git is apparently pre-installed.

Shutdown the VM and to the following:

* Go to Settings.../Startup Disk and select Hard Disk (NVMe).
* Go to Settings.../CD/DVD Drive and disconnect the CD/DVD Drive.
* Go to Settings.../Displays, enable "Accelerate 3D Graphics" and set "Shared Graphics memory" to 1024 MB.
* Change Network Adapter to Bridged (Autodetect). This puts the VM directly on your network, accessible by all other devices on your network.

Set the Blank Screen Delay to Never.

    gsettings set org.gnome.desktop.session idle-delay 0

Enable clipboard sharing between host and the VM.

    sudo apt update
    sudo apt install open-vm-tools open-vm-tools-desktop -y
    sudo reboot

Install some common tools:

    sudo apt install net-tools curl -y
    
Install a service and utilities to support Apple's Zeroconf architecture, also known as "Rendezvous" or "Bonjour" :

    sudo apt install avahi-daemon avahi-utils -y

Start and enable the Avahi service:

    sudo systemctl start avahi-daemon
    sudo systemctl enable avahi-daemon

Install an SSH server:

    sudo apt install openssh-server -y

Now you should be able to SSH from the host, for example if the user name is larry on both host and VM, and the hostname is ubuntu-2404:

    ssh ubuntu-2404.local

## Install MESA 3D Graphics Library Utilities

Install utilities for Mesa 3D Graphics Library.

    sudo apt install mesa-utils -y

To check for Graphic Library errors run:

    glxinfo | grep -i error

## Install ROS 2

See <https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html> for full details.

Check for UTF-8:

    locale

Enable required repos:

    sudo apt install software-properties-common -y
    sudo add-apt-repository universe -y
    sudo systemctl daemon-reload
    sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
    echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

Update repo caches and upgrade :

    sudo apt update && sudo apt upgrade -y
    sudo systemctl daemon-reload

Finally install the Desktop:

    sudo apt install ros-jazzy-desktop -y

## Test Installation

In one terminal:

    source /opt/ros/jazzy/setup.bash
    ros2 run demo_nodes_cpp talker

In another terminal:

    source /opt/ros/jazzy/setup.bash
    ros2 run demo_nodes_py listener

## Configure Environment

Add sourcing to shell startup script.

    echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc

Set the ROS domain ID to 0 because the numbers between 0 and 101, inclusive, are safe.

    echo "export ROS_DOMAIN_ID=0" >> ~/.bashrc

Set the Qt Platform Abstraction (QPA) to X11 instead of Wayland.
Wayland causes errors in some ROS 2 GUI utilities such as RQt.
Wayland is used by Ubuntu 22.04+.
Qt (pronounced “cute”) is a cross-platform software development framework used for building graphical user interfaces (GUIs) and other applications.

    echo "export QT_QPA_PLATFORM=xcb" >> ~/.bashrc

Test in a new shell by checking for ROS environment variables.

    printenv | grep -i ROS

## Install GUI Tools

Install RQt. RQt is a graphical user interface framework that implements various tools and interfaces in the form of plugins.

    sudo apt install '~nros-jazzy-rqt*' -y

## Development

Install dev tools.

    sudo apt install python3-colcon-common-extensions -y

## Set up colcon_cd

Modify ~/.bashrc.

    echo "source /usr/share/colcon_cd/function/colcon_cd.sh" >> ~/.bashrc
    echo "export _colcon_cd_root=/opt/ros/jazzy/" >> ~/.bashrc

## Set up colcon tab completion

    echo "source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash" >> ~/.bashrc

## Install Default Colcon Mixins

    colcon mixin add default https://raw.githubusercontent.com/colcon/colcon-mixin-repository/master/index.yaml
    colcon mixin update default

## BASH Shell Environment Customizations

The last six lines of ~/.bashrc should read as follows:

    source /opt/ros/jazzy/setup.bash
    export ROS_DOMAIN_ID=0
    export QT_QPA_PLATFORM=xcb
    source /usr/share/colcon_cd/function/colcon_cd.sh
    export _colcon_cd_root=/opt/ros/jazzy/
    source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash

## Visual Studio Code

You can now test connecting to your Ubuntu host from [VS Code](/Visual_Studio_Code.md).
