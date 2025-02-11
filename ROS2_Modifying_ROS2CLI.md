# ROS 2 - Modifying ROS2CLI

## Notes

To set local branch to match remote branch:

    git branch --set-upstream-to=origin/try-git-username-for-maintainer-name 

## Overlay installation

    cd ~/ros2_ws/src/ros2cli/

    $ git status
    On branch git-username-for-maintainer-name
    Your branch is up to date with 'origin/git-username-for-maintainer-name'.

    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
        modified:   ros2pkg/ros2pkg/verb/create.py

    Untracked files:
    (use "git add <file>..." to include in what will be committed)
        .vscode/

    no changes added to commit (use "git add" and/or "git commit -a")

    $ git remote -v
    origin git@github.com:lgezelius/ros2cli.git (fetch)
    origin git@github.com:lgezelius/ros2cli.git (push)
    upstream https://github.com/ros2/ros2cli.git (fetch)
    upstream https://github.com/ros2/ros2cli.git (push)

## Build?

Is this correct when only updating something in ros2cli?

    cd ~/ros2_ws
    colcon build --packages-select ros2cli --allow-overriding ros2cli
    source install/setup.bash

## Manual Tests

    cd ~/ros2_ws/src
    mv ~/.gitconfig ~/.gitconfig_save
    ros2 pkg create --build-type ament_python --license Apache-2.0 --maintainer-name "Daffy Duck" test_package_33
    mv ~/.gitconfig_save ~/.gitconfig

    ros2 pkg create --build-type ament_python --license Apache-2.0 test_package_34

    ros2 pkg create --build-type ament_python --license Apache-2.0 test_package_34 --maintainer-email "INVALID"

## Commit & Sign

    git commit -s

## TODO

<https://docs.ros.org/en/jazzy/Tutorials/Intermediate/Testing/CLI.html>
