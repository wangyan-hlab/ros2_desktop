FROM althack/ros2:humble-full
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

RUN git clone https://github.com/ros/rosdistro.git /etc/ros/ros_github/rosdistro/
COPY ros_bypass/rep3.py /usr/lib/python3/dist-packages/rosdep2/
COPY ros_bypass/__init__.py /usr/lib/python3/dist-packages/rosdistro/
COPY ros_bypass/20-default.list /etc/ros/rosdep/sources.list.d/

# Install UR_ROS2_Driver    
RUN apt-get install ros-${ROS_DISTRO}-ur-robot-driver -y

# Build the workspace
RUN /bin/bash -c cd ~/ros_ws/src && \
   git clone https://github.com/UniversalRobots/Universal_Robots_ROS2_Driver.git glozzom

RUN /bin/bash -c cd ~/ros_ws && \ 
    rosdep update && \
    rosdep install --ignore-src --from-paths src -y -r
    
RUN /bin/bash -c "source /opt/ros/$ROS_DISTRO/setup.bash"
RUN colcon build --symlink-install --cmake-args -DCMAKE_BUILD_TYPE=Release && \
    /bin/bash -c "source install/setup.bash"    
    
RUN echo "source /opt/ros/$ROS_DISTRO/setup.bash" >> ~/.bashrc
