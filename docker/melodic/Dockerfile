FROM ros:melodic-robot

# Update
RUN apt update
RUN apt-get install software-properties-common apt-utils -y

# Set working directory
WORKDIR /home/ros/src

# Get the realsense package from git
RUN git clone https://github.com/appliedAI-Initiative/orb_slam_2_ros.git

# Set up Melodic keys
RUN apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

# Install required ROS packages
RUN apt-get update && \
    apt-get install ros-melodic-tf2-geometry-msgs python-catkin-tools -y

WORKDIR /home/ros

# Install ROS dependencies
RUN rosdep update \
&& rosdep install --from-paths src --ignore-src -r -y --skip-keys=librealsense2

# build ros package source
RUN catkin config \
      --extend /opt/ros/$ROS_DISTRO && \
    catkin build

RUN echo "source /home/ros/devel/setup.bash" >> /$HOME/.bashrc
COPY launch /home/ros/launch
CMD "bash"