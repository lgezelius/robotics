# Visual Studio Code

If you have installed and use VS Code somewhere on the same network on which you installed your base ROS computer or VM, then you should plan on using that VS Code installation for ROS development.

You should wait to do the following, until after you have created something in ~/ros2_ws/src, e.g. as you are going through the official tutorials.

## Remote - SSH by Microsoft

If you accessing a remove host, install Remote - SSH by Microsoft Extension.

Tutorials for the extension are available at <https://marketplace.visualstudio.com/items?itemName=ms-iot.vscode-ros>.

Press F1 (fn+F1) and select "Remote-SSH: Connect to Host..."

The first time this added a section to the beginning of ~/.ssh/config

    Host ubuntu-2404.local
      HostName ubuntu-2404.local
      User larry

    Host *
      IdentityAgent "~/Library/Group Containers/2BUA8C4S2C.com.1password/t/agent.sock"%

Install the following extensions. If you are connecting to a remote host using SSH, install the extension after connecting.

## ROS Extension by Microsoft

Adds autocompletion, syntax highlighting, and commands.

Commands are accessed using ⌘ + shift + p on a Mac.

Commands:

* ROS: Create Terminal - opens a terminal and sources install/setup.bash
* ROS: Run a ROS executable (rosrun)
* ROS: Update C++ Properties - fixed an issue where an #include of a .hpp file could not be in a .cpp file

## C/C++ by Microsoft

## C/C++ Extension Pack by Microsoft

## CMAKE Tools by Microsoft

...

## CMAKE Extension by twxs

This extension was recommended in <https://www.youtube.com/watch?v=hf76VY0a5Fk> and in <https://automaticaddison.com/how-to-install-and-configure-visual-studio-code-for-ros-2/>.

VS Code now says that twxs.cmake should be uninstalled because CMAKE Tools now provides language services and no longer depends on this extension.

## Flake8

Linting support for Python. Used by ROS2 tests.

Add the following to ~/ros2_ws/src/.vscode/settings.json:

    ,
    "flake8.args": [
      "--max-line-length=99",
      "--import-order-style=google",
      "--extend-ignore=B902,C816,D100,D101,D102,D103,D104,D105,D106,D107,D203,D212,D404,I202"
    ]

And also the same to ˜/ros2_ws/src/\<PACKAGE\>/.vscode/settings.json as required.
