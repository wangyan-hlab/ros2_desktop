FROM osrf/ros:foxy-desktop

# Install turtlesim package
RUN apt update && \
    apt install ros-$ROS_DISTRO-turtlesim -y
    
# Install rqt tools    
RUN apt update && \
    apt install ~nros-$ROS_DISTRO-rqt* -y
    
# Install rviz2
RUN apt update && \
    sudo apt install ros-$ROS_DISTRO-rviz2 -y
    
# Install gazebo11
RUN curl -sSL http://get.gazebosim.org | sh

RUN echo "source /opt/ros/$ROS_DISTRO/setup.bash" >> ~/.bashrc
