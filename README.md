# ROS2 Docker Image

To build a docker image of ROS2_humble_ur on your Ubuntu 20.04 LTS OS.
 
1. Run the following command directly in this directory:
    ```
    ./BUILD-DOCKER-IMAGE.sh
    ```
2. 2000 years later, run ``` docker images ``` to ensure the build success.

    If it shows a IMAGE called *frrobot/ros2:humble_ur*, congratulations! Move on to the next step.

3. Run this command to start a container:

    ```
    ./RUN-DOCKER.sh
    ```
    Use ``` docker ps ``` to check the container's information, its name should be *$(YOUR_USER_NAME)-ros2_humble_ur-1*.

> **NOTE**:
> 
> 1. The container would be stopped if the PC is rebooted, but it would still exist. 
> Just run ```./RUN-DOCKER.sh``` again to start it.
> 2. **Build workspace** would fail due to a **no matching function for call** ERROR. It is because the ```publish_state()```  function argument list in ```Universal_Robots_ROS2_Driver/ur_controllers/src/scaled_joint_trajectory_controller.cpp``` is inconsistent with that in ```/opt/ros/humble/include/joint_trajectory_controller/joint_trajectory_controller.hpp```. Deleting the redundant argument ```time``` of the ```publish_state()```  function in ```Universal_Robots_ROS2_Driver/ur_controllers/src/scaled_joint_trajectory_controller.cpp``` would help, but the inconsistence remains a problem to solve.
