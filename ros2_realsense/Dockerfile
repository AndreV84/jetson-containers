FROM nvcr.io/nvidia/l4t-base:r32.4.3
RUN apt-get update -y
RUN apt install -y wget curl git
#RUN /bin/bash  -c 'echo "deb http://packages.ros.org/ros/ubuntu bionic main" > /etc/apt/sources.list.d/ros-latest.list'
#RUN  apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
RUN apt-get update -y
RUN locale-gen en_US en_US.UTF-8 && update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8 && LANG=en_US.UTF-8
RUN DEBIAN_FRONTEND="noninteractive"  apt install -y curl gnupg2 lsb-release
RUN curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc |  apt-key add - && sh -c 'echo "deb http://packages.ros.org/ros2/ubuntu `lsb_release -cs` main" > /etc/apt/sources.list.d/ros2-latest.list'
RUN apt update -y
RUN apt-get update -y
ENV TZ America/Los_Angeles
RUN DEBIAN_FRONTEND="noninteractive" apt-get install -y tzdata git curl cmake wget mc mlocate 
RUN DEBIAN_FRONTEND="noninteractive" apt install -y ros-dashing-ros-base
RUN apt update -y 
RUN DEBIAN_FRONTEND="noninteractive" apt install -y ros-dashing-cv-bridge ros-dashing-librealsense2 ros-dashing-message-filters ros-dashing-image-transport
RUN DEBIAN_FRONTEND="noninteractive" apt install -y  libssl-dev libusb-1.0-0-dev pkg-config libgtk-3-dev libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev
RUN DEBIAN_FRONTEND="noninteractive" apt install -y  ros-dashing-realsense-camera-msgs ros-dashing-realsense-ros2-camera
RUN dpkg-reconfigure --frontend noninteractive tzdata
RUN rm -rf /var/lib/apt/lists
WORKDIR /home/nvidia/ros2_ws
RUN  mkdir -p ~/src && cd ~/src && git clone https://github.com/intel/ros2_intel_realsense.git
RUN  sh -c 'echo "deb [arch=amd64,arm64] http://repo.ros2.org/ubuntu/main `lsb_release -cs` main" > /etc/apt/sources.list.d/ros2-latest.list'
RUN curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc |  apt-key add -
RUN apt-get update -y
RUN apt install -y python3-colcon-common-extensions
RUN cd ~ &&  /bin/bash -c '. /opt/ros/dashing/setup.bash; colcon build --base-paths src/ros2_intel_realsense'
