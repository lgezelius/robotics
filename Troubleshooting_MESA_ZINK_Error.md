# Troubleshooting MESA ZINK Error

In Ubuntu 64-bit Arm 24.04 VM:

    $ ros2 run turtlesim turtlesim_node
    QSocketNotifier: Can only be used with threads started with QThread
    [INFO] [1738045121.814641420] [turtlesim]: Starting turtlesim with node name /turtlesim
    [INFO] [1738045121.824381691] [turtlesim]: Spawning turtle [turtle1] at x=[5.544445], y=[5.544445], theta=[0.000000]
    MESA: error: ZINK: failed to choose pdev
    libEGL warning: egl: failed to create dri2 screen
    ^C[INFO] [1738045164.982978673] [rclcpp]: signal_handler(signum=2)

The TurtleSim window appeared with a turtle in the center.

Test to see if OpenGL is properly installed and configured:

    sudo apt install mesa-utils -y

    $ glxinfo | grep OpenGL
    MESA: error: ZINK: failed to choose pdev
    glx: failed to create drisw screen
    OpenGL vendor string: Mesa
    OpenGL renderer string: llvmpipe (LLVM 17.0.6, 128 bits)
    OpenGL core profile version string: 4.5 (Core Profile) Mesa 24.0.9-0ubuntu0.3
    OpenGL core profile shading language version string: 4.50
    OpenGL core profile context flags: (none)
    OpenGL core profile profile mask: core profile
    OpenGL core profile extensions:
    OpenGL version string: 4.5 (Compatibility Profile) Mesa 24.0.9-0ubuntu0.3
    OpenGL shading language version string: 4.50
    OpenGL context flags: (none)
    OpenGL profile mask: compatibility profile
    OpenGL extensions:
    OpenGL ES profile version string: OpenGL ES 3.2 Mesa 24.0.9-0ubuntu0.3
    OpenGL ES profile shading language version string: OpenGL ES GLSL ES 3.20
    OpenGL ES profile extensions:

Stopped VM. Enabled Accelerate 3D Graphics.

    $ ros2 run turtlesim turtlesim_node
    QSocketNotifier: Can only be used with threads started with QThread
    [INFO] [1738046459.745420261] [turtlesim]: Starting turtlesim with node name /turtlesim
    [INFO] [1738046459.754937178] [turtlesim]: Spawning turtle [turtle1] at x=[5.544445], y=[5.544445], theta=[0.000000]

Updated Installation doc to include meta-utils and 3D Graphics acceleration.
