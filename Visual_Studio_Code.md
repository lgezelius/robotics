# Visual Studio Code

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

## CMAKE Extension by twxs

Recommended in <https://www.youtube.com/watch?v=hf76VY0a5Fk> and in <https://automaticaddison.com/how-to-install-and-configure-visual-studio-code-for-ros-2/>.

## CMAKE Tools by Microsoft

...