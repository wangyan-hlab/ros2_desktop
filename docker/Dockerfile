FROM althack/ros2:humble-full
## Prerequisites
# Install some tools
RUN apt update && \
    apt install vim git make python3-pip -y
RUN python3 -m pip install vcstool

# Install colcon
RUN apt update && \
    apt install python3-colcon-common-extensions -y

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
RUN curl -sSL http://get.gazebosim.org | sh && \
    sudo apt install ros-$ROS_DISTRO-gazebo-ros-pkgs -y

## Build the workspace
RUN /bin/bash -c "source /opt/ros/$ROS_DISTRO/setup.bash && \
    mkdir -p ~/ros_ws/src"
# Download source
RUN /bin/bash -c "cd ~/ros_ws/src && \
    git clone -b humble_ur https://github.com/wangyan-hlab/ros2_desktop.git glozzom"

RUN git clone https://github.com/ros/rosdistro.git /etc/ros/ros_github/rosdistro/
COPY ros_bypass/rep3.py /usr/lib/python3/dist-packages/rosdep2/
COPY ros_bypass/__init__.py /usr/lib/python3/dist-packages/rosdistro/
COPY ros_bypass/20-default.list /etc/ros/rosdep/sources.list.d/
# Install ur_driver 
RUN apt-get update && \
    apt-get install ros-${ROS_DISTRO}-ur-robot-driver -y
# Install dependencies
RUN /bin/bash -c "cd ~/ros_ws && \
    rosdep update && \
    rosdep install --ignore-src --from-paths src -y -r"
# Build    
RUN /bin/bash -c "cd ~/ros_ws && \
    source /opt/ros/$ROS_DISTRO/setup.bash && \
    colcon build --symlink-install --cmake-args -DCMAKE_BUILD_TYPE=Release && \
    source install/setup.bash"    
    
RUN echo "source /opt/ros/$ROS_DISTRO/setup.bash" >> ~/.bashrc
