# ROS 2 Installation

## Overview

ROS 2 Jazzy Jelasco's primary target is Ubuntu Linux - Noble Numbat (24.04).

### Install Ubuntu 20.04 VM

For a developer with an M-Chip MacBook, a good option is VMware Fusion Pro (free for personal use) and the [Ubuntu 24.04 64-bit ARM (ARMv8/AArch64) desktop image](https://cdimage.ubuntu.com/daily-live/20240421/).

Create a New Virtual Machine using the ISO.

    Virtual Machine Summary
    Guest Operating System Ubuntu 64-bit Arm 24.04
    New Hard Disk Capacity 20 GB
    Memory 4 GB
    Networking Share with my Mac (NAT)
    Device Summary 2 CPU cores, CD/DVD, USB Controller, Sound Card

Don't select "Use Active Directory". It is overkill for personal use.

When prompted to set a hostname, don't include any periods in it.

If necessary, shutdown the VM to set the startup disk to Hard Disk (NVMe) and disconnect the CD/DVD Drive.

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

### Install ROS 2

See <https://docs.ros.org/en/jazzy/Installation/Ubuntu-Install-Debs.html> for full details.

Check for UTF-8:

    locale

Enable required repos:

<pre style="white-space: pre; overflow-x: auto;">
sudo apt install software-properties-common -y
sudo add-apt-repository universe -y
sudo systemctl daemon-reload
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
</pre>

Skip the following (with the assumption that development can be done on Mac)

    sudo apt update && sudo apt install ros-dev-tools -y

Update repo caches and upgrade :

    sudo apt update && sudo apt upgrade -y
    sudo systemctl daemon-reload

Finally install the Desktop:

    sudo apt install ros-jazzy-desktop -y

### Test Installation

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

Test in a new shell by checking for ROS environment variables.

    printenv | grep -i ROS
