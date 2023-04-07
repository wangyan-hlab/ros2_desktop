# ROS2 Docker Image

To build a docker image of ROS2 on your Ubuntu 20.04 LTS OS.
 
1. Run the following command directly in this directory:
    ```
    ./BUILD-DOCKER-IMAGE.sh
    ```
2. 2000 years later, run ``` docker images ``` to ensure the build success.

    If it shows a IMAGE called *frrobot/ros2:latest*, congratulations! Move on to the next step.

3. Run this command to start a container:

    ```
    ./RUN-DOCKER.sh
    ```
    Use ``` docker ps ``` to check the container's information, its name should be *$(YOUR_USER_NAME)-ros2-1*.

> **NOTE**:
> The container would be stopped if the PC is rebooted, but it would still exist. 
> Just run ```./RUN-DOCKER.sh``` again to start it.
